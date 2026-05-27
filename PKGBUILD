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
_evmfs_available="$(
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
if [[ ! -v "_ns" ]]; then
  if [[ "${_evmfs}" == "true" ]]; then
    _ns="themartiancompany"
  elif [[ "${_evmfs}" == "false" ]]; then
    _ns="gnu"
  fi
fi
if [[ ! -v "_git" ]]; then
  if [[ "${_ns}" == "gnu" ]]; then
    _git="false"
  elif [[ "${_ns}" == "themartiancompany" ]]; then
    _git="true"
  fi
fi
if [[ ! -v "_git_service" ]]; then
  if [[ "${_ns}" == "gnu" ]]; then
    _git_service="gnu"
  elif [[ "${_ns}" == "themartiancompany" ]]; then
    _git_service="github"
  fi
fi
if [[ ! -v "_tag_name" ]]; then
  if [[ "${_ns}" == "gnu" ]]; then
    _tag_name="pkgver"
  elif [[ "${_ns}" == "themartiancompany" ]]; then
    _tag_name="commit"
  fi
fi
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_ns}" == "gnu" ]]; then
    _archive_format="tar.xz"
  fi
fi
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_evmfs}" == "true" ]]; then
      _archive_format="bundle"
    elif [[ "${_evmfs}" == "false" ]]; then
      _archive_format="git"
    fi
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_ns}" == "gnu" ]]; then
      _archive_format="tar.xz"
    elif [[ "${_ns}" == "themartiancompany" ]]; then
      if [[ "${_git_service}" == "github" ]]; then
        _archive_format="zip"
      elif [[ "${_git_service}" == "gitlab" ]]; then
        _archive_format="tar.gz"
      fi
    fi
  fi
fi
_pkg=mpc
_pkg_alt=multiprecision
pkgname="lib${_pkg}"
pkgver=1.4.1
_commit="532a18ae8222f928c58f7ffd1b4f0122062172bd"
_bundle_commit="b8c90939ef1dc32cfbaa1823fe9e676ad5515ef4"
pkgrel=3
_pkgdesc=(
  'Library for the arithmetic of complex'
  'numbers with arbitrarily high precision.'
)
arch=(
  "aarch64"
  "arm"
  "armv7l"
  "armv8l"
  "i686"
  "mips"
  "powerpc"
  "pentium4"
  "x86_64"
)
url="http://www.${_pkg_alt}.org"
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
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    "git"
  )
fi
if [[ "${_evmfs}" == "true" ]]; then
  makedepends+=(
    "evmfs"
  )
fi
provides=(
  "${_pkg_alt}=${pkgver}"
)
conflicts=(
  "${_pkg_alt}"
)
# Tallero
_evmfs_ns="0x6ec7cC56dCeC0a00CB15E97C64B1a5Ec7A31403c"
_bundle_sum="4c58b9172bdf60fad14f115a6d613c3adab1914fa7d461de6da870ab6d35b7fe"
_bundle_sig_sum="a9c129ca1b913ca0bddfbe451abdff8723aa735c3a4d5240d64f15236bd7ba0b"
_gnu_sum='91204cd32f164bd3b7c992d4a6a8ce6519511aadab30f78b6982d0bf8d73e931'
_gnu_sig_sum_hinge="3752a19777570c8c23db295c0b36c447f013338815dc7aec9c38cb6403ddd5bd"
if [[ ! -v "_tag" ]]; then
  if [[ "${_git}" == "false" ]]; then
    if [[ "${_ns}" == "gnu" ]]; then
      if [[ "${_tag_name}" == "pkgver" ]]; then
        _tag="${pkgver/_/-}"
      fi
    fi
  elif [[ "${_git}" == "true" ]]; then
    _tag="${_commit}"
  fi
fi
_tarname="${_pkg}-${_tag}"
_tarfile="${_tarname}.${_archive_format}"
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_evmfs_dir="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}"
_evmfs_uri="${_evmfs_dir}/${_bundle_sum}"
_evmfs_src="${_tarfile}::${_evmfs_uri}"
_sig_uri="${_evmfs_dir}/${_bundle_sig_sum}"
_sig_src="${_tarfile}.sig::${_sig_uri}"
if [[ "${_evmfs}" == "true" ]]; then
  if [[ "${_git}" == "true" ]]; then
    _src="${_evmfs_src}"
    _sum="${_bundle_sum}"
    _sig_sum="${_bundle_sig_sum}"
    source+=(
      "${_sig_src}"
    )
    sha256sums+=(
      "${_bundle_sig_sum}"
    )
  fi
elif [[ "${_evmfs}" == "false" ]]; then
  if [[ "${_git}" == true ]]; then
    _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}?signed"
    _sum="SKIP"
  elif [[ "${_git}" == false ]]; then
    _uri=""
    if [[ "${_ns}" == "gnu" ]]; then
      _http="https://ftp.gnu.org"
      _url="${_http}/${_ns}/${_pkg}"
      _uri="${_url}/${_tarname}.tar.xz"
      _sum="${_gnu_sum}"
      _sig_src="${_tarfile}.sig::${_uri}.sig"
      _sig_sum="SKIP"
      source+=(
        "${_sig_src}"
      )
      sha256sums+=(
        "${_sig_sum}"
      )
    elif [[ "${_ns}" == "themartiancompany" ]]; then
      if [[ "${_git_service}" == "github" ]]; then
        if [[ "${_tag_name}" == "commit" ]]; then
          _uri="${_url}/archive/${_commit}.${_archive_format}"
          _sum="${_github_sum}"
        fi
      elif [[ "${_git_service}" == "gitlab" ]]; then
        if [[ "${_tag_name}" == "commit" ]]; then
          _uri="${_url}/-/archive/${_tag}/${_tag}.${_archive_format}"
        fi
      fi
    fi
    _src="${_tarfile}::${_uri}"
  fi
fi
if [[ "${_ns}" == "gnu" ]]; then
  _src="${_tarfile}::${_uri}"
  _sig_src="${_tarfile}.sig::${_uri}.sig"
  _sig_sum='SKIP'
  _src="${_tarfile}::${_uri}"
fi
source=(
  "${_src}"
  "${_sig_src}"
)
sha256sums=(
  "${_sum}"
  "${_sig_sum}"
)
if [[ "${_ns}" == "gnu" ]]; then
  validpgpkeys=(
    # Andreas Enge
    'AD17A21EF8AED8F1CC02DBD9F7D5C9BF765C61E3'
  )
elif [[ "${_ns}" == "themartiancompany" ]]; then
  validpgpkeys=(
    # Truocolo
    #   <truocolo@aol.com>
    '97E989E6CF1D2C7F7A41FF9F95684DBE23D6A3E9'
    #   <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
    'F690CBC17BD1F53557290AF51FC17D540D0ADEED'
    # Pellegrino Prevete (dvorak)
    #   <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
    '12D8E3D7888F741E89F86EE0FEC8567A644F1D16'
  )
fi


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
