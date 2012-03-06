project(foo)

cmake_minimum_required(VERSION 2.8)

set(PACKAGE_MAJOR_VERSION "0")
set(PACKAGE_MINOR_VERSION "1")
set(PACKAGE_BUILD_VERSION "0")
set(PACKAGE_VERSION "${PACKAGE_MAJOR_VERSION}.${PACKAGE_MINOR_VERSION}.${PACKAGE_BUILD_VERSION}")

add_subdirectory("inc")
add_subdirectory("src")

configure_file(
	${CMAKE_CURRENT_SOURCE_DIR}/foo-config.cmake.in
	${CMAKE_CURRENT_BINARY_DIR}/foo-config.cmake @ONLY
)
configure_file(
	${CMAKE_CURRENT_SOURCE_DIR}/foo-config-version.cmake.in
	${CMAKE_CURRENT_BINARY_DIR}/foo-config-version.cmake @ONLY
)
install(FILES
	${CMAKE_CURRENT_BINARY_DIR}/foo-config.cmake
	${CMAKE_CURRENT_BINARY_DIR}/foo-config-version.cmake
	DESTINATION "lib/cmake/${PROJECT_NAME}"
)
