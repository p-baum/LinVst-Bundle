# Maintainer: Kyle Bronsdon <kyle at silksow dot com>
# Contributor: Mads Kjeldgaard <mail@madskjeldgaard.dk>
pkgname=('linvst-bin' 'linvst3-bin' 'linvstmanager-git')
pkgver=4.9
linvstmanager_ver=1.1.1
pkgrel=1
pkgdesc="LinVst, LinVst3 and LinVstManager bundle"
arch=('x86_64')
url="https://github.com/osxmidi/LinVst"
license=('GPL')
groups=('pro-audio')
depends=('wine' 'gtk3')
makedepends=('make' 'cmake' 'git')
optdepends=('jack')
source=("$url/releases/download/$pkgver/LinVst-$pkgver.zip"
"https://github.com/osxmidi/LinVst3/releases/download/$pkgver/LinVst3-$pkgver.zip"
"https://github.com/Goli4thus/linvstmanager/archive/refs/tags/v$linvstmanager_ver.zip"
)
md5sums=('bcd078785ae233fe2ea26b5c2950b0ff'
         '1493a6e88b33d847cb653195b9d20c33'
         '36d9540486a95d92b23dd5d6e8ededa7')

package_linvst-bin() {
    pkgdesc="Linux Windows vst wrapper/bridge"
    conflicts=('linvst')

	# Shared library
	install -Dm755 "$srcdir/LinVst-$pkgver/linvst.so" "$pkgdir/usr/share/LinVst/linvst.so"

	# Embedded
	install -Dm755 "$srcdir/LinVst-$pkgver/lin-vst-server.exe" "$pkgdir/usr/bin/lin-vst-server.exe"
	install -Dm755 "$srcdir/LinVst-$pkgver/lin-vst-server.exe.so" "$pkgdir/usr/bin/lin-vst-server.exe.so"

	install -Dm755 "$srcdir/LinVst-$pkgver/lin-vst-server32.exe.so" "$pkgdir/usr/bin/lin-vst-server32.exe.so"
	install -Dm755 "$srcdir/LinVst-$pkgver/lin-vst-server32.exe" "$pkgdir/usr/bin/lin-vst-server32.exe"

	# Converter
	install -Dm755 "$srcdir/LinVst-$pkgver/linvstconvert" "$pkgdir/usr/bin/linvstconvert"
}

package_linvst3-bin() {
    pkgdesc="Linux Windows vst3 wrapper/bridge"

	# Shared library
	install -Dm755 "$srcdir/LinVst3-$pkgver/linvst3.so" "$pkgdir/usr/share/LinVst/linvst3.so"

	# Embedded
	install -Dm755 "$srcdir/LinVst3-$pkgver/lin-vst3-server.exe" "$pkgdir/usr/bin/lin-vst3-server.exe"
	install -Dm755 "$srcdir/LinVst3-$pkgver/lin-vst3-server.exe.so" "$pkgdir/usr/bin/lin-vst3-server.exe.so"

	# Converter
	install -Dm755 "$srcdir/LinVst3-$pkgver/linvst3convert" "$pkgdir/usr/bin/linvst3convert"

	#test
	install -Dm755 "$srcdir/LinVst3-$pkgver/TestVst3/testvst3.exe" "$pkgdir/usr/bin/testvst3.exe"
	install -Dm755 "$srcdir/LinVst3-$pkgver/TestVst3/testvst3.exe.so" "$pkgdir/usr/bin/testvst3.exe.so"
}

build() {
	cd "$srcdir/linvstmanager-$linvstmanager_ver"
    mkdir build && cd build
    cmake ..
    make -j4
}

package_linvstmanager-git() {
    pkgdesc="Graphical companion application for various bridges like LinVst, etc."

    cd "$srcdir/linvstmanager-$linvstmanager_ver/build"
    make DESTDIR=${pkgdir} install
    mv ${pkgdir}/usr/local/bin ${pkgdir}/usr/
    mv ${pkgdir}/usr/local/share ${pkgdir}/usr/
    rmdir ${pkgdir}/usr/local
}
