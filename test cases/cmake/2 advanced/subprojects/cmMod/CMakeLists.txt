cmake_minimum_required(VERSION 3.5)

project(cmMod)
set(CMAKE_CXX_STANDARD 14)

find_package(ZLIB REQUIRED)

include_directories(${CMAKE_CURRENT_BINARY_DIR} ${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_SOURCE_DIR}/lib)

set(CONFIG_OPT 42)
configure_file("config.h.in" "${CMAKE_CURRENT_BINARY_DIR}/config.h" @ONLY)

add_library(cmModLib SHARED lib/cmMod.cpp)
include(GenerateExportHeader)
generate_export_header(cmModLib)

add_executable(testEXE main.cpp)

target_link_libraries(cmModLib ZLIB::ZLIB)
target_link_libraries(testEXE cmModLib)

install(TARGETS cmModLib testEXE LIBRARY DESTINATION lib RUNTIME DESTINATION bin)
