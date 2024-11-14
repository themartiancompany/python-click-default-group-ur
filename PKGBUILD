# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Truocolo <truocolo@aol.com>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_proj="click"
_pkg="${_proj}-default-group"
_pkgname="${_pkg}"
pkgname="${_py}-${_pkg}"
pkgver=1.2.4
pkgrel=1
_pkgdesc=(
  "Extends click.Group to invoke"
  "a command without explicit subcommand name"
)
pkgdesc="${_pkgdesc[*]}"
_http="https://github.com"
_ns="${_proj}-contrib"
url="${_http}/${_ns}/${_pkg}"
license=(
  'BSD'
)
arch=(
  'any'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
  "${_py}-${_proj}"
)
makedepends=(
  "${_py}-build"
  "${_py}-installer"
  "${_py}-flit-core"
)
checkdepends=(
  "${_py}-pytest"
)
source=(
  "${url}/archive/v${pkgver}/${pkgname}-${pkgver}.tar.gz"
)
sha512sums=(
  '0239e703421e693399e8e54e4a6bdc4a74e6f16307f008ee742788ce3e8040f633de2b1bf12997a5c448b70cb55f77ccd4f42c5b4abe3b6a05df18908daf61da'
)

build() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      build \
    -nw
}

check() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      pytest
}

package() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  install \
    -Dm644 \
    LICENSE \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}"
}

# vim:set sw=2 sts=-1 et:
