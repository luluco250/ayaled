# Maintainer: Lucas Melo <luluco250 at gmail dot com>
# Contributor: Maya Matuszczyk maccraft123mc at gmail dot com>

pkgname=ayaled-updated
pkgver=0.6.0
pkgrel=1
pkgdesc="A daemon to manage joystick LEDs on AYANEO devices, updated fork."
arch=('x86_64')
makedepends=('cargo')
provides=('ayaled')
conflicts=('ayaled' 'ayaled2')

prepare() {
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  export RUSTUP_TOOLCHAIN=stable
  export CARGO_TARGET_DIR=target
  cargo build --frozen --release --all-features
}

check() {
  export RUSTUP_TOOLCHAIN=stable
  cargo test --frozen --all-features
}

package() {
  install -Dm0755 -t "$pkgdir/usr/bin/" "target/release/$pkgname"
  mkdir -p "$pkgdir/etc/systemd/system"
  install -m755 "$srcdir/ayaled.service" "$pkgdir/etc/systemd/system/ayaled.service"
}
