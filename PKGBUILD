# Maintainer: Yurii Kolesnykov <root@yurikoles.com>
# Contributor: Solomon Choina <shlomochoina@gmail.com>
#
# Pull Requests are welcome: https://github.com/yurikoles-aur/kcm-grub2-git

pkgname=kcm-grub2-git
_product="${pkgname%-git}"
pkgver=0.6.4.r269.g6262f8d
pkgrel=1
pkgdesc="A KDE Control Module for configuring the GRUB2 bootloader"
arch=('x86_64')
url='https://invent.kde.org/system/kcm-grub2'
license=('GPL-3.0-or-later')
depends=(
    'grub'
    'hwinfo'
    'kcmutils5'
    'libmagick'
)
makedepends=(
    'cmake'
    'extra-cmake-modules'
    'git'
    'kdoctools5'
)

conflicts=('grub2-editor-frameworks')
provides=('grub2-editor-frameworks')
optdepends=('os-prober: To detect other OSes when generating grub.cfg in BIOS systems')
source=("${_product}"::"git+${url}.git")
sha256sums=('SKIP')

pkgver() {
  cd "${_product}"
  # cutting off 'v' prefix that presents in the git tag
  git describe --long --tags | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
    export PKG_CONFIG_PATH='/usr/lib/imagemagick6/pkgconfig'
    cmake -B build -S "${_product}" \
       -D BUILD_TESTING=OFF \
       -Wno-dev

   cmake --build build
}

package() {
	 DESTDIR="${pkgdir}" cmake --install build
}
