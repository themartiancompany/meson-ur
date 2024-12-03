# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Jan Alexander Steffens (heftig) <heftig@archlinux.org>
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Anatol Pomozov <anatol dot pomozov at gmail>

_py="python"
_pkg=meson
pkgname="${_pkg}"
pkgver=1.6.0
pkgrel=3
pkgdesc="High productivity build system"
_ns="${_pkg}build"
url="https://${_ns}.com/"
arch=(
  any
)
license=(
  Apache-2.0
)
depends=(
  bash
  ninja
  "${_py}"
  "${_py}-tqdm"
)
makedepends=(
  "${_py}-build"
  "${_py}-installer"
  "${_py}-setuptools"
  "${_py}-wheel"
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
provides=(
  "${_py}-${_pkg}=${pkgver}"
)
conflicts=(
  "${_py}-${_pkg}"
)
_http="https://github.com"
_url="${_http}/${_ns}/${_pkg}"
source=(
  "${_url}/releases/download/${pkgver}/${_pkg}-${pkgver}.tar.gz"{,.asc}
  "${_pkg}-reference-${pkgver}.3::${_url}/releases/download/${pkgver}/${_pkg}-reference.3"
  "${_pkg}-reference-${pkgver}.json::${_url}/releases/download/${pkgver}/reference_manual.json"
  "arch-${_pkg}"
  cross-lib32
  native-clang
  0001-Skip-broken-tests.patch
  fix-cmake.diff
  fix-gir.diff
)
b2sums=(
  'c1d8f143b17fab90c6128a721ac45b9ed6b85d67272149058e74ab827822b6f2c84ebdc261290585e6af38ab5dca52ca013de9b7be70922c96260fc5ee708893'
  'SKIP'
  '18704b557298da2ea1f3edb4ed6c421bff3f973a215e56b340de2e78b1330e13eb00830cf44c3a8d04fd685ec6f8e6d078a4b9f03cf5b9e5413cbbfce55a22dd'
  '4d3bbf98706fd5c1e80da562ea2e737625db455e2eea30d1457a78862afa0b51456d5368abe19542cd524bd96d14d5cb33a22909d988be17e6ecb26929c49bb2'
  '70f042a7603d1139f6cef33aec028da087cacabe278fd47375e1b2315befbfde1c0501ad1ecc63d04d31b232a04f08c735d61ce59d7244521f3d270e417fb5af'
  '9b16477aa77a706492e26fb3ad42e90674b8f0dfe657dd3bd9ba044f921be12ceabeb0050a50a15caee4d999e1ec33ed857bd3bed9e4444d73bb4a4f06381081'
  '7d88929d5a3b49d91c5c9969f19d9b47f3151706526b889515acaeda0141257d5115875ac84832e9ea46f83a7700d673adcc5db84b331cd798c70ae6e90eac1e'
  'f23df4324b30b81f1756a9b443dd35185c4e8717b31fafcd2479071b6f38a8ee0776e97a3cd21a7921a6da892685a45632f6f8282007123b2dd5745492768f54'
  '8e75e4f6cac65cef19dade915528d05fedecf83586c482db17ebe1ed6399f1539fa74687fb7dad9747b8d2b2ca2fcfe89af049e19aedf489d34de93aec61dcbb'
  '8f00fa21777fe012b6e3cb880b0442ba9074d90ab8a2c7b7c67e8c69e418ef0625a047f372f68c43b775f95c36f9119d6997fd337f2296b036e89e306346abbd'
)
validpgpkeys=(
  # Jussi Pakkanen <jpakkane@gmail.com>
  19E2D6D9B46D8DAA6288F877C24E631BABB1FE70
)

prepare() {
  cd \
    "${_pkg}-${pkgver}"
  # Pass tests
  patch \
    -Np1 \
    -i \
    ../0001-Skip-broken-tests.patch
  # Unbreak CMake
  # https://github.com/mesonbuild/meson/issues/13888
  patch \
    -Np1 \
    -i \
    ../fix-cmake.diff
  # Unbreak GIR
  # https://github.com/mesonbuild/meson/issues/13850
  patch \
    -Np1 \
    -i \
    ../fix-gir.diff
}

build() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --no-isolation
}

check() (
  cd \
    "${_pkg}-${pkgver}"
  export \
    LC_CTYPE=en_US.UTF-8 \
    CPPFLAGS= \
    CFLAGS= \
    CXXFLAGS= \
    LDFLAGS=
  ./run_tests.py \
    --failfast
)

package() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  install \
    -d \
    "${pkgdir}/usr/share/vim/vimfiles"
  cp \
    -rt \
    "${pkgdir}/usr/share/vim/vimfiles" \
    "data/syntax-highlighting/vim/"*"/"
  install \
    -Dm644 \
    "data/shell-completions/bash/"* \
    -t \
    "${pkgdir}/usr/share/bash-completion/completions"
  install \
    -Dm644 \
    "data/shell-completions/zsh/"*  \
    -t \
    "${pkgdir}/usr/share/zsh/site-functions"
  install \
    -Dm644 \
    "../${_pkg}-reference-${pkgver}.3" \
    "${pkgdir}/usr/share/man/man3/${_pkg}-reference.3"
  install \
    -Dm644 \
    "../${_pkg}-reference-${pkgver}.json" \
    "${pkgdir}/usr/share/doc/${pkgname}/reference_manual.json"
  install \
    -D \
    "../arch-${_pkg}" \
    -t \
    "${pkgdir}/usr/bin"
  install \
    -Dm644 \
    "../cross-lib32" \
    "${pkgdir}/usr/share/${_pkg}/cross/lib32"
  install \
    -Dm644 \
    "../native-clang" \
    "${pkgdir}/usr/share/${_pkg}/native/clang"
}

# vim:set sw=2 sts=-1 et:
