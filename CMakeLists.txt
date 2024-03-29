project(x11ew)

cmake_minimum_required (VERSION 2.6)
if (NOT CMAKE_VERSION VERSION_LESS 2.8.4)
  cmake_policy (SET CMP0017 NEW)
endif()

include(CMakeParseArguments)

set(CMAKE_ALLOW_LOOSE_LOOP_CONSTRUCTS TRUE)
message(STATUS "Project source dir = ${PROJECT_SOURCE_DIR}")
message(STATUS "Project build dir = ${CMAKE_BINARY_DIR}")

if(CMAKE_COMPILER_IS_GNUCC)
  set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fPIC")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC")
endif()

include_directories(include)

add_library(x11ew
  src/x11ew.c
  src/x11ew_xkblib.c
  src/x11ew_xlib.c
  src/x11ew_xlibint.c
  src/x11ew_xlib-xcb.c

  src/x11ew_private.h

  include/x11ew.h
  include/x11ew_xkblib.h
  include/x11ew_xlib.h
  include/x11ew_xlibint.h
  include/x11ew_xlib-xcb.h
)

add_executable(testx11ew x11ewTest/x11ewTest.c include/x11ew.h)
target_link_libraries(testx11ew x11ew ${CMAKE_DL_LIBS})
