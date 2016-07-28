# Maintainer: X0rg

_pkgbasename=memtest86
pkgname=$_pkgbasename-efi
pkgver=7.0
pkgrel=3
pkgdesc="A free, thorough, stand alone memory test as an EFI application"
arch=('i686' 'x86_64')
url="http://www.memtest86.com"
license=('GPL2' 'custom:PassMark')
makedepends=('libarchive')
optdepends=('efibootmgr: to add a new EFI boot entry'
	'grub: to add MemTest86 entry in GRUB2 menu')
backup=(etc/$pkgname/$pkgname.conf)
install=$pkgname.install
source=("http://www.memtest86.com/downloads/$_pkgbasename-iso.tar.gz"
	"memtest86-efi"
	"memtest86-efi.conf"
	"grub.conf"
	"systemd-boot.conf")
md5sums=('c709d3147295defc50e3f2b0e779a88e'
         '6d78d97e54e9feb75e3b1f835297ffd8'
         '6c096df3f55baf3e27c3bd605a418aa2'
         'f848ecf41edb2d95f469ff2251bcfa4a'
         '496120c33c2af986933bf33456fa6cf3')

prepare() {
	msg2 "Extract ISO..."
	bsdtar -xf "Memtest86-$pkgver.iso"
}

package() {
	msg2 "Move MemTest86 stuff in share directory..."
	[[ "$CARCH" == "i686" ]]   && install -Dvm755  "$srcdir/EFI/BOOT/BOOTIA32.EFI" "$pkgdir/usr/share/$pkgname/bootia32.efi"
	[[ "$CARCH" == "x86_64" ]] && install -Dvm755  "$srcdir/EFI/BOOT/BOOTX64.EFI"  "$pkgdir/usr/share/$pkgname/bootx64.efi"
	install -Dvm644 "$srcdir/EFI/BOOT/MT86.PNG"    "$pkgdir/usr/share/$pkgname/mt86.png"
	install -Dvm644 "$srcdir/EFI/BOOT/UNIFONT.BIN" "$pkgdir/usr/share/$pkgname/unifont.bin"
	install -Dvm644 "$srcdir/LICENSE.RTF"          "$pkgdir/usr/share/licenses/$pkgname/LICENSE.rtf"

	msg2 "Install AUR provided script..."
	install -Dvm755 "$srcdir/memtest86-efi"        "$pkgdir/usr/bin/memtest86-efi"
	install -Dvm644 "$srcdir/memtest86-efi.conf"   "$pkgdir/etc/memtest86-efi/memtest86-efi.conf"
	install -Dvm644 "$srcdir/grub.conf"            "$pkgdir/etc/memtest86-efi/grub.conf"
	install -Dvm644 "$srcdir/systemd-boot.conf"    "$pkgdir/etc/memtest86-efi/systemd-boot.conf"
}
