# Maintainer: Chris Morgan <me@chrismorgan.info>

pkgname=princexml
pkgver=10r2
pkgrel=1
pkgdesc="Convert HTML documents to PDF with CSS"
arch=(i686 x86_64)
url="http://www.princexml.com/"
depends=(fontconfig libidn libxml2)
license=(custom)
if test "$CARCH" = "i686"
then
	md5sums=('ca6c74d30d11d33e4bba2b6b65bd6479')
else
	md5sums=('64db57c92cf83e6a460a4c023de2632b')
fi
source=(http://www.princexml.com/download/prince-${pkgver}-linux-generic-${CARCH}.tar.gz)

package() {
	mkdir -p $pkgdir/opt/prince

	cd ${srcdir}/prince-${pkgver}-linux-generic-${CARCH}/lib/prince
	for file in `find -type f`; do
		if [ -x "$file" ]; then
			install -D "$file" "$pkgdir/opt/prince/$file"
		else
			install -D -m 644 "$file" "$pkgdir/opt/prince/$file"
		fi
	done

	mkdir -p $pkgdir/usr/bin
	echo "#!/bin/sh" > $pkgdir/usr/bin/prince
	echo 'exec /opt/prince/bin/prince --prefix=/opt/prince "$@"' >> $pkgdir/usr/bin/prince
	chmod +x $pkgdir/usr/bin/prince

	cd ../..
	install -D -m644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
