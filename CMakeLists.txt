cmake_minimum_required(VERSION 3.21)
cmake_policy(SET CMP0110 NEW)

if(NOT PROJECT_NAME AND NOT PROJECT_IS_TOP_LEVEL)
    set(CMAKE_TOOLCHAIN_FILE "$ENV{VCPKG_ROOT}/scripts/buildsystems/vcpkg.cmake")
    message("Toolchain=${CMAKE_TOOLCHAIN_FILE}")
    project(gumbo_query CXX)
endif()

include_directories(include)

include(CTest)
include(cmake/PreventInSourceBuilds.cmake)

# Debug build.
set(CMAKE_VERBOSE_MAKEFILE ON)
set(CMAKE_BUILD_TYPE Debug)

# Set our output directories.
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_LIBRARY_OUTPUT_DIRECTORY})

# Create library directory if it does not exist.
file(MAKE_DIRECTORY ${CMAKE_LIBRARY_OUTPUT_DIRECTORY})

# Add the cmake modules directory to our module path.
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${PROJECT_SOURCE_DIR}/cmake)
find_package(unofficial-gumbo CONFIG REQUIRED)

set(Gumbo_LIBRARY unofficial::gumbo::gumbo)

# Set our library source directory.
set(gumbo_query_SOURCE_DIRECTORY ${PROJECT_SOURCE_DIR}/src)

# Add source subdirectories.
add_subdirectory(src)