# Maintainer: Kuba Serafinowski <zizzfizzix(at)gmail(dot)com>
# Contributor: Teo Mrnjavac <teo@kde.org>
# https://github.com/zizzfizzix/pkgbuilds

# What type of build do you want?
# See http://techbase.kde.org/Development/CMake/Addons_for_KDE#Buildtypes to check what is supported.

_buildtype='Release'

_pkgname=qtkeychain
pkgname=qtkeychain-qt5
pkgver=0.3
pkgrel=2
pkgdesc='Provides support for secure credentials storage.'
arch=('i686' 'x86_64' 'armv7h')
url='https://github.com/frankosterfeld/qtkeychain'
license=('BSD')
depends=('qt5-base' 'qt5-tools')
makedepends=('cmake' 'icu')
source=("${_pkgname}-${pkgver}.zip::https://github.com/frankosterfeld/qtkeychain/archive/${pkgver}.zip")
md5sums=('8a82d813969fd1144d1d06769a2476f8')

if [[ ! ${_buildtype} == 'Release' ]] && [[ ! ${_buildtype} == 'release' ]]; then
  options=('debug')
fi

prepare() {
    if [[ -e ${srcdir}/${_pkgname}-${pkgver}-build ]]; then rm -rf ${srcdir}/${_pkgname}-${pkgver}-build; fi
    mkdir ${srcdir}/${_pkgname}-${pkgver}-build
}

build() {
    cd ${srcdir}/${_pkgname}-${pkgver}-build
    cmake -DCMAKE_INSTALL_PREFIX=/usr \
          -DCMAKE_INSTALL_LIBDIR=lib \
          -DCMAKE_INSTALL_LIBEXECDIR=lib/${pkgname} \
          -DCMAKE_BUILD_TYPE=${_buildtype} \
          ../${_pkgname}-${pkgver}
    make
}

package() {
    cd ${srcdir}/${_pkgname}-${pkgver}-build
    make DESTDIR=${pkgdir} install
    install -D -m644 ${srcdir}/${_pkgname}-${pkgver}/COPYING ${pkgdir}/usr/share/licenses/${pkgname}/LICENSE
}
