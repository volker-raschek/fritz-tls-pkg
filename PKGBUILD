# Maintainer: Markus Pesch <markus.pesch plus apps at cryptic.systems>

pkgname=fritz-tls
pkgver=0.20.0 # renovate: datasource=github-releases depName=tisba/fritz-tls
pkgrel=1
pkgdesc="Automate TLS certificate installation for AVM FRITZ!Box "
arch=('armv7h' 'aarch64' 'x86_64')
url="https://github.com/tisba/$pkgname"
license=('MIT')
makedepends=('go')

source=(
  "$url/archive/refs/tags/v$pkgver.zip"
)
sha512sums=('bebdf41a615102410ef13a94ec310a271d3c034078a1b0b59316d94d576c2a7cce45503a53eb6cf1f040483e145beb12dcb8a142f833e625eabdec1df0b810c8')
b2sums=('4da5de9d766bcf07bb920364310ae65c069fc51bba63e84ad94fb48cdb623e69ccc0355c26ab1b037db7edb32619ff5ae7d123011b4ae6d466c5406f3d5c7743')

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
