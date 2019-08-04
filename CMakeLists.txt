cmake_minimum_required(VERSION 3.1)
project(cpp_localization)

set(CMAKE_CXX_STANDARD 11)

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/build/bin)
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/build/lib)

#############################
#Dependencies
#############################

find_package(Eigen3 REQUIRED)
include_directories(${EIGEN3_INCLUDE_DIR})

find_package(OpenCV REQUIRED)
#include_directories(${EIGEN3_INCLUDE_DIR})
include_directories(OpenCV_INCLUDE_DIR)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

##############################
#Localization
##############################

add_library(ukflib SHARED src/unscented_kalman_filter.cpp)

##############################
# Tests
##############################

set(LIB_TEST_SOURCES
    ${CMAKE_CURRENT_SOURCE_DIR}/src/unscented_kalman_filter_test.cpp
)

add_executable(ukftest ${LIB_TEST_SOURCES})
target_link_libraries(ukftest ukflib ${OpenCV_LIBS} gtest_main)


#### googletest
# Download and unpack googletest at configure time
configure_file(CMakeLists.txt.googletest googletest-download/CMakeLists.txt)
execute_process(COMMAND ${CMAKE_COMMAND} -G "${CMAKE_GENERATOR}" .
  RESULT_VARIABLE result
  WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/googletest-download )
if(result)
  message(FATAL_ERROR "CMake step for googletest failed: ${result}")
endif()
execute_process(COMMAND ${CMAKE_COMMAND} --build .
  RESULT_VARIABLE result
  WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/googletest-download )
if(result)
  message(FATAL_ERROR "Build step for googletest failed: ${result}")
endif()

# Prevent overriding the parent project's compiler/linker
# settings on Windows
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)

# Add googletest directly to our build. This defines
# the gtest and gtest_main targets.
add_subdirectory(${CMAKE_CURRENT_BINARY_DIR}/googletest-src
                 ${CMAKE_CURRENT_BINARY_DIR}/googletest-build
                 EXCLUDE_FROM_ALL)

# The gtest/gtest_main targets carry header search path
# dependencies automatically when using CMake 2.8.11 or
# later. Otherwise we have to add them here ourselves.
if (CMAKE_VERSION VERSION_LESS 2.8.11)
  include_directories("${gtest_SOURCE_DIR}/include")
endif()
