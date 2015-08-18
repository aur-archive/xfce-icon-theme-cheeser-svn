# Maintainer: ssf <punx69 at gmx dot net>

pkgname=xfce-icon-theme-cheeser-svn
pkgver=r75
pkgrel=1
pkgdesc="An extended/remixed version of the default GNOME icon theme"
arch=("any")
url="https://github.com/chekavy/cheser-icon-theme"
license=("CCPL:cc-by-sa-3.0-US")
makedepends=('subversion' 'gtk-update-icon-cache' 'curl')
optdepends=('adwaita-icon-theme: for missing icons' 'gnome-icon-theme: for missing icons' 'gnome-icon-theme-extras: for missing icons' 'gnome-icon-theme-symbolic: for missing icons')
provides=("xfce-icon-theme-cheeser=${pkgver}")
_svntrunk=https://github.com/chekavy/cheser-icon-theme/trunk/Cheser
_svnmod=$pkgname
_copying=https://raw.githubusercontent.com/chekavy/cheser-icon-theme/master/COPYING

pkgver() {
	cd "$srcdir"/"$_svnmod"  >/dev/null 2>&1
	local ver="$(svnversion)"
	printf "r%s" "${ver//[[:alpha:]]}"
}

build() {
	cd "$srcdir"
	msg "Connecting to SVN server...."
	if [ -d "$_svnmod/.svn" ]; then
		(cd "$_svnmod" && svn up .)
	else
	svn co "$_svntrunk" --config-dir ./ "$_svnmod"
	fi
	msg "SVN checkout done or server timeout"
}

package() {
	cd "$srcdir"
	mkdir -p "$pkgdir/usr/share/icons"
	mv "$_svnmod" "$pkgdir/usr/share/icons/cheeser"
	gtk-update-icon-cache "$pkgdir/usr/share/icons/cheeser"
	rm -drf "$pkgdir/usr/share/icons/cheeser/.svn"
	mkdir -p "$pkgdir/usr/share/licenses/$pkgname"
	curl -L "$_copying" > "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
