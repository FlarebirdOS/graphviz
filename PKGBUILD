pkgname=graphviz
pkgver=14.0.0
pkgrel=1
pkgdesc="Graph visualization software"
arch=('x86_64')
url="https://www.graphviz.org"
license=('EPL')
depends=(
    'gd'
    'gts'
    'libtool'
    'librsvg'
    'pango'
    'ghostscript'
)
makedepends=(
    'swig'
    'guile'
    'lua'
    'mono'
    'perl'
    'python'
    'qt6-qtbase'
    'r'
    'tk'
)
source=(https://gitlab.com/graphviz/graphviz/-/archive/${pkgver}/${pkgname}-${pkgver}.tar.bz2)
sha256sums=(78d06cf3db0cc2298199d9ca0a9dd4be7f623f90f70ca72f60f1880d848a4f3d)

prepare() {
    cd ${pkgname}-${pkgver}

    ./autogen.sh NOCONFIG
}

build() {
    cd ${pkgname}-${pkgver}

    local configure_args=(
        --enable-python3=yes
        --disable-python
        --enable-lefty
        ${configure_options}
    )

    export LIBPOSTFIX=/
    export CXXFLAGS+=' -fPIC -fpermissive'

    ./configure "${configure_args[@]}"

    make
}

package() {
    cd ${pkgname}-${pkgver}

    make DESTDIR=${pkgdir} install

    # fix symlink to symlink that doesn't get picked up by makepkg's zipman
    ln -s gv2gxl.1.gz ${pkgdir}/usr/share/man/man1/dot2gxl.1.gz
    rm ${pkgdir}/usr/share/man/man1/dot2gxl.1
}
