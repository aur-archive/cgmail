# Contributor: Jaroslav Lichtblau <dragonlord@aur.archlinux.org>
# Contributor: Geoffroy Carrier <geoffroy.carrier@aur.archlinux.org>
# Contributor: Marco Ferragina <marco.ferragina@gmail.com>
# Maintainer: Lucas Salies Brum <lucas@archlinux.com.br>

pkgname=cgmail
pkgver=0.6.2
pkgrel=4
pkgdesc="An email checker and notifier applet for gmail"
arch=('any')
url="http://cgmail.tuxfamily.org/"
license=('GPL')
depends=('hicolor-icon-theme' 'dbus-python' 'python2-gconf' 'python2-libgnome' 'python2-gnomekeyring' 'gnome-keyring' 'python2-wnck' 'python2-feedparser' 'python2-notify' 'pyxdg')
makedepends=('setuptools' 'python2-distutils-extra' 'libcanberra')
install=$pkgname.install
source=(http://launchpad.net/$pkgname/0.6/$pkgver/+download/$pkgname-$pkgver.tar.gz
		cgmail.patch)
sha256sums=('eda5059d8e29ccd6d0967499c031bc86ddab74a26e11a6f9b90403214e01f2de'
            'e638b56c455ea6c55d5581bed3e735894bd4081fcb9ab640f64df47946134178')

build() {
  cd "$srcdir/$pkgname-$pkgver"
  patch -Np0 -i ../../cgmail.patch
  
  # python2 fix
  for file in $(find . -name '*.py' -print); do
    sed -i 's_^#!.*/usr/bin/python_#!/usr/bin/python2_' $file
    sed -i 's_^#!.*/usr/bin/env.*python_#!/usr/bin/env python2_' $file
  done
  sed -i 's_^#!.*/usr/bin/env.*python_#!/usr/bin/env python2_' waf

  ./waf configure --prefix=/usr
  ./waf build ${MAKEFLAGS}
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  ./waf install --destdir="${pkgdir}"

  #chmod 644 "$pkgdir"/usr/share/cGmail/cgmailservice.desktop
}
