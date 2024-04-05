pkgname=android-file-transfer
_pkgname=android-file-transfer-linux
pkgver=4.3
pkgrel=2
pkgdesc="A reliable MTP client with a minimalistic UI similar to official Android File Transfer by Google. It just works."
arch=('x86_64')
url="https://whoozle.github.io/android-file-transfer-linux/"
license=('GPL3')
depends=('systemd' 'qt6-base' 'file' 'glibc' 'gcc-libs' 'readline' 'fuse'
         'fuse' 'libxkbcommon'  'hicolor-icon-theme' 'taglib' 'openssl' 'zlib')
makedepends=('qt6-tools' 'cmake' 'ninja')
provides=('android-file-transfer' 'aft-mtp-cli' 'aft-mtp-mount')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/whoozle/${_pkgname}/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('SKIP')

prepare() {
  mkdir -p "${srcdir}/${_pkgname}-${pkgver}/build/"
}

build() {
  cmake -S "${srcdir}/${_pkgname}-${pkgver}/" \
        -B "${srcdir}/${_pkgname}-${pkgver}/build/" \
        -G Ninja -DCMAKE_INSTALL_PREFIX="/usr/" \
        -DCMAKE_CXX_FLAGS="$CXXFLAGS -ffat-lto-objects" \
        -DCMAKE_EXE_LINKER_FLAGS=-Wl,-O1,--sort-common,-z,relro,-z,now

  ninja -C "${srcdir}/${_pkgname}-${pkgver}/build/" all
}

package() {
  DESTDIR="${pkgdir}" ninja -C "${srcdir}/${_pkgname}-${pkgver}/build/" install

  install -Dm644 "${srcdir}/${_pkgname}-${pkgver}/LICENSE" -t "${pkgdir}/usr/share/licenses/${pkgname}/"
  ln -s "/usr/bin/${pkgname}" "${pkgdir}/usr/bin/${_pkgname}"
}
