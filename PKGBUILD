# Maintainer: Jan Alexander Steffens (heftig) <heftig@archlinux.org>
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Anatol Pomozov <anatol dot pomozov at gmail>

pkgname=meson
pkgver=1.5.0rc2
pkgrel=1
pkgdesc="High productivity build system"
url="https://mesonbuild.com/"
arch=(any)
license=(Apache-2.0)
depends=(
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
b2sums=('e3bd5cb22676b69576698faa955eaaa14af9b891efd6853180eb9824a9a75e102af1b1c7c3c9cfc27581605720536e569911697ea1248cb1328d72169f270fb1'
        'SKIP'
        '70e07aa724d6e46a1679178c7e34b05ec0cf825d0f163981f70e25f8e914a5746156e2c2169d68f0ad482a813f77bc6a2343009f84f0aa4746c0f47e65ae6dfe'
        'fadd73bbee04e203b9002e81e4c1476127aca1ce7fb4bc1b1665dfe891cdbc2e5b184d8d0979d2c724a452a1c6483d7eb758358ce5e96e8636362d0f3198df28'
        '70f042a7603d1139f6cef33aec028da087cacabe278fd47375e1b2315befbfde1c0501ad1ecc63d04d31b232a04f08c735d61ce59d7244521f3d270e417fb5af'
        '9b16477aa77a706492e26fb3ad42e90674b8f0dfe657dd3bd9ba044f921be12ceabeb0050a50a15caee4d999e1ec33ed857bd3bed9e4444d73bb4a4f06381081'
        '7d88929d5a3b49d91c5c9969f19d9b47f3151706526b889515acaeda0141257d5115875ac84832e9ea46f83a7700d673adcc5db84b331cd798c70ae6e90eac1e'
        'ee2b3a174c86affd7b5c26128eda7c51f8b223184eb4a67d957fb32a1396068e5b2613bfdb142134e4ceb8b64dd4464fad3a73e2b4087e0a87f9d0ccb83203d8')
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
