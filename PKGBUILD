# Maintainer: Hermann von Kleist (stertingen yahoo com)
pkgdesc="ROS - Underlying data libraries for roscpp messages."
url='https://www.wiki.ros.org/roscpp_core'
pkgbase='ros-noetic-roscpp-core'
pkgname=(
    'ros-noetic-cpp-common'
    'ros-noetic-roscpp-core'
    'ros-noetic-roscpp-serialization'
    'ros-noetic-roscpp-traits'
    'ros-noetic-rostime'
)
pkgver='0.7.1'
arch=('i686' 'x86_64' 'aarch64' 'armv7h' 'armv6h')
pkgrel=1
license=('BSD')

source=("${pkgname}-${pkgver}.tar.gz"::"https://github.com/ros/roscpp_core/archive/${pkgver}.tar.gz")
sha256sums=('8fddbafd3fc76470e4a706f7923b7a03f914943d7edb0b70273d8b98e003b108')

makedepends=(
    boost
    cmake
    console-bridge
    ros-build-tools
    ros-noetic-catkin
)

build() {
    # Use ROS environment variables.
    source /usr/share/ros-build-tools/clear-ros-env.sh
    [ -f /opt/ros/noetic/setup.bash ] && source /opt/ros/noetic/setup.bash

    catkin_make_isolated \
        --directory ${srcdir} \
        --source ${srcdir}/roscpp_core-${pkgver} \
        --install-space /opt/ros/noetic \
        --cmake-args \
        -DCMAKE_BUILD_TYPE=Release \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DPYTHON_EXECUTABLE=/usr/bin/python3 \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
}

check() {
    catkin_make_isolated \
        --directory ${srcdir} \
        --source ${srcdir}/roscpp_core-${pkgver} \
        --install-space /opt/ros/noetic \
        --catkin-make-args run_tests
}

package_ros-noetic-cpp-common() {
    pkgdesc="ROS - cpp_common contains C++ code for doing things that are not necessarily ROS related, but are useful for multiple packages."
    url='https://wiki.ros.org/cpp_common'
    depends=(
        boost
        console-bridge
    )
    cd "${srcdir}/build_isolated/cpp_common"
    make DESTDIR="${pkgdir}/" install
}

package_ros-noetic-roscpp-core() {
    pkgdesc="ROS - Underlying data libraries for roscpp messages."
    url='https://www.wiki.ros.org/roscpp_core'
    depends=(
        ros-noetic-roscpp-traits
        ros-noetic-cpp-common
        ros-noetic-rostime
        ros-noetic-roscpp-serialization
    )
    cd "${srcdir}/build_isolated/roscpp_core"
    make DESTDIR="${pkgdir}/" install
}

package_ros-noetic-roscpp-serialization() {
    pkgdesc="ROS - roscpp_serialization contains the code for serialization as described in MessagesSerializationAndAdaptingTypes."
    url='https://wiki.ros.org/roscpp_serialization'
    depends=(
        ros-noetic-roscpp-traits
        ros-noetic-cpp-common
        ros-noetic-rostime
    )
    cd "${srcdir}/build_isolated/roscpp_serialization"
    make DESTDIR="${pkgdir}/" install
}

package_ros-noetic-roscpp-traits() {
    pkgdesc="ROS - roscpp_traits contains the message traits code as described in MessagesTraits."
    url='https://wiki.ros.org/roscpp_traits'
    depends=(
        ros-noetic-rostime
        ros-noetic-cpp-common
    )
    cd "${srcdir}/build_isolated/roscpp_traits"
    make DESTDIR="${pkgdir}/" install
}

package_ros-noetic-rostime() {
    pkgdesc="ROS - Time and Duration implementations for C++ libraries, including roscpp."
    url='https://wiki.ros.org/rostime'
    depends=(
        boost
        ros-noetic-cpp-common
    )
    cd "${srcdir}/build_isolated/rostime"
    make DESTDIR="${pkgdir}/" install
}
