# Maintainer: Brian Knox <taotetek at gmail>

pkgname=hiredis-git
pkgver=20120401
pkgrel=1
pkgdesc="Minimalistic C client for Redis >= 1.2"
arch=('i686' 'x86_64')
url="http://github.com/antirez/hiredis/"
source=('hiredis.pc')
md5sums=('335e405802bd38c30610eaf49d56134d')
license=('BSD')
depends=('gcc-libs')
makedepends=('git make')
conflicts=('hiredis')
provides=('hiredis')
_gitroot="git://github.com/antirez/hiredis.git"
_gitname="hiredis"
unset CFLAGS

build() {
  cd "$srcdir"
  msg "Connecting to Git server...."

  if [ -d $_gitname ]; then
    pushd $_gitname && git pull origin && popd
    msg "The local files are updated"
  else
    git clone $_gitroot
  fi

  msg "Git checkout done or server timeout"
  msg "Starting make..."

  rm -rf $_gitname-build
  git clone $_gitname $_gitname-build
  cd $_gitname-build
}

package() {
  install -Dm644 hiredis.pc ${pkgdir}/usr/lib/pkgconfig/hiredis.pc
  cd "$srcdir/$_gitname-build"
  make PREFIX="$pkgdir/usr" install
  install -Dm644 COPYING "$pkgdir/usr/share/licenses/$_gitname/COPYING"
}
