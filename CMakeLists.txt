cmake_minimum_required(VERSION 3.10)
project(clandro-am-socket)

if (CMAKE_INSTALL_PREFIX STREQUAL "/usr/local")
    set(CMAKE_INSTALL_PREFIX $ENV{PREFIX})
    message(STATUS "prefix set from env: " ${CMAKE_INSTALL_PREFIX})
endif()

set(CLANDRO_PREFIX ${CMAKE_INSTALL_PREFIX})

configure_file(
    ${CMAKE_CURRENT_SOURCE_DIR}/clandro-am.h.in
    clandro-am.h @ONLY
)

configure_file(
  ${CMAKE_CURRENT_SOURCE_DIR}/clandro-am.sh.in
  clandro-am @ONLY
)

add_executable(clandro-am-socket clandro-am.cpp)
target_include_directories(clandro-am-socket PUBLIC ${CMAKE_BINARY_DIR})


install(FILES ${CMAKE_BINARY_DIR}/clandro-am TYPE BIN PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE)
install(TARGETS clandro-am-socket DESTINATION bin PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE)
