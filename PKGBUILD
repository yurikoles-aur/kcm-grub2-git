# Maintainer: Yurii Kolesnykov <root@yurikoles.com>
# Contributor: Solomon Choina <shlomochoina@gmail.com>
#
# Pull Requests are welcome here: https://github.com/yurikoles-aur/kcm-grub2-git
#

pkgname=kcm-grub2-git
_product="${pkgname%-git}"
pkgver=0.6.4.r280.gef91a2a
_branch='work/nico/qt6'
pkgrel=1
pkgdesc="A KDE Control Module for configuring the GRUB2 bootloader"
arch=('x86_64')
url='https://invent.kde.org/system/kcm-grub2'
license=('GPL-3.0-or-later')
depends=(
	'grub'
	'hwinfo'
	'kcmutils'
	'libmagick'
)
makedepends=(
    'cmake'
	'extra-cmake-modules'
	'git'
	'packagekit-qt6'
)
conflicts=('grub2-editor-frameworks')
provides=('grub2-editor-frameworks')
optdepends=(
	'os-prober: To detect other OSes when generating grub.cfg in BIOS systems'
	'packagekit-qt6'
)
source=("${_product}::git+${url}.git#branch=${_branch}")
sha256sums=('SKIP')

pkgver() {
	cd "${_product}"
	# cutting off 'v' prefix that presents in the git tag
	git describe --long --tags | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
	cmake -B build -S "${_product}" \
		-D BUILD_TESTING=OFF \
		-Wno-dev
	cmake --build build
}

package() {
	DESTDIR="${pkgdir}" cmake --install build
}
