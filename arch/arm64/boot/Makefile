OBJCOPYFLAGS_Image := -O binary -R .note -R .note.gnu.build-id -R .comment -S

targets := Image Image.bz2 Image.gz Image.lz4 Image.lzma Image.lzo

# ==== 手動加入自訂 DTB ====
MY_DTB := $(srctree)/camellia.dtb
DTB_OBJS := $(MY_DTB)
# =========================

$(obj)/Image: vmlinux FORCE
	$(call if_changed,objcopy)

$(obj)/Image.gz: $(obj)/Image FORCE
	$(call if_changed,gzip)

$(obj)/Image-dtb: $(obj)/Image $(DTB_OBJS) FORCE
	$(call if_changed,cat)

$(obj)/Image.gz-dtb: $(obj)/Image.gz $(DTB_OBJS) FORCE
	$(call if_changed,cat)
