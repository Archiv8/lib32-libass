#!/bin/bash

# Created from the original package by

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# [Query]: Is package still being maintained.  Last release was 3.100, 2017-10-13.  Latest commit was 2021-06-19.
# [ToDo]: Add files: User documentation
# [ToDo]: Add files: Tooling
# [FixMe]: Namcap warnings and errors

# Maintainer: Ross Clark <https://github.com/Archiv8/lib32-lame/discussions>
# Contributor: Ross Clark <https://github.com/Archiv8/lib32-lame/discussions>

# Contributor: GordonGR <ntheo1979@gmail.com>
# Contributor: Johannes Dewender  arch at JonnyJD dot net
# Contributor: jospehgbr <rafael.f.f1@gmail.com>
# Maintainer: Adam <adam900710@gmail.com>

_relname=libass

pkgname=lib32-${_relname}
pkgver=0.15.2
pkgrel=1
pkgdesc="A portable library for SSA/ASS subtitles rendering (32 bit)"
arch=("x86_64")
url="https://github.com/libass/libass/"
license=("BSD")
depends=(
  "${_relname}"
  "lib32-freetype2"
  "lib32-fribidi"
  "lib32-fontconfig"
  "lib32-glib2"
  "lib32-glibc"
  "lib32-harfbuzz"
)
makedepends=(
  "git"
  "nasm"
)
provides=(
  "libass.so"
)
source=(
  "https://github.com/libass/libass/releases/download/${pkgver}/libass-${pkgver}.tar.xz"
)
sha512sums=(
  "4a352d2d21d8a7f25d593f0456cd057912589e55c0709dbf33150d23253fa7859da41584238f03c51782e066a0f92c6849c36b6210324cdb57ed01539921a39b"
)

build() {
  cd "${_relname}-${pkgver}"
  export PKG_CONFIG_PATH="/usr/lib32/pkgconfig"
  export CC="gcc -m32"

  ./configure \
    --prefix="/usr" \
    --libdir="/usr/lib32" \
    --host=i686-linux-gnu \
    --enable-harfbuzz \
    --enable-fontconfig

  make
}

package() {
  cd "${_relname}-${pkgver}"

  make DESTDIR="${pkgdir}" install

  install -Dm 644 COPYING -t "${pkgdir}"/usr/share/licenses/${pkgname}/
  
  rm -rf "${pkgdir}"/usr/include
}

# vim: ts=2 sw=2 et:
