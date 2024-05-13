# Maintainer: Jerome Leclanche <jerome@leclan.ch>
# Previous contributors:
# William Gathoye, Emil Vanherp, Alad Wenter, Xavier D., Valere Monseur
# Troubleshooting: https://eid.belgium.be/en/faq/google-chromechromium-how-do-i-log
# Test if login works: https://iamapps.belgium.be/tma/

pkgname=eid-mw
pkgver=5.1.18
pkgrel=1
pkgdesc="The Belgian e-ID (electronic identity card) viewer and Firefox extension"
arch=("x86_64")
url="https://eid.belgium.be/"
license=("LGPL-3.0-only")
depends=("gtk3" "libproxy" "curl" "libbsd")
makedepends=("autoconf-archive" "pcsclite")
optdepends=(
    "firefox: Extension for Belgian eid"
    "acsccid: ACS CCID smart card readers"
    "ccid: Needed for Belgian Digipass 870"
    "pcsc-tools: PC/SC smartcard tools"
)
source=(
    "https://dist.eid.belgium.be/continuous/sources/$pkgname-$pkgver-v$pkgver.tar.gz"
    "https://dist.eid.belgium.be/continuous/sources/$pkgname-$pkgver-v$pkgver.tar.gz.asc"
)
sha256sums=('677ab121643a722b6b8c148433b6c9b5f5312d177296c6a1282117bb7abf54bd'
            'SKIP')
validpgpkeys=("D95426E309C0492990D8E8E2824A5E0010A04D46")

# Upstream has decided not signing sources using the GPG key as this was
# confusing users who are not used to use .asc signature files.  So while the
# binaries proposed on the following page
# https://eid.belgium.be/en/using_your_eid/installing_the_eid_software/linux
# are signed, the sources are not. It is asked to security-conscious users
# using the dist server instead.
#
# On Wed, Mar 29, 2017 at 11:08:34AM +0200, William Gathoye wrote:
# > On 03/29/2017 10:54 AM, Wouter Verhelst wrote:
# >> It is not meant for the security-conscious. If you want to be 100%
# >> certain, then https://dist.eid.belgium.be/continuous/sources/ is signed
# >> by a GPG key.
# >
# > Ok. I'm gonna switch to that channel again then (for Arch).
#
# Good, I was hoping you'd say that
#
# > But then why do you have specified on the eid.belgium.be page that the
# > binaries could be checked using the GPG key
# > B37D9040098C3DEEE00F6D08A35743EA6773D225 as we cannot check it as the
# > .asc file is not present.?
#
# The precompiled binaries in the repositories that can be found on
# files.eid.belgium.be (and for which the "eid-archive" packages on that page add
# configuration to supported distributions) *are* signed with that key. The
# sources aren't, for reasons as explained above.
#
# [...]

prepare() {
    # This should be removed after v5.1.18. Only to re-configure after xz-issues.
    cd "${pkgname}-${pkgver}-v${pkgver}"
    NOCONFIGURE=1 autoreconf -vfi
}

build() {
    cd "$pkgname-$pkgver-v$pkgver"
    sed -i "s/c_rehash/openssl rehash/g" plugins_tools/eid-viewer/Makefile.in
    SSL_PREFIX=/usr ./configure --prefix=/usr --libexecdir=/usr/bin --sysconfdir=/etc
    make
}

package() {
    cd "$pkgname-$pkgver-v$pkgver"
    make install DESTDIR="$pkgdir"
}
