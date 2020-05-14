pkgname='st-xresources-git'
_pkgname='st'
pkgver=r4.8a8358d
pkgrel=1

pkgdesc='Simple terminal with Xresources support'
url='https://github.com/null2264/st-xresources'
arch=('i686' 'x86_64')
license=('MIT')

depends=('libxft' 'libxext')
makedepends=('ncurses')

provides=($pkgname)
conflicts=(${_pkgname})

source=('git://github.com/null2264/st-xresources')

md5sums=('SKIP')

pkgver() {
  cd st-xresources
  printf 'r%s.%s' "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  cd st-xresources
  # skip terminfo which conflicts with ncurses
  sed -i '/\@tic /d' Makefile
}

build() {
  cd st-xresources
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd st-xresources
  make PREFIX=/usr DESTDIR="$pkgdir" TERMINFO="$pkgdir/usr/share/terminfo" install
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
}
