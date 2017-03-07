# Maintainer: Jan Alexander Steffens (heftig) <jan.steffens@gmail.com>
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Anatol Pomozov <anatol dot pomozov at gmail>

pkgname=meson
pkgver=0.39.0
pkgrel=1
pkgdesc='High productivity build system'
url='http://mesonbuild.com/'
arch=('any')
license=('Apache')
depends=('python' 'ninja')
makedepends=('python-setuptools')
checkdepends=('gcc-objc' 'vala' 'rust' 'gcc-fortran' 'mono' 'boost' 'qt5-base' 'git' 'gnustep-base'
              'cython' 'gtkmm3' 'gtest' 'gmock' 'protobuf' 'wxgtk' 'python-gobject' 'gobject-introspection'
              'itstool' 'gtk3')
source=(https://github.com/mesonbuild/meson/releases/download/${pkgver}/meson-${pkgver}.tar.gz{,.asc})
sha512sums=('d6282e3d6d8824dce58589dc0da7c957dfd0ea23c81cce7108f3d23b796f62fb9f976fd0963ec34bdaf645a906a10626e27e93bc6d732c60ab8a306a4e8337c0'
            'SKIP')
validpgpkeys=('95181F4EED14FDF4E41B518D3BF4693BFEEB9428') # Jussi Pakkanen <jpakkane@gmail.com>

check() {
  cd ${pkgname}-${pkgver}
  MESON_PRINT_TEST_OUTPUT=1 LC_CTYPE=en_US.UTF-8 ./run_tests.py
}

package() {
  cd ${pkgname}-${pkgver}
  python setup.py install --root="${pkgdir}" -O1
  install -Dm 644 syntax-highlighting/vim/ftdetect/meson.vim -t "${pkgdir}/usr/share/vim/vimfiles/ftdetect"
  install -Dm 644 syntax-highlighting/vim/indent/meson.vim -t "${pkgdir}/usr/share/vim/vimfiles/indent"
  install -Dm 644 syntax-highlighting/vim/syntax/meson.vim -t "${pkgdir}/usr/share/vim/vimfiles/syntax"
}

# vim: ts=2 sw=2 et:
