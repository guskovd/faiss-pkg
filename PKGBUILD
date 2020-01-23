pkgname=faiss
pkgdesc='A library for efficient similarity search and clustering of dense vectors.'
arch=('i686' 'x86_64')
url="https://github.com/facebookresearch/faiss"
license=('BSD')
pkgver=v1.6.1.r5.ge084949
pkgrel=1
source=('git+https://github.com/facebookresearch/faiss.git')
sha256sums=('SKIP')

pkgver() {
  cd "$pkgname"
  git describe --long | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}


build() {
  cd "${srcdir}/faiss"
  ./configure --without-cuda && make
  # make py
  cd c_api
  make
}

package() {
  cd "${srcdir}/faiss"
  make DESTDIR="$pkgdir/" includedir="usr/include/" libdir="usr/lib/" install
  # cd python
  # python setup.py install --root="$pkgdir/" --optimize=1 --skip-build
  cd c_api
  cp libfaiss_c.so $pkgdir/usr/lib
}
