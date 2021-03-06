include $(SUPPORT_DIR)/functions.mk

NAME := gst-plugins-base
TARGET_DEPENDENCIES := gstreamer alsa-lib xlib
SOURCE := $(SOURCES_DIR)/gst-plugins-base-1.12.3.tar.xz
SOURCE_URL := https://gstreamer.freedesktop.org/src/gst-plugins-base/gst-plugins-base-1.12.3.tar.xz
MD5 := e69d41472a9b08eaf9659cde5dc0a4a4

system:
	@export CC=$(TOOLS_DIR)/bin/$(CONFIG_TARGET)-gcc
	@export CXX=$(TOOLS_DIR)/bin/$(CONFIG_TARGET)-g++
	@export AR=$(TOOLS_DIR)/bin/$(CONFIG_TARGET)-ar
	@export AS=$(TOOLS_DIR)/bin/$(CONFIG_TARGET)-as
	@export LD=$(TOOLS_DIR)/bin/$(CONFIG_TARGET)-ld
	@export RANLIB=$(TOOLS_DIR)/bin/$(CONFIG_TARGET)-ranlib
	@export READELF=$(TOOLS_DIR)/bin/$(CONFIG_TARGET)-readelf
	@export STRIP=$(TOOLS_DIR)/bin/$(CONFIG_TARGET)-strip
	@$(STEP) "gst-plugins-base 1.12.3"
	@$(call check_source, $(SOURCE), $(MD5), $(SOURCE_URL))
	@$(call system_dependencies, $(TARGET_DEPENDENCIES))
	@$(EXTRACT) $(SOURCE) $(BUILD_DIR)
	@( cd $(BUILD_DIR)/gst-plugins-base-1.12.3 && \
	PKG_CONFIG="$(TOOLS_DIR)/bin/pkg-config" \
	ac_cv_lbl_unaligned_fail=yes \
	ac_cv_func_mmap_fixed_mapped=yes \
	ac_cv_func_memcmp_working=yes \
	ac_cv_have_decl_malloc=yes \
	gl_cv_func_malloc_0_nonnull=yes \
	ac_cv_func_malloc_0_nonnull=yes \
	ac_cv_func_calloc_0_nonnull=yes \
	ac_cv_func_realloc_0_nonnull=yes \
	lt_cv_sys_lib_search_path_spec="" \
	ac_cv_c_bigendian=no \
	CONFIG_SITE=/dev/null \
	./configure \
	--target=$(CONFIG_TARGET) \
	--host=$(CONFIG_TARGET) \
	--build=$(CONFIG_HOST) \
	--prefix=/usr \
	--exec-prefix=/usr \
	--sysconfdir=/etc \
	--localstatedir=/var \
	--program-prefix="" \
	--disable-static \
	--enable-shared \
	--with-package-name="$(CONFIG_PKG_VERSION)" \
	--with-package-origin="$(CONFIG_BUG_URL)" )
	@make -j$(CONFIG_PARALLEL_JOBS) -C $(BUILD_DIR)/gst-plugins-base-1.12.3
	@make -j$(CONFIG_PARALLEL_JOBS) DESTDIR=$(SYSROOT_DIR) install -C $(BUILD_DIR)/gst-plugins-base-1.12.3
	@$(call dependency_libs_patch)
	@make -j$(CONFIG_PARALLEL_JOBS) DESTDIR=$(ROOTFS_DIR) install -C $(BUILD_DIR)/gst-plugins-base-1.12.3
	@rm -rf $(BUILD_DIR)/gst-plugins-base-1.12.3
	@echo $(NAME) >> $(SYSTEM_DEPENDENCIES)
