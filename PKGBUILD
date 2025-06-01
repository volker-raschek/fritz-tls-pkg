# Maintainer: Markus Pesch <markus.pesch plus apps at cryptic.systems>

pkgname=fritz-tls
pkgver=0.22.0 # renovate: datasource=github-releases depName=tisba/fritz-tls
pkgrel=1
pkgdesc="Automate TLS certificate installation for AVM FRITZ!Box "
arch=('armv7h' 'aarch64' 'x86_64')
url="https://github.com/tisba/$pkgname"
license=('MIT')
makedepends=('go')

source=(
  "$url/archive/refs/tags/v$pkgver.zip"
)
sha512sums=('6ac3065756933eb9bfbe44fccfb974fe8c454c2ce5fb822b87f8f536e3b99633d5a77aa28553faba8136603c94fb1700b2715fbb949f75a7a58b36bf04b803f2')
b2sums=('f18f009e74c31f4a6d2b5bd59ce49de61ab457d9c4ae5ce07c7937a18ac4df1e0f9e267cba609db5024ff013eab0cf98d5256e993242afb033be2f6efdf66bb8')

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
