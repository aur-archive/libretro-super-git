_name=libretro-super
pkgdesc="A collection of libretro implementations for RetroArch."
license=('various')
arch=('i686' 'x86_64')

url="https://github.com/libretro/${_name}"
source=("git://github.com/libretro/${_name}.git")
pkgname=${_name}-git
pkgver=938.dead658
pkgrel=1
makedepends=('git')
provides=("${_name}")
conflicts=("${_name}")
md5sums=('SKIP')

pkgver() {
	cd "${_name}"
	echo "$(git rev-list --count HEAD).$(git describe --always)"
}

build() {
	cd "${_name}"
	./libretro-fetch.sh

	## Disable Broken Cores Temporarily
	sed -i -e '/build_libretro_emux/d' libretro-build.sh

	## Build Cores
	RARCH_DIST_DIR="${srcdir}/dist/libretro" ./libretro-build.sh
	RARCH_DIST_DIR="${srcdir}/dist/libretro" PARTIAL=1 ./libretro-build.sh build_libretro_mess
	RARCH_DIST_DIR="${srcdir}/dist/libretro" PARTIAL=1 ./libretro-build.sh build_libretro_ume
}

package() {
	install -dm755 "${pkgdir}/usr/lib/libretro/"
	install -m644 libretro-super/dist/info/*.info "${pkgdir}/usr/lib/libretro/"
	install -m644 dist/libretro/*.so "${pkgdir}/usr/lib/libretro/"
}

