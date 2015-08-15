# Maintainer: Sarkasper <echo a2FzcGVyLm1lbnRlbkBnbXguY29tCg== | base64 -d>
# Contributor: Christian Himpel <chressie at gmail dot com>
# Contributor: Johannes Hanika  <hanatos at gmail dot com>
# Contributor: Kevin Brubeck Unhammer <unhammer at member dot fsf dot org>
# Contributor: orbisvicis <orbisvicis at gmail dot com>

pkgname=darktable-xtrans2-git
_gitname=darktable
pkgver=release.0.9.3.7910.gd8735a6
pkgrel=1
pkgdesc="A virtual lighttable and darkroom for photographers Xtrans2 for Fuji fork"
arch=('i686' 'x86_64')
url=http://www.darktable.org/
license=('GPL3')
depends=('exiv2>=0.18' 'intltool>=0.40' 'lcms2' 'lensfun>=0.2.3' 'libglade' 'dbus-glib'
	 'curl' 'libgnome-keyring' 'libgphoto2' 'libusb-compat' 'openexr' 'sqlite' 'libxslt'
	 'libsoup' 'gtk-engines')
makedepends=(git 'intltool>=0.40' 'cmake' 'librsvg')
optdepends=('librsvg' 'flickcurl: flickr upload -> install and rebuild')
conflicts=(darktable)
provides=(darktable)
install=darktable.install
options=(!emptydirs !libtool)
source=('git://github.com/dtorop/darktable.git')
md5sums=('SKIP')

pkgver() {
  cd $_gitname
  git describe --always | sed 's|-|.|g'
}

build() {
  local _gitdir=$srcdir/$_gitname
  cd $_gitdir
  git clean -dfx
  git reset --hard
  git checkout origin/xtrans2-dev
  [[ ! -d build ]] && mkdir -p build
  cd build
  cmake \
      -DCMAKE_INSTALL_PREFIX=/usr \
      -DCMAKE_BUILD_TYPE=Release \
      -DDONT_INSTALL_GCONF_SCHEMAS=True \
      -DBINARY_PACKAGE_BUILD=1 \
      -DUSE_GCONF_BACKEND=Off \
      -DBUILD_USERMANUAL=False \
      -DUSE_GNOME_KEYRING=Off \
      ..
  make
}

package() {
  cd $srcdir/$_gitname/build
  make DESTDIR=$pkgdir install
  mv "${pkgdir}/usr/share/doc/darktable" "${pkgdir}/usr/share/doc/${pkgname}-${pkgver}"
}
