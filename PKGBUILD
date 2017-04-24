# Maintainer: Felix Yan <felixonmars at gmail dot com>: original fbterm-patched
# Contributor: silenvx <czvziwzx at gmail dot com>: addon-fixes.patch
# Contributor: Nobuhiro Iwamatsu <iwamatsu at nigauri dot org>: gcc-6-build-fixes.patch
# Contributor: Arthur Shevchenko <dekross at outlook dot com>: infinality-fix.patch
# Contributor: Dalrik: miscoloring-fix.patch
# Contributor: Helle Vaanzinn <glitsj16 at riseup dot net>: revised fbterm-patched

_pkgname=fbterm
pkgname=fbterm-patched
pkgver=1.7
pkgrel=1
pkgdesc="Terminal emulator for linux with framebuffer device or VESA video card - patched"
arch=(x86_64)
url="https://github.com/izmntuk/fbterm"
license=(GPL2)
makedepends=(gpm)
depends=('fontconfig' 'gcc-libs')
optdepends=('gpm: for mouse support'
    'libx86: for VESA video card support')
conflicts=(fbterm-git)
provides=(fbterm)
install=fbterm.install
source=("${url}/archive/v${pkgver}.tar.gz"
    'addon-fixes.patch'
    'gcc-6-build-fixes.patch'
    'infinality-fix.patch'
    'insertmode-fix.patch'
    'miscoloring-fix.patch')
sha256sums=('68e9742b23d6f143d809a5930f5f22c7e55d7c14a4ab2c8a842e0b5c27b1f863'
    '1ad1dd1261bdc610d42ef53114fa7442d6481e973c09b61248f59c4c9a4df5fd'
    '8054410ab97da3df03406543c6a471acf3323b9e5712da6455d7c49cad7489ce'
    '549328db49421a3037c7afaf3773eacb531ff312cafe56a3efcc5df8b0d68310'
    '140d10f21bf401b56517367ea8c6a1915e48abd274887e29490b5fc7704d4dad'
    'a049e3d5ba29422783730980dd2b1f288506b60bc75cf99496423f09a2fc5ad6')
    
prepare() {
    cd "${srcdir}/${_pkgname}-${pkgver}"
    for patch in ../*.patch; do
        msg "Applying ${patch} ..."
        patch -Np1 -i $patch
    done
}

build() {
    cd "${srcdir}/${_pkgname}-${pkgver}"
    ./configure --prefix=/usr --enable-gpm
    CFLAGS=-Wno-fatal-errors CPPFLAGS=-Wno-fatal-errors make
}

package() {
    cd "${srcdir}/${_pkgname}-${pkgver}"
    install -Dm644 terminfo/fbterm "${pkgdir}/usr/share/terminfo/f/fbterm"
    install -Dm644 COPYING "${pkgdir}/usr/share/licenses/fbterm/LICENSE"
    make DESTDIR="${pkgdir}" TERMINFO="${pkgdir}/usr/share/terminfo" install
}
