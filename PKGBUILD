# Contributor: Whitney Marshall <whitney.marshall@gmail.com>
# Maintainer: Matthew Phipps <mphipps1@umd.edu>

pkgname=icaclient-umd
pkgver=11.100.158406
pkgrel=1
pkgdesc="Citrix Receiver for Linux (ICAClient) for the University of MD VCL"
arch=('i686')
url="http://www.citrix.com/English/SS/downloads/details.asp?downloadId=2309164&productId=1689163"
license=('custom:Citrix')
depends=(
    'gstreamer0.10-base'
    'alsa-lib'
    'libvorbis'
    'libxmu'
    'libxp'
    'libxpm'
    'gtk2'
    'openmotif'
    )
conflicts=('citrix-client' 'citrix-client' 'icaclient')
install=$pkgname.install
source=(linuxx86-$pkgver.tar::'http://download.citrix.com.edgesuite.net/akdlm/5883/linuxx86-11.100.158406.tar.gz?__gda__=1331918957_0ddaae53bc87113f1908ae0efb031258&__dlmgda__=1332005057_4bbfc516360850f0cea93a1edc231caa&fileExt=.gz')
md5sums=('069bb3337791b0b55cbbf666c95403e5')

package() {
  ICAROOT=/opt/Citrix/ICAClient
  install --directory --owner=root --group=root --mode=555 \
    "$pkgdir$ICAROOT"{,/lib,/util,/keystore,/keystore/cacerts,/config/usertemplate,/keyboard,/help,/icons,/nls,/gtk,/gtk/glade,/nls/{en,de,ja}/{LC_MESSAGES,UTF-8}} 

  cd "$srcdir/linuxx86/linuxx86.cor"
  echo foo
  install --owner=root --group=root --mode=555 \
    wfica \
    wfcmgr \
    *.so \
    *.DLL \
    "$pkgdir$ICAROOT"
  echo bar
  install --owner=root --group=root --mode=555 \
    util/*.sh \
    util/*.so \
    util/echo_cmd \
    util/gst_{read,play}.32 \
    util/hinst \
    util/nslaunch \
    util/pacexec \
    util/pnabrowse \
    util/what \
    util/xcapture \
    "$pkgdir$ICAROOT/util"
  # The following 32-bit library causes false namcap errors
  # MGP: commenting this for now
  #rm util/libgstflatstm.32.so
  install --owner=root --group=root --mode=444 \
    util/pac.js \
    "$pkgdir$ICAROOT/util"
  install --owner=root --group=root --mode=444 \
    keystore/cacerts/*.crt \
    "$pkgdir$ICAROOT/keystore"
  install --owner=root --group=root --mode=444 \
    config/*.ini \
    "$pkgdir$ICAROOT/config"
  install --owner=root --group=root --mode=444 \
    config/usertemplate/*.ini \
    "$pkgdir$ICAROOT/config/usertemplate"
  install --owner=root --group=root --mode=444 \
    keyboard/*.ini keyboard/*.kbd \
    "$pkgdir$ICAROOT/keyboard"
  install --owner=root --group=root --mode=444 \
    icons/*.png icons/session.xpm \
    "$pkgdir$ICAROOT/icons"
  install --owner=root --group=root --mode=444 \
    gtk/resource.gtkrc \
    "$pkgdir$ICAROOT/gtk"
  install --owner=root --group=root --mode=444 \
    gtk/glade/*.glade \
    "$pkgdir$ICAROOT/gtk/glade"
  install --owner=root --group=root --mode=444 \
    lib/*.so \
    "$pkgdir$ICAROOT/lib"
  for locale in de en ja; do
     install --owner=root --group=root --mode=444 \
       nls/$locale/{*.{ini,txt,htm,ad,nls},Wfcmgr} \
       "$pkgdir$ICAROOT/nls/$locale"
     install --owner=root --group=root --mode=444 \
       nls/$locale/LC_MESSAGES/*.mo \
       "$pkgdir$ICAROOT/nls/$locale/LC_MESSAGES"
     install --owner=root --group=root --mode=444 \
       nls/$locale/UTF-8/{*.{txt,ad,nls},Wfcmgr} \
       "$pkgdir$ICAROOT/nls/$locale/UTF-8"
  done
  
  cd "$pkgdir$ICAROOT"
  ln -s en nls/C
  for locale in de en ja; do
    ln -s Npica.ad nls/$locale/Npica
    ln -s UTF-8 nls/$locale/utf8
    ln -s XCapture.ad nls/$locale/UTF-8/XCapture
    ln -s XCapture.ad nls/$locale/XCapture
  done

  cat > wfica.sh << EOF
#!/bin/sh
ICAROOT=$ICAROOT
export ICAROOT
\$ICAROOT/wfica -file \$1
EOF
  chmod 755 wfica.sh

  install --owner=root --group=root --mode=444 -D \
    nls/en/eula.txt \
    "$pkgdir/usr/share/licenses/$pkgname/eula.txt"
}

# vim:set ts=2 sw=2 et:
