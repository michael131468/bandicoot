cmake_minimum_required(VERSION 3.15)
project(Bandicoot VERSION 1.0.1)

set(CMAKE_CXX_VISIBILITY_PRESET hidden)
set(CMAKE_C_VISIBILITY_PRESET hidden)

add_library(bandicoot SHARED bandicoot.h bandicoot.cpp)
target_include_directories(bandicoot PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

set_target_properties(bandicoot PROPERTIES VERSION 1.0.1 SOVERSION 1)
set_target_properties(bandicoot PROPERTIES PUBLIC_HEADER bandicoot.h)

configure_file(bandicoot.pc.in bandicoot.pc @ONLY)

add_executable(bandicootDemo main.cpp)
target_link_libraries(bandicootDemo LINK_PUBLIC bandicoot)

include(GNUInstallDirs)
install(TARGETS bandicoot bandicootDemo
	RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
	LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
	PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
install(FILES ${CMAKE_BINARY_DIR}/bandicoot.pc DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/pkgconfig)
