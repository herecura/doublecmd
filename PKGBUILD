# vim:set ft=sh:
# Maintainer: BlackIkeEagle <ike DOT devolder AT gmail DOT com>
# Contributor: (sirocco AT ngs.ru)

pkgbase=doublecmd
pkgname=('doublecmd-gtk2' 'doublecmd-qt5')
pkgver=0.9.4
pkgrel=1
url="http://doublecmd.sourceforge.net/"
arch=('x86_64')
license=('GPL')
provides=("$pkgbase")
makedepends=('lazarus' 'qt5pas' 'gtk2')
optdepends=(
    'lua: scripting'
    'unzip: support extracting zip archives'
    'zip: suport packing zip archives'
    'p7zip: support for 7zip archives'
    'libunrar: support for rar archives'
)
source=(
    "https://downloads.sourceforge.net/project/$pkgbase/Double%20Commander%20Source/$pkgbase-$pkgver-src.tar.gz"
)
sha512sums=('c1cf9b35da6293f6047f95bb6fb105c2c4f881bc078fa599525ef29a1a714f278db2db67ba2f67f001a1d28238f6c8de8a841347f9996a466acf8678af559fb8')

prepare() {
    cp -a /usr/lib/lazarus ./

    cd "$pkgbase-$pkgver"
    sed -e 's/LIB_SUFFIX=.*/LIB_SUFFIX=/g' -i install/linux/install.sh
    sed -e "s@=\$(which lazbuild)@=\"\$(which lazbuild) --lazarusdir=$srcdir/lazarus\"@" -i build.sh

    cd "$srcdir"

    cp -a "$pkgbase-$pkgver" "$pkgbase-gtk"
    cp -a "$pkgbase-$pkgver" "$pkgbase-qt5"
}

build() {
    msg2 'build gtk'
    cd "$srcdir/$pkgbase-gtk"
    ./build.sh beta gtk2

    msg2 'build qt5'
    cd "$srcdir/$pkgbase-qt5"
    ./build.sh beta qt5
}

package_doublecmd-gtk2() {
    pkgdesc="twin-panel (commander-style) file manager (GTK2)"
    depends=('gtk2' 'desktop-file-utils' 'hicolor-icon-theme' 'shared-mime-info')
    conflicts=('doublecmd-qt5')
    cd "$srcdir/$pkgbase-gtk"
    ./install/linux/install.sh --install-prefix="$pkgdir"
}

package_doublecmd-qt5() {
    pkgdesc="twin-panel (commander-style) file manager (Qt5)"
    depends=('qt5pas' 'desktop-file-utils' 'hicolor-icon-theme' 'shared-mime-info')
    conflicts=('doublecmd-gtk2')
    replaces=('doublecmd-qt' 'doublecmd-qt4')
    cd "$srcdir/$pkgbase-qt5"
    ./install/linux/install.sh --install-prefix="$pkgdir"
}
