# Maintainer: alex-no1 <sanja dot msg at gmx dot de>
# Contributor: alex-no1 <sanja dot msg at gmx dot de>

pkgname=eclipse-indigo
_realname=eclipse
pkgver=3.7.2
_internal_pkgver=3.7.2
pkgrel=3
_date=201202080800
pkgdesc="An IDE for Java and other languages - Indigo"
arch=('i686' 'x86_64')
url="http://www.eclipse.org/"
license=('EPL')
depends=('desktop-file-utils' 'gtk2' 'unzip' 'libwebkit' 'libxtst' 'python2')
provides=(${_realname})
conflicts=(${_realname} 'xulrunner')
install=${pkgname}.install
source=("http://download.eclipse.org/eclipse/downloads/drops/R-${pkgver}-${_date}/${_realname}-SDK-${pkgver}-linux-gtk.tar.gz"
        "eclipse.desktop"
        "eclipse.ini.patch"
        "eclipse.sh")
md5sums=('79b90faa1ee6e7af1910c3a5077b594f'
         '3f394a30d0f20c1e07e12ff292c49d90'
         '18f0c725a424e6efbdc6363a8049bc76'
         '7ea99a30fbaf06ec29261541b8eb1e23')
[ "${CARCH}" = "x86_64" ] && source[0]="http://download.eclipse.org/eclipse/downloads/drops/R-${pkgver}-${_date}/${_realname}-SDK-${pkgver}-linux-gtk-${CARCH}.tar.gz"
[ "${CARCH}" = "x86_64" ] && md5sums[0]='6a0fd32cb6a986032a67defab3753476'

package() {
  cd "${srcdir}/eclipse"

  # patch to increase default memory limits
  patch -Np0 -i ${srcdir}/eclipse.ini.patch

  # python2 fix
  sed -i 's|#!/usr/bin/python|#!/usr/bin/python2|' \
    plugins/org.apache.ant_1.8.2.v20120109-1030/bin/runant.py

  # install eclipse
  install -d -m755 ${pkgdir}/usr/share/${_realname}
  cp -r * ${pkgdir}/usr/share/${_realname}/

  # install bin file
  install -d -m755 ${pkgdir}/usr/bin
  install -m755 ${srcdir}/${_realname}.sh ${pkgdir}/usr/bin/${_realname}

  # install icon and desktop files
  install -d -m755 ${pkgdir}/usr/share/{applications,pixmaps}
  install -m644 ${srcdir}/${_realname}.desktop ${pkgdir}/usr/share/applications/
  install -m644 plugins/org.eclipse.sdk_${_internal_pkgver}.v${_date}/${_realname}48.png \
    ${pkgdir}/usr/share/pixmaps/${_realname}.png
}
