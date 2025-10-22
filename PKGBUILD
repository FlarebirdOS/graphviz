pkgname=graphviz
pkgver=14.0.2
pkgrel=2
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
sha256sums=(d4d8baa81471166a3d81670cc38870b37f1a4f6f0c473ad7a2f0a74c9914a8e0)

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
