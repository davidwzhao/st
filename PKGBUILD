# Maintainer: Jose Riha <jose1711 gmail com>
# Contributor: Patrick Jackson <PatrickSJackson gmail com>
# Contributor: Christoph Vigano <mail@cvigano.de>

pkgname=st
pkgver=0.8.2
pkgrel=2
pkgdesc='A simple virtual terminal emulator for X.'
arch=('i686' 'x86_64' 'armv7h')
license=('MIT')
depends=('libxft' 'libxext' 'xorg-fonts-misc')
makedepends=('ncurses')
url="http://st.suckless.org"
source=(http://dl.suckless.org/st/$pkgname-$pkgver.tar.gz
        config.h
        https://st.suckless.org/patches/xresources/st-xresources-20190105-3be4cf1.diff
        https://st.suckless.org/patches/boxdraw/st-boxdraw_v2-$pkgver.diff)
sha256sums=('aeb74e10aa11ed364e1bcc635a81a523119093e63befd2f231f8b0705b15bf35'
            'SKIP'
            '71c55b796beebecb5e268405f369122fa5a8cf22d992725f00c6c88fe5895f84'
            'c1b7ab7672815b73e8328ecc55300c12fddce9ecae4ab04ff4377bd9132089f6')
            # 'bed7977c855f02e3968a754e813015e4214b52102e3c54712d8a52245bcceeec')

prepare() {
  cd $srcdir/$pkgname-$pkgver
  # skip terminfo which conflicts with nsurses
  sed -i '/tic /d' Makefile
  cp $srcdir/config.h config.h
  patch < $srcdir/st-boxdraw_v2-$pkgver.diff
  patch < $srcdir/st-xresources-20190105-3be4cf1.diff
}

build() {
  cd $srcdir/$pkgname-$pkgver
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd $srcdir/$pkgname-$pkgver
  make PREFIX=/usr DESTDIR="$pkgdir" TERMINFO="$pkgdir/usr/share/terminfo" install
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
  # remove to avoid conflict with ncurses
  rm -f "${pkgdir}/usr/share/terminfo/s/st" "${pkgdir}/usr/share/terminfo/s/st-256color" 
}
