cmake_minimum_required(VERSION 3.16)
project(prj)
 
# Include CPM
include(cmake/CPM.cmake)
 
# Add libultrahdr as a dependency
CPMAddPackage(
    NAME libuhdr
    GITHUB_REPOSITORY anshjain04/libultrahdr
    # VERSION 1.4.0
    GIT_TAG e4788226b205fdd99700eaee222a692edf95
    OPTIONS "BUILD_SHARED_LIBS OFF"
            "UHDR_BUILD_EXAMPLES OFF"
            "UHDR_BUILD_TESTS OFF"
            "UHDR_BUILD_BENCHMARK OFF"
            "UHDR_BUILD_FUZZERS OFF"
            "UHDR_ENABLE_INTRINSICS OFF"
            "BUILD_SHARED_LIBS ON"
)
 
# Add an executable for the upstream project
add_executable(uprj src/main.cpp)

find_package(libuhdr REQUIRED)

set(LIBUHDR_INCLUDED 1)

configure_file(config.h.in config.h @ONLY)


include_directories ($ {CMAKE_CURRENT_BINARY_DIR})
 
# Link against uhdr
target_link_libraries(uprj PRIVATE uhdr)