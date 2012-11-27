project(foo)

cmake_minimum_required(VERSION 2.8.8)

set(PACKAGE_MAJOR_VERSION "0")
set(PACKAGE_MINOR_VERSION "1")
set(PACKAGE_BUILD_VERSION "0")
set(PACKAGE_VERSION "${PACKAGE_MAJOR_VERSION}.${PACKAGE_MINOR_VERSION}.${PACKAGE_BUILD_VERSION}")

include(GNUInstallDirs)	# cmake 2.8.5

add_subdirectory("inc")
add_subdirectory("src")

include(CMakePackageConfigHelpers)	# cmake 2.8.8
configure_package_config_file(foo-config.cmake.in
	"${CMAKE_CURRENT_BINARY_DIR}/foo-config.cmake"
	INSTALL_DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}"
	PATH_VARS CMAKE_INSTALL_INCLUDEDIR
	NO_CHECK_REQUIRED_COMPONENTS_MACRO
)
write_basic_package_version_file(
	"${CMAKE_CURRENT_BINARY_DIR}/foo-config-version.cmake"
	VERSION ${PACKAGE_VERSION}
	COMPATIBILITY AnyNewerVersion
)
install(FILES
	"${CMAKE_CURRENT_BINARY_DIR}/foo-config.cmake"
	"${CMAKE_CURRENT_BINARY_DIR}/foo-config-version.cmake"
	DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}"
)
