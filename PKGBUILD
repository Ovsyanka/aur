# Maintainer: Richard Bradfield <bradfier@fstab.me>

pkgname=github-cli
pkgver=0.9.0
pkgrel=2
pkgdesc="The GitHub CLI"
arch=("x86_64")
url="https://github.com/cli/cli"
license=("MIT")
depends=("glibc")
makedepends=("go")
optdepends=("git: To interact with repositories")
source=("$pkgname-$pkgver.tar.gz::https://github.com/cli/cli/archive/v$pkgver.tar.gz")
sha256sums=('318295e5a662f785662751f1e2cd4b1f613ec3aced1c4e7f1755d27922dbfdbf')

build() {
    cd "cli-$pkgver"
    go build \
        -trimpath \
        -ldflags "-extldflags $LDFLAGS -X github.com/cli/cli/command.Version=v$pkgver -X github.com/cli/cli/command.BuildDate=$(date +%Y-%m-%d)" -o "bin/gh" ./cmd/gh

    # Generate manpage
    go run ./cmd/gen-docs --man-page --doc-path ./share/man/man1/

    # Build shell completion files
    mkdir ./_completions
    bin/gh completion -s bash > ./_completions/bash
    bin/gh completion -s zsh > ./_completions/zsh
    bin/gh completion -s fish > ./_completions/fish
}

package() {
    cd "cli-$pkgver"
    install -Dm755 "bin/gh" "$pkgdir/usr/bin/gh"
    install -Dm644 "LICENSE" "$pkgdir/usr/share/licenses/github-cli"
    install -Dm644 "README.md" "$pkgdir/usr/share/doc/github-cli/README.md"

    install -Dm644 "_completions/bash" "$pkgdir/usr/share/bash-completion/completions/gh"
    install -Dm644 "_completions/zsh" "$pkgdir/usr/share/zsh/site-functions/_gh"
    install -Dm644 "_completions/fish" "$pkgdir/usr/share/fish/vendor_completions.d/gh.fish"

    install -Dm644 -t "$pkgdir/usr/share/man/man1/" share/man/man1/*
}
