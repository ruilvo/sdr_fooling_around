cmake_minimum_required(VERSION 3.17 FATAL_ERROR)

project(sdr_fooling_around)

set(BINARY_EXTDEP_DIR "${CMAKE_BINARY_DIR}/extdep")

# Download miniaudio as required
if(NOT EXISTS "${BINARY_EXTDEP_DIR}/include/miniaudio/miniaudio.h")
  message(STATUS "Downloading miniaudio.h")
  file(DOWNLOAD
       "https://raw.githubusercontent.com/mackron/miniaudio/master/miniaudio.h"
       "${BINARY_EXTDEP_DIR}/include/miniaudio/miniaudio.h" TLS_VERIFY ON)
else()
  message(STATUS "Found miniaudio.h")
endif()

add_executable(
  miniaudio_example
  "${CMAKE_CURRENT_SOURCE_DIR}/src/miniaudio_example/miniaudio_example.cpp")
target_include_directories(miniaudio_example
                           PRIVATE "${CMAKE_BINARY_DIR}/extdep/include")
