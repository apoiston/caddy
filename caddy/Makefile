include $(TOPDIR)/rules.mk

PKG_NAME:=caddy
PKG_VERSION:=2.11.4
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/caddyserver/caddy/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=2c3d02078286a6282cdb4d1d8744077788d556659dac0b64d8ed5886a7e5aeb9

PKG_LICENSE:=Apache-2.0
PKG_MAINTAINER:=apois

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1

GO_PKG:=github.com/caddyserver/caddy/v2
GO_PKG_BUILD_PKG:=github.com/caddyserver/caddy/v2/cmd/caddy
GO_PKG_LDFLAGS_X:=$(GO_PKG).CustomVersion=v$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/golang/golang-package.mk

define Package/caddy
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Caddy File Server
  URL:=https://caddyserver.com/
  DEPENDS:=$(GO_ARCH_DEPENDS) +ca-certificates
endef

define Package/caddy/description
  A file server built using Caddy.
endef

define Package/caddy/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(GO_PKG_BUILD_BIN_DIR)/caddy $(1)/usr/bin/caddy

	$(INSTALL_DIR) $(1)/etc/caddy
	$(INSTALL_DIR) $(1)/etc/caddy/conf.d
	$(INSTALL_DATA) ./files/Caddyfile $(1)/etc/caddy/Caddyfile

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/caddy.init $(1)/etc/init.d/caddy
endef

$(eval $(call BuildPackage,caddy))
