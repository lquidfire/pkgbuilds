# Maintainer: James An <james@jamesan.ca>
# Contributor: Helge Willum Larsen <helgesdk@gmail.com>
# Contributor: Ng Oon-Ee <ngoonee.talk@gmail.com>
# Contributor: Byron Clark <byron@theclarkfamily.name> (auto-disper-git)
# Contributor: phillipberndt (maintainer of the current autorandr)
# Contributor: wertarbyte (original author of auto-disper and autorandr)

_pkgname=autorandr
pkgname=autorandr-git
pkgver=r210.582290b
pkgrel=1
pkgdesc='Auto-detect the connect display hardware and load the appropiate X11 setup using xrandr. Formerly autodisper. No disper support.'
arch=('any')
url="https://github.com/phillipberndt/autorandr"
license=('GPL3')
depends=('python' 'xorg-xrandr')
makedepends=('git')
optdepends=(
  'pm-utils: For changing autorandr profile on thaw/resume'
  'python2: For using autorandr_monitor'
  'xorg-xdpyinfo: For detecting the primary XRandR output'
)
provides=('autorandr')
conflicts=(
  'autorandr'
  'auto-disper-git'
  'autorandr-asch-git'
  'autorandr-phillipberndt-git'
)
install="$pkgname.install"
source=(
  "$_pkgname"::"git+https://github.com/phillipberndt/$_pkgname.git"
  "$pkgname.install"
  systemd-unit-dir.patch
)
md5sums=('SKIP'
         'bedb41a350cdf6983872119aef71fed6'
         '04ccd2e108878ee07fbb3282a3f7f75f')

pkgver() {
  cd "$_pkgname"
  (
    set -o pipefail
    git describe --long --tag | sed -r 's/([^-]*-g)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  ) 2>/dev/null
}

prepare() {
  cd "$_pkgname"
  patch -p1 -i ../systemd-unit-dir.patch
}

package() {
  cd "$_pkgname"
  make DESTDIR="$pkgdir" PREFIX=/usr install
}
