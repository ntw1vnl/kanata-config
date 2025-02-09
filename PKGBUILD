# Maintainer: fenuks

pkgname=kanata
pkgver=1.8.0
pkgrel=1
pkgdesc="Bring the customizability of a QMK board to any keyboard near you"
arch=('i686' 'pentium4' 'x86_64' 'arm' 'armv7h' 'armv6h' 'aarch64')
url="https://github.com/jtroo/kanata"
license=("LGPL-3.0")
depends=(libevdev)
optdepends=()
makedepends=(cargo)
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/refs/tags/v${pkgver}.tar.gz"
        'kanata.service'
)
sha256sums=('396a379d7620001531b856913a2677baa56fa16c5c9d329f6937dfb57d3ac704'
            '02f657a0d3e6c2621d74282b192c45bbfba868a26c35fe0f351cb77c3c666e55')

prepare() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  export RUSTUP_TOOLCHAIN=stable
  cargo fetch --target "${CARCH}-unknown-linux-gnu"
}

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  export RUSTUP_TOOLCHAIN=stable
  export CARGO_TARGET_DIR=target
  cargo build --frozen --release
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  install -Dm0755 -t "$pkgdir/usr/bin/" "target/release/${pkgname}"
  install -Dm0644 -t "$pkgdir/usr/lib/systemd/system/" "${srcdir}/kanata.service"
}
