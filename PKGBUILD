# Maintainer: Anthony Rabine anthony.rabine@tarotclub.fr

_pkgname=tarotclub
pkgname="${_pkgname}-hg"
pkgver=1531.318ebe275da7
pkgrel=1
_hgtag=VERSION_2_5_1
pkgdesc="A local/network French Tarot card game."
url="http://www.tarotclub.fr"
arch=('any')
license=('GPLv3')
depends=('qt5-base' 'qt5-svg' 'libgl')
optdepends=()
makedepends=('mercurial')
conflicts=('tarotclub')
replaces=()
backup=()
install='tarotclub-hg.install'
# Adding the tag does not work :(  #tag=
source=('tarotclub.desktop' 'tarotclub.sh' "hg+https://bitbucket.org/tarotclub/tarotclub#tag=${_hgtag}")

# MD5 signature of source files
md5sums=('289ae912415776f7f77f907ec64ff067'
         '4aaef27ca4b547493c879d76f24beea7'
         'SKIP')

pkgver() {
  cd $_pkgname
  echo $(hg identify -n).$(hg identify -i)
}

build() {
    cd "${srcdir}/${_pkgname}"
    qmake prj/desktop.pro
    make

}
package() {
    cd "${srcdir}/${_pkgname}"

    ## EXECUTABLE AND RELATED FILES ##

    install -Dm644 ./COPYING "${pkgdir}"/usr/share/tarotclub/COPYING
    install -Dm644 ./HISTORY.md "${pkgdir}"/usr/share/tarotclub/HISTORY.md
    install -Dm644 ./README.md "${pkgdir}"/usr/share/tarotclub/README.md
    install -Dm755 ./build-desktop/release/TarotClub "${pkgdir}"/usr/share/tarotclub
    install -Dm644 ./assets/fonts/kanzlei.ttf "${pkgdir}"/usr/share/tarotclub/kanzlei.ttf
    install -Dm644 ./assets/fonts/kanzlei.ttf "${pkgdir}"/usr/share/fonts/TTF/kanzlei.ttf
    install -Dm644 ./prj/desktop/tarotclub_fr.qm "${pkgdir}"/usr/share/tarotclub/tarotclub_fr.qm

    ## CARDS ##
    cp -r ./assets/cards/default/ "${pkgdir}"/usr/share/tarotclub/
    chmod 644 "${pkgdir}"/usr/share/tarotclub/default/*

    ## AI JAVASCRIPT FILES ##

    install -d "${pkgdir}"/usr/share/tarotclub/ai/tarotlib/
    cp -a ./assets/ai/tarotlib/{system,util,card,deck,player,bot,game}.js "${pkgdir}"/usr/share/tarotclub/ai/tarotlib/
    chmod 644 "${pkgdir}"/usr/share/tarotclub/ai/tarotlib/*
    install -Dm644 ./assets/ai/noob.js "${pkgdir}"/usr/share/tarotclub/ai/noob.js
    install -Dm644 ./assets/ai/noob.json "${pkgdir}"/usr/share/tarotclub/ai/noob.json

    ## ICONS ##
    install -Dm644 ./assets/icons/icon256x256.png "${pkgdir}"/usr/share/pixmaps/tarotclub.png
    install -Dm644 ./assets/icons/club.svg "${pkgdir}"/usr/share/icons/hicolor/scalable/apps/tarotclub.svg
    for res in 16 32 48 128 256 512; do
        install -Dm644 "./assets/icons/icon${res}x${res}.png" \
                     "${pkgdir}/usr/share/icons/hicolor/${res}x${res}/apps/tarotclub.png"
    done

    ## DOCUMENTATION ##

    install -Dm644 ./doc/index.html           "${pkgdir}"/usr/share/tarotclub/doc/index.html
    install -Dm644 ./doc/rules_en.html        "${pkgdir}"/usr/share/tarotclub/doc/rules_en.html
    install -Dm644 ./doc/rules_fr.html        "${pkgdir}"/usr/share/tarotclub/doc/rules_fr.html
    cp -r ./doc/images/                       "${pkgdir}"/usr/share/tarotclub/doc
    chmod 644 "${pkgdir}"/usr/share/tarotclub/doc*

    ## MISC FILES LOCATED AT THE PACKAGE ROOT ##
    
    cd "$srcdir/"
    install -Dm644 tarotclub.desktop "${pkgdir}"/usr/share/applications/tarotclub.desktop  
    install -Dm755 tarotclub.sh "${pkgdir}"/usr/bin/tarotclub
}

