# Maintainer: Sven-Hendrik Haase <sh@lutzhaase.com>
# Contributor: Daenyth <Daenyth+Arch [AT] gmail [DOT] com>
# Contributor: Allan McRae <allan@archlinux.org>
# Contributor: rabyte <rabyte__gmail>

pkgname=supertuxkart
pkgver=0.10.rc1
_pkgver=0.10-rc1
pkgrel=1
pkgdesc='Kart racing game featuring Tux and his friends'
arch=('x86_64')
url='http://supertuxkart.sourceforge.net/'
license=('GPL2')
depends=('openal' 'libvorbis' 'fribidi' 'curl' 'bluez-libs' 'libxrandr' 'glu')
makedepends=('cmake' 'subversion' 'mesa' 'imagemagick' 'setconf' 'mesa-libgl')
source=("https://downloads.sourceforge.net/${pkgname}/${pkgname}-${_pkgver}-src.tar.xz")
sha512sums=('13db484a317bac86b5d799250022638b27b0b0b4739d6bb6c96fd97e89cac639c95a5bfd98b5bb1ec780499544e0a745c278f67dea0a1d67a65802a4e0f0b221')

build() {
  cd ${srcdir}/supertuxkart-${_pkgver}

  _fn="data/${pkgname}.desktop"
  setconf "$_fn" Exec "$pkgname"
  setconf "$_fn" TryExec "$pkgname"
  setconf "$_fn" Icon "$pkgname"

  [[ -d build ]] && rm -r build
  mkdir build && cd build

  cmake .. \
    -DIRRLICHT_DIR="$srcdir/irrlicht" \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DBUILD_RECORDER=0 \
    -DCMAKE_CXX_FLAGS="-lpthread -lm -ldl $CXXFLAGS -std=gnu++98"

  make
}

package() {
  cd ${srcdir}/supertuxkart-${_pkgver}

  cd build
  make DESTDIR=${pkgdir} install
}

# vim:set ts=2 sw=2 et:
