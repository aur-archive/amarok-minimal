# Maintainer: hbdee <hbdee.arch@gmail.com>

pkgname=amarok-minimal
pkgver=2.8.0
pkgrel=1
pkgdesc="The powerful music player for KDE without integrated web services, default scripts, iPod and media devices support."
arch=("i686" "x86_64")
url="http://amarok.kde.org/"
license=('GPL2' 'LGPL2.1' 'FDL')
depends=('kdebase-runtime' 'mariadb' 'qtscriptgenerator' 'taglib-extras' 'ffmpeg')
makedepends=('pkgconfig' 'automoc4' 'cmake') # Add 'libgpod', 'libmtp', 'loudmouth', 'libmygpo-qt', and/or 'clamz' if you require them.
optdepends=("libgpod: support for Apple iPod audio devices"
	    "libmtp: support for portable media devices"
	    "loudmouth: backend for Mp3tunes.com integration"
	    "openssl: Mp3tunes.com integration"
	    "ifuse: support for Apple iPod Touch and iPhone"
	    "libmygpo-qt: gpodder.net Internet Service"
	    "liblastfm: LastFM Internet Service"
	    "libofa: Open Fingerprint Architecture library for Musicbrainz and AmpliFIND"
	    "qjson: JSON parser for the Playdar Collection"
	    "clamz: support for downloading songs from Amazon.com"
	    "phonon-gstreamer: alternative backend supports Equalizer and Audio Analyzer Visualization Applet"
	    "kdemultimedia-audiocd-kio: Compact Disc(CD) support"
	    "taglib-1.9-or-higher: support of Opus files")
conflicts=('amarok' 'amarok-devel' 'amarok-git' 'amarok-minimal-git')
provides=('amarok')
install="amarok.install"
source=("http://download.kde.org/stable/amarok/${pkgver}/src/amarok-${pkgver}.tar.bz2")
sha1sums=('e76ccd53c05d57f9457d74cd08c2c41383c00937')

prepare() {
  
  # services
  sed -i '/amazon/d' amarok-${pkgver}/src/services/CMakeLists.txt
  sed -i '/magnatune/d' amarok-${pkgver}/src/services/CMakeLists.txt
  sed -i '/ampache/d' amarok-${pkgver}/src/services/CMakeLists.txt
  sed -i '/mp3tunes/d' amarok-${pkgver}/src/services/CMakeLists.txt
  sed -i '/jamendo/d' amarok-${pkgver}/src/services/CMakeLists.txt
  sed -i '/opmldirectory/d' amarok-${pkgver}/src/services/CMakeLists.txt
  sed -i '/LIBMYGPO_QT_FOUND/d' amarok-${pkgver}/src/services/CMakeLists.txt
  sed -i '/gpodder/d' amarok-${pkgver}/src/services/CMakeLists.txt
  sed -i '/LIBLASTFM_FOUND/d' amarok-${pkgver}/src/services/CMakeLists.txt
  sed -i '/lastfm/d' amarok-${pkgver}/src/services/CMakeLists.txt
  
  # scripts
  sed -i '/free_music_charts_service/d' amarok-${pkgver}/src/scripts/CMakeLists.txt
  sed -i '/librivox_service/d' amarok-${pkgver}/src/scripts/CMakeLists.txt
  sed -i '/radio_station_service/d' amarok-${pkgver}/src/scripts/CMakeLists.txt
  sed -i '/lyrics_lyricwiki/d' amarok-${pkgver}/src/scripts/CMakeLists.txt
  
  # utilities
  sed -i '/amzdownloader/d' amarok-${pkgver}/utilities/CMakeLists.txt

  if [[ -d build ]]
  then
    rm -rf build
  fi
   mkdir build
  
}

build() {

  cd build
  cmake ../amarok-${pkgver} \
    -DCMAKE_BUILD_TYPE=Release \
    -DQT_QMAKE_EXECUTABLE=qmake-qt4 \
    -DKDE4_BUILD_TESTS=OFF \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DWITH_LibLastFm=OFF \
    -DWITH_MP3Tunes=OFF \
    -DWITH_Mtp=OFF \
    -DWITH_IPOD=OFF \
    -DWITH_LibOFA=OFF \
    -DWITH_QJSON=OFF \
    -DWITH_Mygpo-qt=OFF \
    -DWITH_NepomukCore=OFF \
    -DWITH_Soprano=OFF \
    -DWITH_PLAYGROUND=OFF
  make
  
}

package(){

  cd build
  make DESTDIR="${pkgdir}" install
  
}
