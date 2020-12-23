# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Maintainer: Adrián Pérez de Castro <aperez@igalia.com>

pkgname=sile-git
pkgdesc='Modern typesetting system inspired by TeX'
pkgver=0.10.13.r3.g6024bde
pkgrel=1
arch=('x86_64')
url='https://www.sile-typesetter.org'
license=('MIT')
_lua_deps=('bit32'
           'cassowary'
           'cosmo'
           'cliargs'
           'expat'
           'filesystem'
           'linenoise'
           'lpeg'
           'luaepnf'
           'penlight'
           'repl'
           'sec'
           'socket'
           'stdlib'
           'vstruct'
           'zlib')
depends=('fontconfig'
         'freetype2'
         'harfbuzz'
         'gentium-plus-font'
         'icu'
         'libpng' # this goes with libtexpdf if ever split out to a library package
         'lua'
         "${_lua_deps[@]/#/lua-}"
         'zlib')
# Note find via find-deps; needs rebuilding any time versions of these change;
# currently missing several because parent packages are missing the provides=()
depends+=('libfreetype.so'
          'libharfbuzz.so'
          'libicudata.so'
          'libicui18n.so'
          'libicuio.so'
          'libicuuc.so')
makedepends=('git')
checkdepends=('poppler')
provides=('libtexpdf.so'
          "${pkgname%-git}=$pkgver")
conflicts=("${pkgname%-git}")
source=("git://github.com/sile-typesetter/${pkgname%-git}.git"
        "git://github.com/sile-typesetter/libtexpdf.git")
sha256sums=('SKIP' 'SKIP')

pkgver() {
    cd "${pkgname%-git}"
    git describe --long --tags --abbrev=7 --match="v*" HEAD |
        sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare () {
    cd "${pkgname%-git}"
    git submodule init
    git config submodule.libtexpdf.url "$srcdir/libtexpdf"
    git submodule update
    ./bootstrap.sh
}

build () {
    cd "${pkgname%-git}"
    ./configure \
        --prefix /usr \
        --docdir /usr/share/doc/$pkgname \
        --with-system-luarocks
    make all
}

check () {
    cd "${pkgname%-git}"
    make check
}

package () {
    cd "${pkgname%-git}"
    make install DESTDIR="$pkgdir"
    mv "$pkgdir/usr/share/licenses/"{sile,$pkgname}
}
