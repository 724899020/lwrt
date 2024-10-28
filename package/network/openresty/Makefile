# SPDX-License-Identifier: GPL-2.0
#
# OpenResty Makefile for OpenWRT

# 引入 OpenWRT 的通用规则文件 rules.mk
include $(TOPDIR)/rules.mk

# 包基本信息
PKG_NAME:=openresty                # 定义包名为 openresty
PKG_VERSION:=1.27.1.1              # 指定 OpenResty 的版本号
PKG_RELEASE:=1                     # 包的发布版本号

# 定义源代码文件的名称、下载链接和校验值
PKG_SOURCE:=openresty-$(PKG_VERSION).tar.gz  # 源代码文件名
PKG_SOURCE_URL:=https://openresty.org/download/  # 下载源代码的 URL
PKG_HASH:=skip  # 校验值，开发阶段可以先用 skip，后续可使用 make package/openresty/check 获取并填写

# 定义编译目录和许可证信息
PKG_BUILD_DIR:=$(BUILD_DIR)/openresty-$(PKG_VERSION)  # 解压和编译目录

PKG_LICENSE:=BSD-2-Clause              # 定义许可证类型
PKG_LICENSE_FILES:=LICENSE             # 指定许可证文件

# 包含包构建所需的通用定义
include $(INCLUDE_DIR)/package.mk

# 定义包的基本信息，便于在 OpenWRT 的菜单中显示
define Package/openresty
  SECTION:=net                          # 包的类别
  CATEGORY:=Network                     # 包在 OpenWRT 菜单中的分类
  TITLE:=OpenResty - A Scalable Web Platform by Extending NGINX with Lua  # 包的标题
  URL:=https://openresty.org/           # 包的官网地址
  DEPENDS:=+libpcre +zlib +openssl +luajit  # 定义包的依赖项
endef

# 包的详细描述
define Package/openresty/description
  OpenResty 是一个可扩展的 Web 平台，通过 Lua 脚本扩展了 NGINX 的功能。
endef

# 配置编译选项
define Build/Configure
	# 使用默认的配置命令，并启用 LuaJIT 和 HTTP SSL 模块
	$(call Build/Configure/Default,--with-luajit --with-http_ssl_module)
endef

# 编译安装指令
define Build/Install
	# 创建目标目录并将编译生成的 nginx 文件安装到 /usr/sbin/openresty
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/build/nginx/sbin/nginx $(1)/usr/sbin/openresty
endef

# 定义包安装的内容及路径
define Package/openresty/install
	# 创建安装目录并将 openresty 可执行文件放置在 /usr/sbin 下
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/build/nginx/sbin/nginx $(1)/usr/sbin/openresty
	# 将初始化脚本 openresty.init 放入 /etc/init.d，确保服务能启动和停止
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/openresty.init $(1)/etc/init.d/openresty
endef

# 启动构建过程，定义并构建 openresty 包
$(eval $(call BuildPackage,openresty))
