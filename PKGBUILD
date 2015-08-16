# Maintainer: David Herrmann <dh.herrmann@googlemail.com>
pkgname=kmscon
pkgver=6
pkgrel=2
pkgdesc='Terminal emulator based on Kernel Mode Setting (KMS)'
arch=('i686' 'x86_64')
url="http://github.com/dvdhrm/$pkgname"
license=('MIT')
depends=('udev' 'systemd' 'libdrm' 'mesa' 'libgbm' 'libgles' 'pango' 'freetype2' 'fontconfig' 'libxkbcommon' 'libpciaccess' 'libegl' 'xkeyboard-config')
makedepends=('libxslt' 'docbook-xsl' 'linux-api-headers')
provides=('kmscon')
conflicts=('kmscon')
options=(!libtool !strip)
source=(https://github.com/downloads/dvdhrm/$pkgname/$pkgname-$pkgver.tar.bz2)
#source=($pkgname-$pkgver.tar.bz2)
md5sums=('12f6966cef8e846f31dbcad916a9f347')

build() {
  cd "$srcdir/$pkgname-$pkgver"
  ./configure \
    --prefix=/usr \
    --enable-kmscon \
    --disable-wlterm \
    --enable-debug \
    --enable-multi-seat \
    --enable-hotplug \
    --enable-pciaccess \
    --with-video=fbdev,dumb,drm \
    --with-fonts=pango,freetype2,8x16 \
    --with-sessions=dummy,terminal
  make
}

package() {
  cd "$srcdir/$pkgname-$pkgver"

  mkdir -p "$pkgdir/usr/share/licenses/$pkgname/"
  cp COPYING "$pkgdir/usr/share/licenses/$pkgname/"

  mkdir -p "$pkgdir/usr/lib/systemd/system/"
  install -Dm644 "docs/kmscon.service" "$pkgdir/usr/lib/systemd/system/kmscon.service"
  install -Dm644 "docs/kmscon@.service" "$pkgdir/usr/lib/systemd/system/kmscon@.service"

  make DESTDIR="$pkgdir/" install
}
