# Maintainer: Markus Pesch <markus.pesch plus apps at cryptic.systems>

pkgname=fritz-tls
pkgver=0.23.0 # renovate: datasource=github-releases depName=tisba/fritz-tls
pkgrel=1
pkgdesc="Automate TLS certificate installation for AVM FRITZ!Box "
arch=('armv7h' 'aarch64' 'x86_64')
url="https://github.com/tisba/$pkgname"
license=('MIT')
makedepends=('go')

source=(
  "$url/archive/refs/tags/v$pkgver.zip"
)
sha512sums=('29554553a580b63edd677772e1a2711c0d69ec8ebec3e2819199f5587416d7836ead494a763ef20b9b0e089f87378e213c2a44533ee2d5c3bd15eb814bd1ee7d')
b2sums=('443d25f73ecd09cc63535b271f4e13e48ae22d9863446404090ebc4902877f3f21bccbb3b94e1e38083eef0755e2ceed40a4046721d03eaa3df9eb30d2f79d9c')

build() {
  cd "$pkgname-$pkgver"

  # https://wiki.archlinux.org/title/Go_package_guidelines
  export CGO_CPPFLAGS="${CPPFLAGS}"
  export CGO_CFLAGS="${CFLAGS}"
  export CGO_CXXFLAGS="${CXXFLAGS}"
  export CGO_LDFLAGS="${LDFLAGS}"

  go build -v \
    -trimpath \
    -buildmode=pie \
    -mod=readonly \
    -modcacherw \
    -ldflags "-linkmode external -extldflags \"${LDFLAGS}\"" \
    -o $pkgname \
    .
}

package() {
  # binary
  install -D --mode 0755 --target-directory "$pkgdir/usr/bin" "$pkgname-$pkgver/$pkgname"

  # license
  install -D --mode 0755 --target-directory "$pkgdir/usr/share/licenses/$pkgname" "$pkgname-$pkgver/LICENSE"
}
