# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Contributor: William Turner <willtur.will@gmail.com>

pkgname=afdko
pkgver=3.8.1
pkgrel=1
pkgdesc='Adobe Font Development Kit for OpenType'
arch=(x86_64)
url="https://github.com/adobe-type-tools/$pkgname"
license=(custom)
_py_deps=(booleanoperations
          brotli # for fonttools[woff]
          defcon
          fontmath
          fontparts
          fontpens # for defcon[pens]
          fonttools
          fs # for fonttools[ufo]
          lxml # for fonttools[lxml] and defcon[lxml]
          tqdm
          ufonormalizer
          ufoprocessor
          unicodedata2 # for fonttools[unicode]
          zopfli) # for fonttools[woff]
depends=(python
        "${_py_deps[@]/#/python-}"
        psautohint)
makedepends=(cmake
             git # Upstream Issue: https://github.com/adobe-type-tools/afdko/issues/1407
             python-setuptools-scm
             python-scikit-build)
checkdepends=(python-pytest)
_archive="$pkgname-$pkgver"
source=("$url/releases/download/$pkgver/$_archive.tar.gz")
sha256sums=('05a4a9c3b4e2072982be83f4ff3d73ca758a4091ff3e36db19ff39648f4b399c')

prepare () {
	cd "$_archive"
	sed -i -e 's/==/>=/g;s/,<=[0-9.]\+//' requirements.txt
	sed -i -E "/'(wheel|cmake|ninja)',?$/d" setup.py
}

build() {
	cd "$_archive"
	python setup.py build_ext
	python setup.py build
}

check() {
	cd "$_archive"
	# Upstream test suite uses vendored deps and the paths are foobared
	# PYTHONPATH=python pytest
}

package() {
	cd "$_archive"
	export PYTHONHASHSEED=0
	python setup.py -q install --root="$pkgdir" --optimize=1 --skip-build
	install -Dm644  -t "$pkgdir/usr/share/licenses/$pkgname/" LICENSE.md
}
