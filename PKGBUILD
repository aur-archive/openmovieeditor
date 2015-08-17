# $Id: PKGBUILD 57798 2011-11-03 09:05:56Z spupykin $
# Contributor: Robert Emil Berge <filoktetes@linuxophic.org>
# Maintainer: Robert Emil Berge
# Maintainer: Mateusz Herych <heniekk@gmail.com>

pkgname=openmovieeditor
pkgver=0.0.20090105
pkgrel=8
pkgdesc="A simple video editor"
arch=('i686' 'x86_64')
url="http://openmovieeditor.sourceforge.net/HomePage"
license=('GPL')
depends=('libquicktime' 'libsamplerate' 'fltk' 'jack'
	 'portaudio' 'gmerlin-avdecoder' 'libxtst')
source=(http://downloads.sourceforge.net/$pkgname/$pkgname-$pkgver.tar.gz)
md5sums=('ce4f76c0b3e90aabf9c2d5c8dd31e9b1')

build() {
  cd $srcdir/$pkgname-$pkgver
  unset LDFLAGS

  export CFLAGS="$CFLAGS -fpermissive"
  export CXXFLAGS="$CXXFLAGS -fpermissive"
  export CPPFLAGS="$CPPFLAGS -fpermissive"
  sed -i 's|= sizes();|= (short*)sizes();|g' src/Fl_Split.cpp

  # Fix missing includes
  sed -e 's|<sstream>|<sstream>\n#include <stdint.h>|' -i src/VideoViewGL.H
  sed -e 's|<string>|<string>\n#include <stdint.h>|' -i src/WaveForm.H
  sed -e 's|<stdint.h>|<stdint.h>\n#include <stdio.h>|' -i src/AddCommand.H
  sed -e 's|<string>|<stdint.h>\n#include <stdio.h>|' -i src/MediaBrowser.H
  sed -e 's|<iostream>|<iostream>\n#include <stdio.h>|' -i src/fl_font_browser.h
  sed -e 's|<cstdio>|<cstdio>\n#include <unistd.h>|' -i src/DiskCache.cxx

  ./configure --prefix=/usr
  make
  make DESTDIR=$pkgdir install
}
