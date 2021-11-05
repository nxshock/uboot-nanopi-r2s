# U-Boot: NanoPi R2S/R2C

buildarch=8

pkgname=uboot-nanopi-r2s
pkgver=2021.10
pkgrel=1
pkgdesc="U-Boot for NanoPi R2S/R2C"
arch=('aarch64')
url='http://www.denx.de/wiki/U-Boot/WebHome'
license=('GPL')
backup=('boot/extlinux/extlinux.conf')
makedepends=('bc' 'git' 'python' 'swig' 'dtc')
install=${pkgname}.install
source=("ftp://ftp.denx.de/pub/u-boot/u-boot-${pkgver}.tar.bz2"
        "https://github.com/ARM-software/arm-trusted-firmware/archive/v2.5.tar.gz"
		"extlinux.conf")
md5sums=('f1392080facf59dd2c34096a5fd95d4c'
         'a3c01d2a73d5171e3f1c0737ff5321d9'
		 'faf2b85206cb66c31f7c97da7b2b281d')

prepare() {
	cd ${srcdir}/arm-trusted-firmware-2.5
	make PLAT=rk3328

	cd ${srcdir}/u-boot-${pkgver}

	cd ${srcdir}/u-boot-${pkgver}/configs
	echo 'CONFIG_IDENT_STRING=" Arch Linux ARM"' >> nanopi-r2s-rk3328_defconfig
}

build() {
	cd ${srcdir}/u-boot-${pkgver}

	unset CLFAGS CXXFLAGS CPPFLAGS LDFLAGS
	export BL31=../arm-trusted-firmware-2.5/build/rk3328/release/bl31/bl31.elf

	make nanopi-r2s-rk3328_defconfig
	make
}

package() {
	cd u-boot-${pkgver}

	mkdir -p "${pkgdir}/boot/extlinux"

	cp ./u-boot-rockchip.bin   "${pkgdir}/boot/u-boot-rockchip.bin"
	cp ${srcdir}/extlinux.conf "${pkgdir}/boot/extlinux/extlinux.conf"
}
