# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2022, 2023, 2024, 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>

# shellcheck disable=SC2034
_os="$( \
  uname \
    -o)"
_evmfs_available="$( \
  command \
    -v \
    "evmfs" || \
    true)"
if [[ ! -v "_evmfs" ]]; then
  if [[ "${_evmfs_available}" != "" ]]; then
    _evmfs="true"
  elif [[ "${_evmfs_available}" == "" ]]; then
    _evmfs="false"
  fi
fi
if [[ ! -v "_docs" ]]; then
  _docs="true"
fi
if [[ ! -v "_git" ]]; then
  _git="false"
fi
if [[ "${_os}" == "Android" ]]; then
  _emulator="retroarch"
elif [[ "${_os}" != "Android" ]]; then
  _emulator="duckstation"
fi
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
_platform="playstation"
_pkg=soundscope-player
pkgbase="${_pkg}"
pkgname=(
  "${_pkg}"
)
if [[ "${_docs}" == "true" ]]; then
  pkgname+=(
    "${_pkg}-docs"
  )
fi
pkgver=1.1.1
_commit="7e76c78da14ca3ad9a64f5e455c4208a3a112443"
_mkaudiocdrimg_pkgver="1.2.3"
pkgrel=1
_pkgdesc=(
  "SoundScope PlayStation media player."
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'any'
)
_http="https://github.com"
# _ns="tallero"
_ns="themartiancompany"
url="${_http}/${_ns}/${_pkg}"
license=(
  "AGPL3"
)
depends=(
  "${_emulator}"
  'ffmpeg'
  "mkaudiocdrimg>=${_mkaudiocdrimg_pkgver}"
  'shntool'
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
  "${_py}-appdirs"
  "${_py}-gobject"
  "psx-soundscope-bios"
)
makedepends=(
  "${_py}-setuptools"
)
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    "git"
  )
fi
if [[ "${_docs}" == "true" ]]; then
  makedepends+=(
    "make"
    "${_py}-docutils"
  )
fi
provides=(
  "${_py}-${_pkg}=${pkgver}"
)
conflicts=(
  "${_py}-${_pkg}"
)
if [[ "${_evmfs}" == "true" ]]; then
  _tag="${_commit}"
elif [[ "${_git}" == "true" ]]; then
  _tag="${pkgver}"
fi
_tarname="${_pkg}-${_tag}"
_sum="e1e7a1a150071250e6015d64d9c1740b3641da03279500aa4a6a7a04d0a48b87"
_sig_sum="049081f4cc049551ff82baeb798a8e93d646c675f7f29cd9817da6b6d5ff48ea"
# The kid
_evmfs_ns="0x926acb6aA4790ff678848A9F1C59E578B148C786"
# Dvorak
_evmfs_sig_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
_chain_id="100"
_fs="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_evmfs_dir="evmfs://${_chain_id}/${_fs}/${_evmfs_ns}"
_evmfs_sig_dir="evmfs://${_chain_id}/${_fs}/${_evmfs_sig_ns}"
_evmfs_uri="${_evmfs_dir}/${_sum}"
_evmfs_sig_uri="${_evmfs_sig_dir}/${_sig_sum}"
source=()
sha256sums=()
if [[ "${_evmfs}" == "true" ]]; then
  _src="${_tarname}.tar.gz::${_evmfs_uri}"
  _sig_src="${_tarname}.tar.gz.sig::${_evmfs_sig_uri}"
  source+=(
    "${_sig_src}"
  )
  sha256sums+=(
    "${_sig_sum}"
  )
elif [[ "${_git}" == "true" ]]; then
  _src="${_tarname}::git+${url}#tag=${pkgver}"
  _sum="SKIP"
fi
source+=(
  "${_src}"
)
sha256sums+=(
  "${_sum}"
)

package_soundscope-player() {
  provides=(
    "${_py}-${_pkg}=${pkgver}"
  )
  conflicts=(
    "${_py}-${_pkg}"
  )
  cd \
    "${_tarname}"
  "${_py}" \
    "setup.py" \
    install \
      --root="${pkgdir}" \
      --optimize=1
  install \
    -vDm644 \
    "COPYING" \
    "${pkgdir}/usr/share/licenses/${pkgname}"
}

package_soundscope-player-docs() {
  local \
    _make_opts=()
  provides=(
    "${_py}-${_pkg}-docs=${pkgver}"
  )
  conflicts=(
    "${_py}-${_pkg}-docs"
  )
  _make_opts=(
    PREFIX="/usr"
    DESTDIR="${pkgdir}"
  )
  cd \
    "${_tarname}"
  make \
    "${_make_opts[@]}" \
    install-doc
  make \
    "${_make_opts[@]}" \
    install-man
}
