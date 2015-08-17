pkgdesc="ROS - XmlRpc++ is a C++ implementation of the XML-RPC protocol."
url='http://www.ros.org/'

pkgname='ros-groovy-xmlrpcpp'
pkgver='1.9.50'
arch=('i686' 'x86_64')
pkgrel=1
license=('LGPL')
makedepends=('ros-build-tools')

depends=(ros-groovy-cpp-common
  ros-groovy-catkin)

build() {
  [ -f /opt/ros/groovy/setup.bash ] && source /opt/ros/groovy/setup.bash
  if [ -d ${srcdir}/xmlrpcpp ]; then
    cd ${srcdir}/xmlrpcpp
    git fetch origin --tags
    git reset --hard release/groovy/xmlrpcpp/${pkgver}-0
  else
    git clone -b release/groovy/xmlrpcpp/${pkgver}-0 git://github.com/ros-gbp/ros_comm-release.git ${srcdir}/xmlrpcpp
  fi
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/xmlrpcpp
  cmake ${srcdir}/xmlrpcpp -DCATKIN_BUILD_BINARY_PACKAGE=ON -DCMAKE_INSTALL_PREFIX=/opt/ros/groovy -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
