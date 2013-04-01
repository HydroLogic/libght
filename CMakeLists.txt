#------------------------------------------------------------------------------
# basics
#------------------------------------------------------------------------------

cmake_minimum_required(VERSION 2.8.7)

project (GHT)


#------------------------------------------------------------------------------
# versions
#------------------------------------------------------------------------------

set (GHT_VERSION_MAJOR 0)
set (GHT_VERSION_MINOR 1)
set (GHT_VERSION_PATCH 0)

# full path for identification
set (GHT_VERSION "${GHT_VERSION_MAJOR}.${GHT_VERSION_MINOR}.${GHT_VERSION_PATCH}")

# API breaking changes can happen at minor version update
set (GHT_LIB_SOVERSION "${GHT_VERSION_MAJOR}.${GHT_VERSION_MINOR}")


#------------------------------------------------------------------------------
# internal cmake settings
#------------------------------------------------------------------------------

set (CMAKE_COLOR_MAKEFILE ON)

# Path to additional CMake modules
set (CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake/modules ${CMAKE_MODULE_PATH})


#------------------------------------------------------------------------------
# all the tools use the API
#------------------------------------------------------------------------------

# ght.h is in the src directory
include_directories ("${PROJECT_SOURCE_DIR}/src")


#------------------------------------------------------------------------------
# must find libxml2
#------------------------------------------------------------------------------

find_package(LibXml2 REQUIRED)
mark_as_advanced(CLEAR LIBXML2_INCLUDE_DIR)
mark_as_advanced(CLEAR LIBXML2_LIBRARIES)
include_directories(${LIBXML2_INCLUDE_DIR})
set(GHT_HAVE_LIBXML2 1)

include(FindCUnit)

#------------------------------------------------------------------------------
# build the library, then the test suite
#------------------------------------------------------------------------------

add_subdirectory (src) 
add_subdirectory (test) 
