OBJCOPYFLAGS_Image := -O binary -R .note -R .note.gnu.build-id -R .comment -S

targets := Image Image.bz2 Image.gz Image.lz4 Image.lzma Image.lzo

# === 自訂 DTS 編譯規則 ===
MY_DTS := $(srctree)/arch/arm64/boot/camellia.dts
MY_DTB := $(obj)/camellia.dtb

$(MY_DTB): $(MY_DTS)
	@echo "  DTC     $@"
	$(DTC) -I dts -O dtb -o $@ $<
# ========================

$(obj)/Image: vmlinux FORCE
	$(call if_changed,objcopy)

$(obj)/Image.gz: $(obj)/Image FORCE
	$(call if_changed,gzip)

$(obj)/Image-dtb: $(obj)/Image $(DTB_OBJS) FORCE
	$(call if_changed,cat)

$(obj)/Image.gz-dtb: $(obj)/Image.gz $(DTB_OBJS) FORCE
	$(call if_changed,cat)
