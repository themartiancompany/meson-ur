# Maintainer: Jan Alexander Steffens (heftig) <heftig@archlinux.org>
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Anatol Pomozov <anatol dot pomozov at gmail>

pkgname=meson
pkgver=1.6.0rc2
pkgrel=1
pkgdesc="High productivity build system"
url="https://mesonbuild.com/"
arch=(any)
license=(Apache-2.0)
depends=(
  bash
  ninja
  python
  python-tqdm
)
makedepends=(
  python-build
  python-installer
  python-setuptools
  python-wheel
)
checkdepends=(
  boost
  clang
  cmake
  cuda
  cython
  doxygen
  gcc-fortran
  gcc-objc
  git
  glib2-devel
  glibc-locales
  gmock
  gnustep-base
  gobject-introspection
  graphviz
  gtest
  gtk-doc
  gtk-sharp-2
  gtk3
  gtkmm3
  hotdoc
  itstool
  java-environment=8
  ldc
  libelf
  libwmf
  llvm
  mercurial
  mono
  nasm
  netcdf-fortran
  openmpi
  openssh
  protobuf
  python-gobject
  python-pytest-xdist
  qt5-base
  qt5-tools
  rust
  rust-bindgen
  sdl2
  vala
  valgrind
  vulkan-validation-layers
  wayland-protocols
  wxgtk3
)
source=(
  https://github.com/mesonbuild/meson/releases/download/$pkgver/meson-$pkgver.tar.gz{,.asc}
  meson-reference-$pkgver.3::https://github.com/mesonbuild/meson/releases/download/$pkgver/meson-reference.3
  meson-reference-$pkgver.json::https://github.com/mesonbuild/meson/releases/download/$pkgver/reference_manual.json
  arch-meson
  cross-lib32
  native-clang
  0001-Skip-broken-tests.patch
)
b2sums=('696719ed4e713ba2b927a169eb8946d485d4e5190ded5c6918e760100dc744b7abe863f1f51086851da15feb9ce936b543be5001088e6235d72293c7be55ef14'
        'SKIP'
        'af9e1e7b2737ef70f22c4676cd53b6a9d0d05cac7ccbb321f0511cb4e43f183212a9e2cc53a98ade71bb265c17f80a0464886cee1a6f92d68e8245f1f2e5f232'
        '1c12f10fa55789fe6a1532b8af02d31edf0237520943a617772bea71db9249c94e980fd982e99c4e8c3f6391d3fce79f5999883689347849fc204ae19e5585cf'
        '70f042a7603d1139f6cef33aec028da087cacabe278fd47375e1b2315befbfde1c0501ad1ecc63d04d31b232a04f08c735d61ce59d7244521f3d270e417fb5af'
        '9b16477aa77a706492e26fb3ad42e90674b8f0dfe657dd3bd9ba044f921be12ceabeb0050a50a15caee4d999e1ec33ed857bd3bed9e4444d73bb4a4f06381081'
        '7d88929d5a3b49d91c5c9969f19d9b47f3151706526b889515acaeda0141257d5115875ac84832e9ea46f83a7700d673adcc5db84b331cd798c70ae6e90eac1e'
        '1394951260a964ebdfb5655821f2c63a10ac4ae8b8b3f12c8214430561f1991f939d0fe9fba8612cef2d427940fa3b124fbbfda0f621f39323f0df904c1a1922')
validpgpkeys=(
  19E2D6D9B46D8DAA6288F877C24E631BABB1FE70  # Jussi Pakkanen <jpakkane@gmail.com>
)

prepare() {
  cd $pkgname-$pkgver

  # Pass tests
  patch -Np1 -i ../0001-Skip-broken-tests.patch
}

build() {
  cd $pkgname-$pkgver
  python -m build --wheel --no-isolation
}

check() (
  cd $pkgname-$pkgver
  export LC_CTYPE=en_US.UTF-8 CPPFLAGS= CFLAGS= CXXFLAGS= LDFLAGS=
  ./run_tests.py --failfast
)

package() {
  cd $pkgname-$pkgver
  python -m installer --destdir="$pkgdir" dist/*.whl

  install -d "$pkgdir/usr/share/vim/vimfiles"
  cp -rt "$pkgdir/usr/share/vim/vimfiles" data/syntax-highlighting/vim/*/

  install -Dm644 data/shell-completions/bash/* -t "$pkgdir/usr/share/bash-completion/completions"
  install -Dm644 data/shell-completions/zsh/*  -t "$pkgdir/usr/share/zsh/site-functions"

  install -Dm644 ../meson-reference-$pkgver.3    "$pkgdir/usr/share/man/man3/meson-reference.3"
  install -Dm644 ../meson-reference-$pkgver.json "$pkgdir/usr/share/doc/$pkgname/reference_manual.json"

  install -D ../arch-meson -t "$pkgdir/usr/bin"

  install -Dm644 ../cross-lib32 "$pkgdir/usr/share/meson/cross/lib32"
  install -Dm644 ../native-clang "$pkgdir/usr/share/meson/native/clang"
}

# vim:set sw=2 sts=-1 et:
