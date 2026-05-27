# Maintainer: Antonio Rojas <arojas@archlinux.org>
# Contributor: Allan McRae <allan@archlinux.org>

pkgname=libmpc
pkgver=1.4.1
_commit="b8c90939ef1dc32cfbaa1823fe9e676ad5515ef4"
pkgrel=1
pkgdesc='Library for the arithmetic of complex numbers with arbitrarily high precision'
arch=(x86_64)
url='http://www.multiprecision.org/'
license=(LGPL-3.0-only)
depends=(glibc
         gmp
         mpfr)
# Tallero
_evmfs_ns="0x6ec7cC56dCeC0a00CB15E97C64B1a5Ec7A31403c"
_bundle_sum="4c58b9172bdf60fad14f115a6d613c3adab1914fa7d461de6da870ab6d35b7fe"
_bundle_sum="a9c129ca1b913ca0bddfbe451abdff8723aa735c3a4d5240d64f15236bd7ba0b"
source=(https://ftp.gnu.org/gnu/mpc/mpc-${pkgver/_/-}.tar.xz{,.sig})
sha256sums=('91204cd32f164bd3b7c992d4a6a8ce6519511aadab30f78b6982d0bf8d73e931'
            'SKIP')
validpgpkeys=('AD17A21EF8AED8F1CC02DBD9F7D5C9BF765C61E3')  # Andreas Enge

build() {
  cd mpc-$pkgver
  ./configure \
    --prefix=/usr
  make
}

check() {
  cd mpc-$pkgver
  make check
}

package() {
  cd mpc-$pkgver
  make DESTDIR="$pkgdir" install
  mv "$pkgdir"/usr/share/info/{mpc,libmpc}.info
}
