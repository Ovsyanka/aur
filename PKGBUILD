# Maintainer: Chocobo1 <chocobo1 AT archlinux DOT net>

pkgname=typst-lsp
pkgver=0.4.1
pkgrel=1
pkgdesc="Language server for Typst"
arch=('i686' 'x86_64')
url="https://github.com/nvarner/typst-lsp"
license=('Apache' 'MIT')
depends=('gcc-libs')
makedepends=('rust')
source=("$pkgname-$pkgver-src.tar.gz::https://github.com/nvarner/typst-lsp/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('e8b7b678dbfaa531c130382afdc22a42c6934d894971b82160ca652c91615605')


prepare() {
  cd "typst-lsp-$pkgver"

  if [ ! -f "Cargo.lock" ]; then
    cargo update
  fi
  cargo fetch
}

check() {
  cd "typst-lsp-$pkgver"

  #cargo test \
  #  --frozen
}

package() {
  cd "typst-lsp-$pkgver"

  cargo install \
    --locked \
    --no-track \
    --root "$pkgdir/usr" \
    --path .

  install -Dm644 "LICENSE-MIT.txt" -t "$pkgdir/usr/share/licenses/typst-lsp"
}
