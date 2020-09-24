# Maintainer: Guillaume DELVIT <guiguid@free.fr>

_pkgname=zram-init
pkgname=${_pkgname}-git
pkgver=10.5.r0.gb91acc4
pkgrel=1
pkgdesc="Setup zram-based tmpfs and swap devices on boot"
arch=('any')
url="http://en.wikipedia.org/wiki/ZRam"
license=('GPL')
depends=('bash')
#backup=("modprobe.d/zram.conf")
source=(
	"$pkgname::git+https://github.com/vaeth/zram-init.git#branch=master"
)
md5sums=('SKIP')

pkgver() {
	cd "${srcdir}/${pkgname}" || exit 2
	set -o pipefail
	git describe --tags --long | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
  cd "${srcdir}/${pkgname}"
  make
}

package() {
  cd "${srcdir}/${pkgname}"
  install -Dm755 sbin/zram-init $pkgdir/usr/bin/zram-init
  install -Dm644 modprobe.d/zram.conf $pkgdir/etc/modprobe.d/zram.conf
  install -Dm644 openrc/conf.d/zram-init $pkgdir/etc/conf.d/zram-init
  install -Dm755 openrc/init.d/zram-init $pkgdir/etc/init.d/zram-init
}
