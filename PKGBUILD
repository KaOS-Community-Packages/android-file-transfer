pkgname=android-file-transfer
pkgver=4.3
pkgrel=1
pkgdesc='Android MTP client with a minimalistic UI'
arch=('x86_64')
url='https://whoozle.github.io/android-file-transfer-linux'
license=('LGPL 2.1')
depends=('qt5-base' 'fuse' 'fuse3' 'libxkbcommon' 'libxkbfile' 'hicolor-icon-theme')
makedepends=('cmake' 'qt5-tools')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/MartinVonReichenberg/android-file-transfer/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('SKIP')

build() {
  cd $pkgname-$pkgver
  cmake -DCMAKE_INSTALL_PREFIX=/usr . -DCMAKE_CXX_FLAGS="$CXXFLAGS -ffat-lto-objects"
  make
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir/" install
}
