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

# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Truocolo <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
# Maintainer: Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Maintainer: Pellegrino Prevete (dvorak) <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>

# shellcheck disable=SC2034
_os="$( \
  uname \
    -o)"
if [[ ! -v "_git" ]]; the
  _git="true"
fi
if [[ "${_os}" == "Android" ]]; then
  _emulator="retroarch"
elif [[ "${_os}" == "Android" ]]; then
  _emulator="duckstation"
fi
_py="python"
_platform="playstation2"
_pkg=soundscope-player
pkgbase="${_pkg}"
pkgname=(
  "${_pkg}"
)
pkgver=1.1
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
provides=(
  "${_py}-${_pkg}=${pkgver}"
)
conflicts=(
  "${_py}-${_pkg}"
)
depends=(
  "${_emulator}"
  'ffmpeg'
  'mkaudiocdrimg'
  'shntool'
  "${_py}-appdirs"
  "${_py}-gobject"
)
if [[ "${_os}" == "GNU/Linux" ]]; then
  depends+=(
    "psx-bios"
  )
fi
makedepends=(
  'git'
  "${_py}-setuptools"
)
license=(
  "AGPL3"
)
if [[ "${_git}" == "true" ]]; then
  _src="${_pkg}::git+${url}#tag=${pkgver}"
  _sum="SKIP"
fi
source=(
  "${_src}"
)
sha256sums=(
  "${_sum}"
)

package_soundscope-player() {
  cd \
    "${_pkg}"
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
