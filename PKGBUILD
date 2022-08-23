# Maintainer: alzeih <alzeih@users.noreply.github.com>
# Maintainer: Caleb Maclennan <caleb@alerque.com>

pkgname=mod_auth_openidc
pkgver=2.4.11.3
pkgrel=1
pkgdesc='OpenID Connect Relying Party implementation for Apache 2.x'
arch=(x86_64)
url=https://www.mod-auth-openidc.org
license=(Apache)
depends=(cjose openssl pcre2)
_archive="$pkgname-$pkgver"
makedepends=(apache jansson)
source=("https://github.com/zmartzone/$pkgname/releases/download/v$pkgver/$_archive.tar.gz")
sha256sums=('f71dfbe202832ecf1b71a83d5c299ad3c068ae286a7fcef8eb21b3e65a872ce9')

build() {
	cd "$_archive"
	./configure --prefix=/usr
	make
}

package() {
	cd "$_archive"
	make DESTDIR="$pkgdir" install
}

