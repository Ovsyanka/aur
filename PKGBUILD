# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Contributor: Ian MacKay <immackay0@gmail.com>
# Contributor: Mikel Pintado <mikelaitornube2010@gmail.com>
# Contributor: Jiawen Geng

pkgname=github-desktop
pkgver=2.9.0
gitname="release-$pkgver-linux2"
pkgrel=1
pkgdesc='GUI for managing Git and GitHub'
arch=('x86_64')
url='https://desktop.github.com'
license=('MIT')
depends=('curl' 'gconf' 'git' 'gnome-keyring' 'libsecret' 'libxss' 'nspr' 'nss' 'unzip')
optdepends=('github-cli: CLI interface for GitHub' 'hub: CLI interface for GitHub')
makedepends=('nodejs>=10.16.0' 'npm' 'python2' 'unzip' 'yarn' 'xorg-server-xvfb')
DLAGENTS=("http::/usr/bin/git clone --branch $gitname --single-branch %u")
source=("git+https://github.com/shiftkey/desktop.git#tag=$gitname"
        "$pkgname.desktop")
sha256sums=('SKIP'
            '932e4c456e8c6db03d27172cf0daa37806bf025bb560d8b3d758c0997d1a618c')

build() {
    cd desktop
    export DISPLAY=':99.0'
    Xvfb :99 -screen 0 1024x768x24 > /dev/null 2>&1 &
    yarn install
    yarn build:prod
}

package() {
    cd desktop
    install -d "$pkgdir/opt/$pkgname"
    cp -r --preserve=mode dist/github-desktop-linux-x64/* "$pkgdir/opt/$pkgname/"
    install -Dm644 "../$pkgname.desktop" "$pkgdir/usr/share/applications/$pkgname.desktop"
    install -Dm644 "app/static/logos/1024x1024.png" "$pkgdir/usr/share/icons/hicolor/1024x1024/apps/$pkgname.png"
    install -Dm644 "app/static/logos/512x512.png" "$pkgdir/usr/share/icons/hicolor/512x512/apps/$pkgname.png"
    install -Dm644 "app/static/logos/256x256.png" "$pkgdir/usr/share/icons/hicolor/256x256/apps/$pkgname.png"
    printf "#!/bin/sh\n\n/opt/$pkgname/github-desktop \"\$@\"\n" | install -Dm755 /dev/stdin "$pkgdir/usr/bin/$pkgname"
}
