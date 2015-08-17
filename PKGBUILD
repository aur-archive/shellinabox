# Contributor: Brian Moore <archlinux@cptl.org>
pkgname=shellinabox
pkgver=2.14
pkgrel=4
pkgdesc="A web-based ssh client."
arch=('i686' 'x86_64')
url="http://shellinabox.com/"
license=('GPL2')
optdepends=('openssh: SSL support')
makedepends=(openssh)
#install=shellinabox.install
backup=('etc/conf.d/shellinaboxd')
source=("http://shellinabox.googlecode.com/files/$pkgname-$pkgver.tar.gz" "shellinaboxd.rc.d" "shellinaboxd.conf.d" "shellinaboxd.service")
md5sums=('6c63b52edcebc56ee73a108e7211d174'
         'feea22575089cc7eb4925b1daff88b8c'
         '9850c1b59013c8ae535bb5d30ac2b87b'
	 'be649866d06ba497d88bb14f3e58f862')

prepare() {
	cd "$srcdir/$pkgname-$pkgver"
	sed -i "/ac_cpp=/s/\$CPPFLAGS/\$CPPFLAGS -O2/" configure
}

build() {
  cd "$srcdir/$pkgname-$pkgver"

  ./configure  --prefix=/usr

  make 
}
package() {
  cd "$srcdir/$pkgname-$pkgver"
  make DESTDIR=$pkgdir install || return 1

  install -Dm755 $srcdir/shellinaboxd.rc.d $pkgdir/etc/rc.d/shellinaboxd
  install -D -m644 $srcdir/shellinaboxd.service $pkgdir/usr/lib/systemd/system/shellinaboxd.service
  install -Dm644 $srcdir/shellinaboxd.conf.d $pkgdir/etc/conf.d/shellinaboxd
  install -dm700 -o nobody $pkgdir/var/lib/shellinabox
}
