# Maintainer: Caleb Maclennan <caleb@alerque.com>

pkgname=python-dvc-data
_pkgname=${pkgname#python-}
pkgver=0.28.1
pkgrel=1
pkgdesc='DVC’s data management subsystem'
arch=(any)
license=(Apache)
url="https://github.com/iterative/$_pkgname"
_pydeps=(dictdiffer
         dvc-objects
         funcy
         pygtrie
         shortuuid)
depends=(python
        "${_pydeps[@]/#/python-}")
makedepends=(python-{build,installer} python-setuptools-scm python-wheel)
_archive=("$_pkgname-$pkgver")
source=("https://files.pythonhosted.org/packages/source/${_pkgname::1}/$_pkgname/$_archive.tar.gz")
sha256sums=('4a3af4396c8522ea47c6b55d43b8e8359bd87e7d113bc18706929259046e51bf')

build() {
	cd "$_archive"
	python -m build -wn
}

package() {
	cd "$_archive"
	python -m installer -d "$pkgdir" dist/*.whl
}
