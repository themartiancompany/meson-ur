# Maintainer: Jan Alexander Steffens (heftig) <jan.steffens@gmail.com>
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Anatol Pomozov <anatol dot pomozov at gmail>

pkgname=meson
pkgver=0.47.0
pkgrel=1
pkgdesc='High productivity build system'
url='http://mesonbuild.com/'
arch=('any')
license=('Apache')
depends=('python' 'ninja')
makedepends=('python-setuptools')
checkdepends=('gcc-objc' 'vala' 'rust' 'gcc-fortran' 'mono' 'boost' 'qt4' 'qt5-base' 'git' 'cython'
              'gtkmm3' 'gtest' 'gmock' 'protobuf' 'wxgtk' 'python-gobject' 'gobject-introspection'
              'itstool' 'gtk3' 'java-environment=8' 'gtk-doc' 'llvm' 'clang' 'sdl2' 'graphviz'
              'doxygen' 'vulkan-validation-layers' 'openssh' 'mercurial' 'gtk-sharp-2' 'qt5-tools'
              'libwmf' 'dmd' 'valgrind')
source=(https://github.com/mesonbuild/meson/releases/download/${pkgver}/meson-${pkgver}.tar.gz{,.asc}
        arch-meson)
sha512sums=('844047ad184f60395c4b6dc61b8fb0f321722d19a8647b48cb3f05fda9ba57516bdcc2244d5bc9de74f2834d092235553faccde6172edaeb3c2d14ff633bc513'
            'SKIP'
            '4cdacd6a7d2bdaacde176fd7f90f8a06ae403db7e63498518c637b13bdc344dca595fb8b9f41f978f450cd43ffef8a4013c0e74f669d13ba6881d38068ea1c0d')
validpgpkeys=('95181F4EED14FDF4E41B518D3BF4693BFEEB9428') # Jussi Pakkanen <jpakkane@gmail.com>

prepare() {
  cd ${pkgname}-${pkgver}
}

build() {
  cd ${pkgname}-${pkgver}
  python setup.py build
}

check() (
  cd ${pkgname}-${pkgver}

  # set for debug output
  #export MESON_PRINT_TEST_OUTPUT=1

  export LC_CTYPE=en_US.UTF-8
  ./run_tests.py
)

package() {
  cd ${pkgname}-${pkgver}
  python setup.py install --root="${pkgdir}" --optimize=1 --skip-build

  install -d "${pkgdir}/usr/share/vim/vimfiles"
  cp -rt "${pkgdir}/usr/share/vim/vimfiles" data/syntax-highlighting/vim/*

  install -Dt "${pkgdir}/usr/share/emacs/site-lisp" -m644 data/syntax-highlighting/emacs/*
  install -Dt "${pkgdir}/usr/share/zsh/site-functions" -m644 data/shell-completions/zsh/*

  # Arch packaging helper
  install -D ../arch-meson -t "${pkgdir}/usr/bin"
}

# vim: ts=2 sw=2 et:
