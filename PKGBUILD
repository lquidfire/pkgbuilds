# Maintainer: Jonathan Steel <jsteel at archlinux.org>
# Contributor: Daniel J Griffiths <ghost1227@archlinux.us>
# Contributor: Stefan Clarke <fm0nk3y@yahoo.co.uk>

pkgname=gnubg
pkgver=1.06.002
pkgrel=2
pkgdesc="World class backgammon application"
arch=('x86_64')
url="http://www.gnubg.org"
license=('GPL3')
depends=('python2' 'gtkglext' 'curl')
source=($url/media/sources/$pkgname-release-$pkgver-sources.tar.gz
        $pkgname.desktop)
md5sums=('d3823526d5c503a961024d761adefd5e'
         '965f5c7c25f60b27d06cc6fef7befd30')

build() {
  cd $pkgname-$pkgver

  ./autogen.sh

  ./configure --prefix=/usr --bindir=/usr/bin --sysconfdir=/etc \
    --mandir=/usr/share/man --enable-simd=sse2

  make
}

package() {
  cd $pkgname-$pkgver

  make DESTDIR="$pkgdir" install

  install -Dm644 "$srcdir"/$pkgname.desktop \
    "$pkgdir"/usr/share/applications/$pkgname.desktop
}
