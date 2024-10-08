# Wiki OpenIPC
[Mục lục](../README.md)

**CHỈ** dành cho bo mạch XM với SoC GK7202V300, GK7205V200, GK7205V300!!!
-----------------------------------------------------------------

### Cảm biến được hỗ trợ

Vui lòng tra cứu cảm biến của bạn trong [danh sách thiết bị được hỗ trợ][1].

### Cập nhật firmware thiết bị ban đầu

```
setenv bootargs 'mem=${osmem:-32M} console=ttyAMA0,115200 panic=20 root=/dev/mtdblock3 rootfstype=squashfs init=/init mtdparts=sfc:256k(boot),64k(env),2048k(kernel),5120k(rootfs),-(rootfs_data)'
setenv bootcmd 'setenv setargs setenv bootargs ${bootargs}; run setargs; sf probe 0; sf read 0x42000000 0x50000 0x200000; bootm 0x42000000'
setenv uk 'mw.b 0x42000000 ff 1000000; tftp 0x42000000 uImage.${soc} && sf probe 0; sf erase 0x50000 0x200000; sf write 0x42000000 0x50000 ${filesize}'
setenv ur 'mw.b 0x42000000 ff 1000000; tftp 0x42000000 rootfs.squashfs.${soc} && sf probe 0; sf erase 0x250000 0x500000; sf write 0x42000000 0x250000 ${filesize}'
saveenv

setenv soc gk7xxxxxxx            # Đặt SoC của bạn. gk7202v300, gk7205v200, hoặc gk7205v300.
setenv osmem 32M
setenv totalmem 64M              # 64M cho gk7202v300, gk7205v200, 128M cho gk7205v300.
setenv ipaddr 192.168.1.10
setenv serverip 192.168.1.254    # Địa chỉ IP của máy chủ TFTP của bạn.
saveenv

run uk; run ur; reset            # Flash kernel, rootfs và khởi động lại thiết bị
```

### Cập nhật nhanh tiếp theo

```
run uk; run ur; reset
```

### Mẹo dành cho người dùng GK7205V300+IMX335

```
echo -e "!/bin/sh\n\ndevmem 0x120100f0 32 0x19\n" >/etc/init.d/S96trick
chmod +x /etc/init.d/S96trick
```

Cách thay thế [tại đây](https://github.com/OpenIPC/firmware/pull/117/files)

### Khu vực nguy hiểm

Bạn luôn có tùy chọn cập nhật bootloader. Tuy nhiên, bạn cần phải hiểu rõ những gì bạn đang làm.

Lưu ý! Thay thế tên tệp bootloader bằng tên tệp phù hợp với SoC của bạn.
Danh sách đầy đủ có [tại đây](https://github.com/OpenIPC/firmware/releases/tag/latest).

```
mw.b 0x42000000 ff 1000000
tftp 0x42000000 u-boot-gk7xxxxxxxx-beta.bin
sf probe 0
sf erase 0x0 0x50000
sf write 0x42000000 0x0 ${filesize}
reset
```

[1]: guide-supported-devices.md
