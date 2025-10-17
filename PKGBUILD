pkgname=qt6-qt3d
pkgver=6.10.0
pkgrel=2
pkgdesc="C++ and QML APIs for easy inclusion of 3D graphics"
arch=('x86_64')
url="https://www.qt.io"
license=(
    'GPL-3.0-only'
    'LGPL-3.0-only'
    'LicenseRef-Qt-Commercial'
    'Qt-GPL-exception-1.0'
)
depends=(
    'gcc-libs'
    'glibc'
    'qt6-qtbase'
)
makedepends=(
    'assimp'
    'cmake'
    'git'
    'ninja'
    'qt6-qtdeclarative'
    'qt6-qtshadertools'
    'shaderc'
    'vulkan-headers'
    'vulkan-loader'
)
source=(git+https://code.qt.io/qt/${pkgname#*-}#tag=v${pkgver}
    assimp-6.patch)
sha256sums=(7e783a3f7c1e88f4005559c44179e33494fc649766255b87b329a4818a33dbde
    244589b0a353da757d61ce6b86d4fcf2fc8c11e9c0d9c5b109180cec9273055a)

prepare() {
    cd ${pkgname#*-}

    patch -p1 < ${srcdir}/assimp-6.patch
}

build() {
    cd ${pkgname#*-}

    local cmake_args=(
        -B flarebird-build
        -G Ninja
        -D CMAKE_BUILD_TYPE=Release
        -D CMAKE_INSTALL_PREFIX=/usr
        -D INSTALL_LIBDIR=lib64
        -D CMAKE_MESSAGE_LOG_LEVEL=STATUS
    )

    cmake "${cmake_args[@]}"

    cmake --build flarebird-build
}

package() {
    cd ${pkgname#*-}

    DESTDIR=${pkgdir} cmake --install flarebird-build
}
