# SPDX-License-Identifier: AGPL-3.0

#    -----------------------------------------------------
#    Copyright © 2024, 2025, 2026  Pellegrino Prevete
#
#    All rights reserved
#    -----------------------------------------------------
#
#    This program is free software: you can redistribute
#    it and/or modify it under the terms of the
#    GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of
#    the License, or (at your option) any later version.
#
#    This program is distributed in the hope that it
#    will be useful, but WITHOUT ANY WARRANTY;
#    without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
#    See the GNU Affero General Public License for
#    more details.
#
#    You should have received a copy of the
#    GNU Affero General Public License
#    along with this program.
#    If not, see <https://www.gnu.org/licenses/>.

# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Contributors:
#   Antonio Rojas
#     <arojas@archlinux.org>
#   Allan McRae
#     <allan@archlinux.org>

_os="$(
  uname \
    -o)"
if [[ "${_os}" == "Android" ]]; then
  _libc="ndk-sysroot"
  _compiler="clang"
  _libcompiler="llvm-libs"
elif [[ "${_os}" == "GNU/Linux" ]]; then
  _libc="glibc"
  _compiler="gcc"
  _libcompiler="libgcc"
elif [[ "${_os}" == "Msys" ]]; then
  _libc="msys2-w32api-runtime"
  _libc_headers="msys2-w32api-headers"
  _compiler="gcc"
  _libcompiler="gcc-libs"
else
  _msg=(
    "Unknown os '${_os}'."
  )
  msg \
    "${_msg[*]}"
  _libc="msys2-w32api-runtime"
  _libc_headers="msys2-w32api-headers"
  _compiler="gcc"
  _libcompiler="gcc-libs"
fi
if [[ ! -v "_ns" ]]; then
  _ns="themartiancompany"
  _ns="gnu"
fi
if [[ ! -v "_git" ]]; then
  if [[ ! -v "_git" ]]; then
    _git="false"
  fi
fi
if [[ ! -v "_tag_name" ]]; then
  if [[ "${_ns}" == "gnu" ]]; then
    _tag_name="pkgver"
  fi
fi
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_ns}" == "gnu" ]]; then
    _archive_format="tar.xz"
  fi
fi
_pkg=mpc
_pkg_alt=multiprecision
pkgname="lib${_pkg}"
pkgver=1.4.1
_commit="b8c90939ef1dc32cfbaa1823fe9e676ad5515ef4"
pkgrel=1
_pkgdesc=(
  'Library for the arithmetic of complex'
  'numbers with arbitrarily high precision.'
)
arch=(
  aarch64
  arm
  armv7l
  armv8l
  i686
  mips
  powerpc
  pentium4
  x86_64
)
url="http://www.multiprecision.org"
license=(
  "LGPL-3.0-only"
)
depends=(
  "${_libc}"
  "gmp"
  "mpfr"
)
makedepends=(
  "${_compiler}"
)
if [[ "${_os}" == "Msys" ]]; then
  makedepends+=(
    "${_libc_headers}"
    "windows-default-manifest"
  )
fi
provides=(
  "${_pkg_alt}=${pkgver}"
)
# Tallero
_evmfs_ns="0x6ec7cC56dCeC0a00CB15E97C64B1a5Ec7A31403c"
_bundle_sum="4c58b9172bdf60fad14f115a6d613c3adab1914fa7d461de6da870ab6d35b7fe"
_bundle_sum="a9c129ca1b913ca0bddfbe451abdff8723aa735c3a4d5240d64f15236bd7ba0b"
if [[ ! -v "_tag" ]]; then
  if [[ "${_git}" == "false" ]]; then
    if [[ "${_ns}" == "gnu" ]]; then
      if [[ "${_tag_name}" == "pkgver" ]]; then
        _tag="${pkgver/_/-}"
      fi
    fi
  fi
fi
_tarname="${_pkg}-${_tag}"
_tarfile="${_tarname}.${_archive_format}"
if [[ "${_git}" == "false" ]]; then
  if [[ "${_ns}" == "gnu" ]]; then
    _http="https://ftp.gnu.org"
    _url="${_http}/${_ns}/${_pkg}"
    _uri="${_url}/${_tarname}.tar.xz"
  fi
fi
if [[ "${_ns}" == "gnu" ]]; then
  _src="${_tarfile}::${_uri}"
  _src_sig="${_tarfile}.sig::${_uri}.sig"
  _sig_sum='SKIP'
fi
source=(
  "${_src}"
  "${_src_sig}"
)
sha256sums=(
  '91204cd32f164bd3b7c992d4a6a8ce6519511aadab30f78b6982d0bf8d73e931'
  'SKIP'
)
validpgpkeys=(
  # Andreas Enge
  'AD17A21EF8AED8F1CC02DBD9F7D5C9BF765C61E3'
)

prepare() {
  if [[ "${_git}" == "false" ]]; then
    if [[ "${_ns}" == "gnu" ]]; then
      if [[ "${_tag_name}" == "pkgver" ]]; then
        mv \
          "${_pkg}-${pkgver}" \
	  "${_tarname}"
      fi
    fi
  fi
}

build() {
  local \
    _configure_opts=()
  _configure_opts+=(
    --prefix="/usr"
  )
  cd \
    "${_tarname}"
  ./configure \
    "${_configure_opts[@]}"
  make
}

check() {
  cd \
    "${_tarname}"
  make \
    check
}

package() {
  local \
    _make_opts=()
  _make_opts+=(
    DESTDIR="${pkgdir}"
  )
  cd \
    "${_tarname}"
  make \
    "${_make_opts[@]}" \
    install
  mv \
    "${pkgdir}/usr/share/info/"{"${_pkg}","lib${_pkg}"}".info"
}
