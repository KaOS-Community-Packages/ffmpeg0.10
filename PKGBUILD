pkgname=ffmpeg0.10
pkgver=0.10.16
pkgrel=1
pkgdesc='Complete solution to record, convert and stream audio and video'
arch=('x86_64')
url='http://ffmpeg.org/'
license=('GPL')
depends=('alsa-lib' 'bzip2' 'gsm' 'lame' 'libass' 'libmodplug' 'pulseaudio'
         'libtheora' 'libva' 'opencore-amr' 'openjpeg' 'rtmpdump'
         'schroedinger' 'sdl' 'speex' 'v4l-utils' 'xvidcore' 'zlib'
         'libvorbis' 'libvpx' 'x264')
makedepends=('libvdpau' 'yasm')
source=("http://ffmpeg.org/releases/ffmpeg-${pkgver}.tar.bz2"
        'ffmpeg-0.10-libvpx-1.5.patch')
md5sums=('b73d7b94b3bead6918ad5a3d47453c8b'
         '515b6129f2f943a6fa6ffc784bf98478')

prepare() {
  cd ffmpeg-${pkgver}
  patch -Np1 -i ../ffmpeg-0.10-libvpx-1.5.patch
}

build() {
  cd ffmpeg-${pkgver}
  export CFLAGS="$CFLAGS -I/usr/include/openjpeg-1.5"
  ./configure \
    --prefix='/usr' \
    --incdir='/usr/include/ffmpeg0.10' \
    --libdir='/usr/lib/ffmpeg0.10' \
    --shlibdir='/usr/lib/ffmpeg0.10' \
    --disable-debug \
    --disable-static \
    --enable-gpl \
    --enable-libass \
    --enable-libfreetype \
    --enable-libgsm \
    --enable-libmodplug \
    --enable-libmp3lame \
    --enable-libopencore_amrnb \
    --enable-libopencore_amrwb \
    --enable-libopenjpeg \
    --enable-libpulse \
    --enable-librtmp \
    --enable-libschroedinger \
    --enable-libspeex \
    --enable-libtheora \
    --enable-libv4l2 \
    --enable-libvorbis \
    --enable-libvpx \
    --enable-libx264 \
    --enable-libxvid \
    --enable-postproc \
    --enable-runtime-cpudetect \
    --enable-shared \
    --enable-vdpau \
    --enable-version3 \
    --enable-x11grab
  make
}

package() {
  cd ffmpeg-${pkgver}
  make DESTDIR="${pkgdir}" install
  rm -rf "${pkgdir}"/usr/{bin,share}
  install -dm 755 "${pkgdir}"/etc/ld.so.conf.d
  echo -e '/usr/lib/\n/usr/lib/ffmpeg0.10/' > "${pkgdir}"/etc/ld.so.conf.d/ffmpeg0.10.conf
}
