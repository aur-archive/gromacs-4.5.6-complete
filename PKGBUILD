# Contributor: Hector <hsearaDOTatDOTgmailDOTcom>

pkgname=gromacs-4.5.6-complete
pkgver=4.5.6
pkgrel=1
pkgdesc='A versatile package to perform molecular dynamics. Last stable release of 4.5.x version series. Single and Double precision; Sources; Doxygen documentation'
url='http://www.gromacs.org/'
license=("GPL")
arch=('i686' 'x86_64')
depends=('fftw' 'lesstif' 'perl' 'libxml2' 'libsm' 'libx11' 'doxygen')
options=('!libtool')
makedepends=('cmake')
source=(ftp://ftp.gromacs.org/pub/gromacs/gromacs-$pkgver.tar.gz)
md5sums=('ad7405f8e04df5912ecf89d517ce86f6')
sha1sums=('76734a7fafc2a2a636c1a3e75b36e3c00fae304c')

build() {
  mkdir -p ${srcdir}/{single,double}

  msg2 "Building the single precision files"
  cd ${srcdir}/single
  cmake ../gromacs-$pkgver \
    -DCMAKE_PREFIX=/usr/local/gromacs/gromacs-$pkgver \
    -DCMAKE_INSTALL_PREFIX=/usr/local/gromacs/gromacs-$pkgver \
    -DGMX_SHARED_LIBS=ON
  make

  msg2 "Building the doulbe precision files"
  cd ${srcdir}/double
  cmake ../gromacs-$pkgver \
    -DCMAKE_PREFIX=/usr/local/gromacs/gromacs-$pkgver \
    -DCMAKE_INSTALL_PREFIX=/usr/local/gromacs/gromacs-$pkgver \
    -DGMX_SHARED_LIBS=ON \
    -DGMX_DOUBLE=ON
  make

  msg2 "Building doxygen documentation"
  cd ../gromacs-$pkgver
  ./configure
  doxygen
}

package() {
  msg2 "Making the single precision executables"
  cd ${srcdir}/single 
  make DESTDIR=${pkgdir} install

  msg2 "Making the double precision executables"
  cd ${srcdir}/double
  make DESTDIR=${pkgdir} install

  msg2 "Installing doxygen documentation"
  cd ${srcdir}/gromacs-$pkgver
  cp -R doxygen-doc $pkgdir/usr/local/gromacs/gromacs-$pkgver

  msg2 "Installing Sources"
  cd ${srcdir}/gromacs-$pkgver 
  cp -R src  $pkgdir/usr/local/gromacs/gromacs-$pkgver
}
