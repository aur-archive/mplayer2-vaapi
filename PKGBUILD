# Maintainer: ValdikSS <iam@valdikss.org.ru>

pkgname=mplayer2-vaapi
pkgver=20130414
pkgrel=2
pkgdesc='Advanced general-purpose media player. A fork of the original MPlayer project. With VA-API support.'
arch=('i686' 'x86_64')
license=('GPL')
url='https://github.com/koct9i/mplayer2'
install=$pkgname.install
depends=('a52dec' 'aalib' 'cdparanoia' 'desktop-file-utils' 'enca' 'faad2' 'ffmpeg'
         'fontconfig' 'freetype2' 'jack' 'ladspa' 'lame' 'libass' 'libbluray'
         'libcaca' 'libcdio-paranoia' 'libdca' 'libdvdcss' 'libdvdnav' 'libdvdread'
         'libgl' 'libjpeg' 'libmad' 'libpulse' 'libquvi' 'libtheora' 'libvdpau'
         'libxinerama' 'libxss' 'libxv' 'libxxf86dga' 'libxxf86vm' 'lirc-utils'
         'mpg123' 'ncurses' 'sdl' 'ttf-dejavu')
makedepends=('mesa' 'mesa-libgl' 'unzip' 'yasm' 'python' 'python-docutils' 'git')
backup=('etc/mplayer/codecs.conf' 'etc/mplayer/input.conf')
provides=('mplayer' 'mplayer2')
conflicts=('mplayer' 'mplayer2')
options=(!emptydirs)
source=(git://github.com/koct9i/mplayer2.git)
sha256sums=('SKIP')

prepare() {
  cd mplayer2
  sed 's/gmplayer/mplayer/g' -i etc/mplayer.desktop
  find -type f -exec sed -e 's/python3/python/' -i {} \;
}

build() {
  cd mplayer2

  ./configure --prefix=/usr --confdir=/etc/mplayer \
              --enable-translation --language=all \
              --enable-runtime-cpudetection \
              --enable-joystick \
              --disable-speex \
              --disable-openal \
              --disable-libdv \
              --disable-musepack \
              --disable-gif \
              --enable-vaapi
  make
}

package() {
  cd mplayer2
  make DESTDIR=$pkgdir install

  install -Dm644 etc/{codecs.conf,input.conf,example.conf} $pkgdir/etc/mplayer/
  install -dm755 $pkgdir/usr/share/mplayer/
  ln -s /usr/share/fonts/TTF/DejaVuSans.ttf $pkgdir/usr/share/mplayer/subfont.ttf

  install -dm755 $pkgdir/usr/share/applications/
  install -m 644 etc/mplayer.desktop $pkgdir/usr/share/applications/
}
