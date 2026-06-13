include $(TOPDIR)/rules.mk

PKG_NAME:=opera-proxy
PKG_VERSION:=1.24.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/oskord-sudo/opera-proxy2.git
PKG_SOURCE_VERSION:=master
PKG_MIRROR_HASH:=skip

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/opera-proxy
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Opera VPN/Proxy service
  URL:=https://github.com/oskord-sudo/opera-proxy2
  DEPENDS:=+ca-bundle
endef

define Build/Compile
	( \
		cd $(PKG_BUILD_DIR); \
		export GO111MODULE=on; \
		export GOPROXY=https://proxy.golang.org; \
		export GOOS=linux; \
		export GOARCH=amd64; \
		export CGO_ENABLED=0; \
		go mod tidy; \
		go build -o opera-proxy . ; \
	)
endef

define Package/opera-proxy/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/opera-proxy $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/opera-proxy.init $(1)/etc/init.d/opera-proxy

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DATA) ./files/opera-proxy.config $(1)/etc/config/opera-proxy
endef

$(eval $(call BuildPackage,opera-proxy))
