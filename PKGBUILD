# vim:set ft=sh:
# $Id$
# Maintainer: BlackIkeEagle <ike DOT devolder AT gmail DOT com>
# Contributor: (sirocco AT ngs.ru)

pkgbase=doublecmd
pkgname=('doublecmd-gtk2' 'doublecmd-qt4' 'doublecmd-qt5')
pkgver=0.8.0
_helpver=0.6.0
pkgrel=2
url="http://doublecmd.sourceforge.net/"
arch=('x86_64')
license=('GPL')
provides=("$pkgbase")
makedepends=('lazarus' 'qt4pas' 'qt5pas' 'gtk2')
optdepends=(
	'lua51: scripting'
	'p7zip: support for 7zip archives'
	'libunrar: support for rar archives'
)
source=(
	"http://downloads.sourceforge.net/project/$pkgbase/Double%20Commander%20Source/$pkgbase-$pkgver-src.tar.gz"
	"http://downloads.sourceforge.net/project/$pkgbase/Double%20Commander%20Source/$pkgbase-help-$_helpver-src.tar.gz"
)
sha512sums=('ef5f2202c74ca5963cfe748a2ae469cda7010a6506480c8504e43642fc4dbae076f301a673cbb40f37efb300640b63d6c09d24de91e0976912c5b867e32b99a1'
            '2fe7a58e317c93baf4cfcb9cfc660647d71f4454eef588a512a9b9e8467477a691ec1061f014a42dff4ae0a0ba0600824b33c12c950fe1e26fba2a51122404bb')

prepare() {
    cd "$pkgbase-$pkgver"
    sed -e 's/LIB_SUFFIX=.*/LIB_SUFFIX=/g' -i install/linux/install.sh
    sed -e 's/=$(which lazbuild)/="$(which lazbuild) --lazarusdir=\/usr\/lib\/lazarus"/' -i build.sh

    cd "$srcdir"

    cp -a "$pkgbase-$pkgver" "$pkgbase-gtk"
    cp -a "$pkgbase-$pkgver" "$pkgbase-qt4"
    cp -a "$pkgbase-$pkgver" "$pkgbase-qt5"
}

build() {
    msg2 'build gtk'
    cd "$srcdir/$pkgbase-gtk"
    ./build.sh beta gtk2

    msg2 'build qt4'
    cd "$srcdir/$pkgbase-qt4"
    ./build.sh beta qt

    msg2 'build qt5'
    cd "$srcdir/$pkgbase-qt5"
    ./build.sh beta qt5
}

package_doublecmd-gtk2() {
    pkgdesc="twin-panel (commander-style) file manager (GTK)"
    depends=('gtk2' 'desktop-file-utils' 'hicolor-icon-theme' 'shared-mime-info')
    conflicts=('doublecmd-qt4' 'doublecmd-qt5')
    cd "$srcdir/$pkgbase-gtk"
    ./install/linux/install.sh --install-prefix="$pkgdir"

    # install doc
    cd "$srcdir/$pkgbase-help-$_helpver"
    cp -a * "$pkgdir/usr/share/$pkgbase/doc/"
}

package_doublecmd-qt4() {
    pkgdesc="twin-panel (commander-style) file manager (Qt4)"
    depends=('qt4pas' 'desktop-file-utils' 'hicolor-icon-theme' 'shared-mime-info')
    conflicts=('doublecmd-gtk2' 'doublecmd-qt5')
    replaces=('doublecmd-qt')
    cd "$srcdir/$pkgbase-qt4"
    ./install/linux/install.sh --install-prefix="$pkgdir"

    # install doc
    cd "$srcdir/$pkgbase-help-$_helpver"
    cp -a * "$pkgdir/usr/share/$pkgbase/doc/"
}

package_doublecmd-qt5() {
    pkgdesc="twin-panel (commander-style) file manager (Qt5)"
    depends=('qt5pas' 'desktop-file-utils' 'hicolor-icon-theme' 'shared-mime-info')
    conflicts=('doublecmd-gtk2' 'doublecmd-qt4')
    cd "$srcdir/$pkgbase-qt5"
    ./install/linux/install.sh --install-prefix="$pkgdir"

    # install doc
    cd "$srcdir/$pkgbase-help-$_helpver"
    cp -a * "$pkgdir/usr/share/$pkgbase/doc/"
}
