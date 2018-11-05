# Maintainer: Vladimir Borisov <vladimir@stremio.com>
_pkgname=stremio
pkgname=${_pkgname}-git
pkgver=4.4.10.r43.d4c0fa5
pkgrel=1
pkgdesc="The next generation media center"
arch=($(uname -m))
url="https://www.stremio.com"
license=("MIT")
groups=()
depends=("nodejs" "ffmpeg" "qt5-webengine" "qt5-webchannel" "qt5-declarative" "qt5-quickcontrols" "qt5-quickcontrols2" "qt5-translations" "mpv" "openssl")
makedepends=("git" "wget" "qt5-tools" "librsvg" "imagemagick")
provides=("${_pkgname}")
conflicts=("${_pkgname}")
replaces=()
backup=()
options=()

install=stremio.install

source=("${_pkgname}::git+https://github.com/Stremio/stremio-shell.git#branch=master")
noextract=()
md5sums=("SKIP")

# Please refer to the 'USING git SOURCES' section of the PKGBUILD man page for
# a description of each element in the source array.

pkgver() {
	cd "$srcdir/${_pkgname}"
# Git, tags available
	printf "%s" "$(git describe --long | sed 's/\([^-]*-\)g/r\1/;s/-/./g')"

# Git, no tags available
#	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
	cd "$srcdir/${_pkgname}"
	git submodule update --init
	make -f release.makefile clean
}

build() {
	cd "$srcdir/${_pkgname}"
	make -f release.makefile PREFIX="$pkgdir"
}

package() {
	cd "$srcdir/${_pkgname}"
	export PREFIX="$pkgdir";
	make -f release.makefile install
}
