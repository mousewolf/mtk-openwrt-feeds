include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/version.mk

PKG_NAME:=mt7628
PKG_RELEASE:=1
PKG_BUILD_DEPENDS:=base-files
PKG_FILE_DEPENDS:=
PKG_LICENSE:=GPL-2.0

PKG_MAINTAINER:=Hua Shao <nossiac@163.com>
PKG_URLS:=http://nossiac.com/download/mtk-wifi-ko \
	http://119.23.148.191:8888/mtk-wifi-ko


include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/kernel.mk

define Package/mt7628
  CATEGORY:=MTK Properties
  SUBMENU:=Drivers
  TITLE:=MTK MT7628 WiFi AP driver
  AUTOLOAD:=$(call AutoProbe,mt7628)
endef


define Package/mt7628/config-notyet
	config MT7628_USING_LUA_SCRIPT
		bool "use lua script to init/config driver"
		depends on PACKAGE_mt7628
		default y
endef


define Build/Compile
	for PKG_URL in $(PKG_URLS); do \
		wget $$$${PKG_URL}/$(PKG_NAME)-linux-$(LINUX_VERSION).ko \
			-O $(PKG_BUILD_DIR)/$(PKG_NAME)-linux-$(LINUX_VERSION).ko; \
		if [ "$$$$?" != "0" ]; then continue; else break; fi \
	done
endef

define Package/mt7628/install
	$(INSTALL_DIR) $(1)/lib/modules/$(LINUX_VERSION)
	-$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(PKG_NAME)-linux-$(LINUX_VERSION).ko \
		$(1)/lib/modules/$(LINUX_VERSION)/$(PKG_NAME).ko
	$(CP) ./files/* $(1)/
endef

$(eval $(call BuildPackage,mt7628))
