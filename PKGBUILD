#Maintainer: Nicola Bignami <nicola@kernel-panic.no-ip.net>
#Contributor: Muhammed Uluyol <uluyol0@gmail.com>

pkgname=foo2zjs-testing
pkgver=20150211
pkgrel=1
pkgdesc="foo2zjs Printer Drivers. Includes also foo2hp, foo2hbpl, foo2oak, foo2xqx, foo2qpdl, foo2slx, foo2hiperc and foo2lava drivers."
url="http://foo2zjs.rkkda.com/"
license=('GPL' 'custom')
depends=('psutils' 'cups' 'foomatic-db-engine' 'foomatic-db')
conflicts=('foo2zjs' 'foomatic-db-foo2zjs')
makedepends=('unzip' 'bc' 'wget')
optdepends=('tix: required by hplj10xx_gui.tcl')
arch=('i686' 'x86_64')
options=('!emptydirs' '!ccache')
install='foo2zjs-testing.install'
source=("foo2zjs-${pkgver}.tar.gz::http://foo2zjs.rkkda.com/foo2zjs.tar.gz"
        'destdir-support-20140329-1.patch'
	'gen-fixes-20140329-1.patch'
	'firmware-loader-20130602-1.patch'
	'udev-firmware-loading-ruleset-20130601-1.patch')
md5sums=('1d468fd3513a32eb66bcf2c08f5f457c'
         '26ed4b81ba769a620a249b7395dc7057'
	 'c080b84ca44714eff986e3cf4f8d4bae'
	 'edfa38b48ae6429b957190d2c05a971b'
	 'ab84c888e05378c4618e764fe946d17a')
build() {
  cd "${srcdir}/foo2zjs"
  patch -p1 -i ${srcdir}/${source[1]} 
  patch -p1 -i ${srcdir}/${source[2]} 
  patch -p1 -i ${srcdir}/${source[3]}
  patch -p1 -i ${srcdir}/${source[4]}  
  make
}

package() {
  cd "${srcdir}/foo2zjs"
  for model in $(grep 'getone ' getweb.in | \
                 cut -d'#' -f1 | awk '{ print $2; }'); do
    if [[ $model != '$i' ]]; then
      ./getweb $model || true
    fi
  done

  install -d ${pkgdir}/usr/share/{applications,pixmaps,cups/model}
  install -d ${pkgdir}/usr/share/foomatic/db/source/{driver,opt,printer}

  make DESTDIR=${pkgdir} install install-hotplug-prog

  install -m755 getweb ${pkgdir}/usr/bin
  install -D -m644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"

# files already provided by foomatic-db

  rm ${pkgdir}/usr/share/foomatic/db/source/driver/foo2hiperc.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/driver/foo2hp.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/driver/foo2lava.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/driver/foo2oak-z1.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/driver/foo2oak.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/driver/foo2qpdl.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/driver/foo2slx.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/driver/foo2xqx.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/driver/foo2zjs.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/driver/foo2hbpl2.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/driver/foo2zjs-z1.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/driver/foo2zjs-z2.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/driver/foo2zjs-z3.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_1000.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_1005.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_1018.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_1020.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_1022.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_M1005_MFP.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_1022n.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_1022nw.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_P1005.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_P1006.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_P1007.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_P1008.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-Color_LaserJet_1500.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-Color_LaserJet_1600.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-Color_LaserJet_2600n.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-Color_LaserJet_CP1215.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_M1120_MFP.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_M1319_MFP.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_P1505.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_P1505n.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_P2014.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_P2014n.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_P2035.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_P2035n.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_Pro_CP1025nw.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_Pro_P1102.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_Pro_P1102w.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_Pro_P1566.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/HP-LaserJet_Pro_P1606dn.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Minolta-magicolor_2200_DL.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Minolta-magicolor_2300_DL.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Minolta-magicolor_2430_DL.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/KONICA_MINOLTA-magicolor_2430_DL.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/KONICA_MINOLTA-magicolor_2480_MF.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/KONICA_MINOLTA-magicolor_2490_MF.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/KONICA_MINOLTA-magicolor_2530_DL.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/KONICA_MINOLTA-magicolor_1680MF.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/KONICA_MINOLTA-magicolor_1690MF.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/KONICA_MINOLTA-magicolor_4690MF.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/KONICA_MINOLTA-magicolor_1600W.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Kyocera-KM-1635.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Kyocera-KM-2035.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Xerox-Phaser_6110.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Xerox-Phaser_6115MFP.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Xerox-Phaser_6121MFP.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Xerox-WorkCentre_6015.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Fuji_Xerox-DocuPrint_CM205.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Samsung-CLP-300.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Samsung-CLP-310.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Samsung-CLP-315.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Samsung-CLP-325.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Samsung-CLP-365.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Samsung-CLP-600.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Samsung-CLP-610.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Samsung-CLP-620.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Samsung-CLX-2160.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Samsung-CLX-3160.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Samsung-CLX-3175.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Samsung-CLX-3185.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Generic-OAKT_Printer.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Generic-ZjStream_Printer.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Lexmark-C500.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Minolta-Color_PageWorks_Pro_L.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Oki-C110.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Oki-C301dn.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Oki-C310dn.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Oki-C3100.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Oki-C3200.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Oki-C3300.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Oki-C3400.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Oki-C3530_MFP.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Oki-C5100.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Oki-C5200.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Oki-C5500.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Oki-C5600.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Oki-C5650.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Oki-C5800.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Dell-1355.xml
  rm ${pkgdir}/usr/share/foomatic/db/source/printer/Olivetti-d-Color_P160W.xml

}
