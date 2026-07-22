# Maintainer: Markus Hartung <mail@hartmark.se>

pkgname=libfastjson
pkgver=1.2304.0
pkgrel=2
pkgdesc="A performance-focused json library for C"
arch=('x86_64' 'i686' 'aarch64' 'armv7h')
url="https://github.com/rsyslog/libfastjson"

# https://github.com/rsyslog/libfastjson?tab=License-1-ov-file
license=('LicenseRef-libfastjson')

source=($pkgname-$pkgver.tar.gz::https://github.com/rsyslog/$pkgname/archive/v$pkgver.tar.gz
        LICENSE
        fix-calloc-transposed-args.patch
        add-libm.patch)
sha256sums=('6c18848c75b179108429fc2818273551c68ffe6ddd5e414c20c071c844befbc1'
            'a5adc22a41565fc64da88d84fce7ae16ef21657d07ae3bb2d7292c79d6adf782'
            'db59ae9d860dab8182d297d846aa731c1a99a1c5d0f9112132de6e5f01aeff6d'
            '962d6ebd7ef2eefe14621af36cc32c282519704a9d7146c3b1297079adbe9e9a')

depends=(glibc)

prepare() {
  cd "${pkgname}-$pkgver"
  patch -p1 -i ../fix-calloc-transposed-args.patch
  patch -p1 -i ../add-libm.patch
}

build() {
  cd "${pkgname}-$pkgver"
  autoreconf -fvi
  ./configure --prefix=/usr
  make
}

package() {
  cd "${pkgname}-$pkgver"
  make DESTDIR="$pkgdir/" install
  install -Dm644 \
    "${srcdir}/LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"

}
