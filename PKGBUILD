# Maintainer: Michael Lass <bevan@bi-co.net>
# Contributor: Viktor Drobot (aka dviktor) linux776 [at] gmail [dot] com

# This PKGBUILD is maintained on github:
# https://github.com/michaellass/AUR

pkgname=dream
pkgver=r126.ecc5c476
#_gitrev=402712863e63923a802e0d59d535f85ef0b6328a
pkgrel=1
pkgdesc="Software radio for AM and Digital Radio Mondiale (DRM)"
arch=(i686 x86_64)
url="https://sourceforge.net/projects/drm"
license=(GPL-2.0-only)
depends=(alsa-lib fftw glibc gpsd hamlib libfdk-aac libgcc libsndfile libstdc++ qt6-base qwt speexdsp zlib)
makedepends=(cmake qt6-webengine)
#source=("https://github.com/Drm-tools/$pkgname/archive/$_gitrev.zip")
source=("${pkgname}::git+https://github.com/Drm-tools/dream.git#branch=qt6")
sha256sums=('SKIP')

pkgver() {
    cd "$pkgname"
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  cd "${srcdir}/${pkgname}"
  #git switch qt6
  mkdir build
}

build() {
  cd "${srcdir}/${pkgname}"
  cmake -S . -B build -DUSE_QT=ON -DENABLE_SNDFILE=ON -DENABLE_SPEEXDSP=ON -DENABLE_ALSA=ON -DENABLE_QWT=ON -DENABLE_GPS=ON -DENABLE_FDK_AAC=ON -DENABLE_OPUS=ON -DENABLE_HAMLIB=ON -DCMAKE_BUILD_TYPE=Release -DQWT_LIB=/usr/lib/libqwt.so
  cmake --build build
}

package() {
  cd "${srcdir}/${pkgname}/build"
  make DESTDIR="${pkgdir}" install
}
