cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(onsyte VERSION 1.0)

# install rules
# install(TARGETS onsyte RUNTIME DESTINATION /usr/local/bin)
# set(appdir "/mnt/user_data/devuser_jail/home/devuser/apps")
set(appdir "/home/devuser/apps")
install(FILES ../hello/src/hello.py DESTINATION ${appdir}/hello)
# install(FILES "${PROJECT_BINARY_DIR}/helloConfig.h"
#   DESTINATION include
#   )

# use CPack module
include(InstallRequiredSystemLibraries)
SET(CPACK_GENERATOR "DEB")
SET(CPACK_DEBIAN_PACKAGE_MAINTAINER "FreeWave") #required
SET(CPACK_DEBIAN_PACKAGE_ARCHITECTURE "armhf")
SET(CPACK_DEBIAN_PACKAGE_SECTION "util")
set(CPACK_RESOURCE_FILE_LICENSE "${CMAKE_CURRENT_SOURCE_DIR}/License.txt")
set(CPACK_PACKAGE_VERSION_MAJOR "${onsyte_VERSION_MAJOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${onsyte_VERSION_MINOR}")
set(CPACK_DEBIAN_PACKAGE_DEPENDS "") 
set(CPACK_DEBIAN_PACKAGE_CONTROL_EXTRA "${CMAKE_CURRENT_LIST_DIR}/preinst,${CMAKE_CURRENT_LIST_DIR}/postinst,${CMAKE_CURRENT_LIST_DIR}/postrm")
include(CPack)

