pkgname=dmenu
pkgver=4.9
pkgrel=1
pkgdesc='dynamic menu for X.'
arch=('i686' 'x86_64')
license=('MIT')
depends=('libxft' 'libxinerama' 'sh' 'freetype2')
url="http://tools.suckless.org/dmenu"

_patches=(https://tools.suckless.org/dmenu/patches/fuzzymatch/dmenu-fuzzymatch-4.6.diff)

source=(https://dl.suckless.org/tools/dmenu-${pkgver}.tar.gz
        "config.h"
        "${_patches[@]}")

sha256sums=('b3971f4f354476a37b2afb498693649009b201550b0c7c88e866af8132b64945'
            '6cfa0e126b97a6fbece16bdb2dc84f2e065f243528d7cbab001d5f125f8520a7'
            '4cb6ca498921df1d92e55484dc7c280d66aeaa2bdd4f6335d1865450056a0f6a')

prepare() {
  cd $srcdir/$pkgname-$pkgver

  for patch in "${_patches[@]}"; do
    echo "Applying patch $(basename $patch)..."
    patch -Np1 -i "$srcdir/$(basename $patch)"
  done

  cp $srcdir/config.h config.h
}

build() {
  cd $srcdir/$pkgname-$pkgver
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 FREETYPEINC=/usr/include/freetype2
}

package() {
  cd $srcdir/$pkgname-$pkgver
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
}
