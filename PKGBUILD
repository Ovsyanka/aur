# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Contributor: Yann Büchau <nobodyinperson@posteo.de>

pkgname=hledger-utils
pkgver=1.12.1
pkgrel=1
epoch=
pkgdesc='Utilities extending the hledger plaintextaccounting tool'
arch=(any)
url="https://gitlab.com/nobodyinperson/$pkgname"
license=(GPL)
depends=(hledger
         python
         python-psutil
         python-rich)
makedepends=(python-{build,installer,wheel}
             python-setuptools-scm)
_archive="$pkgname-$pkgver"
source=("https://files.pythonhosted.org/packages/source/${pkgname::1}/$pkgname/$_archive.tar.gz")
sha256sums=('fafeb6ef38f0cb9b793148d0262a0d9112eb70e808f4bc4076c72f6ab3a2907c')

build () {
	cd "$_archive"
	python -m build -wn
}

package () {
	cd "$_archive"
	python -m installer -d "$pkgdir" dist/*.whl
}
