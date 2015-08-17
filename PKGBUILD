# Maintainer: Ed Branch <brance carp at mail dot utexas dot edu nofish>
pkgname=ptpd2
pkgver=2.3.0
pkgrel=3
pkgdesc="An implementation of an IEEE 1588-2008 ordinary clock"
arch=('i686' 'x86_64')
url="http://ptpd.sourceforge.net"
license=('BSD')
depends=('libpcap')
backup=('etc/ptpd2.conf')
source=("http://sourceforge.net/projects/ptpd/files/ptpd/${pkgver}/ptpd-${pkgver}.tar.gz"
        "ptpd2.service")
sha1sums=('a3f6bb7768205b2904f78482fcac1e2b091c913c'
          'f78e0907e432fbc89a4f9e88b25f47b3cb8f576b')

build() {
    cd "${srcdir}/ptpd-${pkgver}"
    autoreconf -vi
    ./configure --prefix=/usr --sbindir=/usr/bin --enable-statistics --enable-ntpdc
    make
}

package() {
    # Systemd Unit File
    mkdir -p ${pkgdir}/usr/lib/systemd/system
    install ptpd2.service ${pkgdir}/usr/lib/systemd/system

    # Install ptpd2
    cd "${srcdir}/ptpd-${pkgver}"
    make DESTDIR="${pkgdir}/" install

    # Config File
    install -D src/ptpd2.conf.default-full ${pkgdir}/etc/ptpd2.conf

    # License
    mkdir -p ${pkgdir}/usr/share/licenses/${pkgname}
    install COPYRIGHT ${pkgdir}/usr/share/licenses/${pkgname}
}
