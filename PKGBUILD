# Maintainer: Caleb Maclennan <caleb@alerque.com>

pkgname=gftools
pkgver=0.9.8
pkgrel=1
pkgdesc='Misc tools for working with the Google Fonts library'
arch=(any)
url="https://github.com/googlefonts/$pkgname"
license=(Apache)
_py_deps=(babelfont
          brotli
          browserstack-local
          fontfeatures
          fontmake
          fonttools
          fs # optdepends of fonttols required for [ufo]
          glyphslib
          glyphsets
          jinja
          opentype-sanitizer
          protobuf
          pyaml
          pybrowserstack-screenshots
          pygit2
          pygithub
          requests
          skia-pathops
          strictyaml
          tabulate
          ufolib2
          ttfautohint-py
          unidecode
          vttlib)
depends=(absl-py
         hyperglot
         python
         "${_py_deps[@]/#/python-}"
         statmake)
makedepends=(python-{build,installer}
             python-setuptools-scm
             python-wheel)
_archive="$pkgname-$pkgver"
source=("https://files.pythonhosted.org/packages/source/${pkgname::1}/$pkgname/$_archive.tar.gz")
sha256sums=('ee310d492f5b402eb0864f819e5a35ff27e0fc39d6f49491a59abd833a8ae3d3')

prepare() {
	cd "$_archive"
    sed -i -e "/setup_requires/s/>=.*'/'/" setup.py
}

build() {
	cd "$_archive"
	python -m build -wn
}

package() {
	cd "$_archive"
	python -m installer -d "$pkgdir" dist/*.whl
}
