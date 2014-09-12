cmake_minimum_required (VERSION 2.6)
project (BingRequest)

# Build static casablanca library without tests
set(BUILD_SHARED_LIBS OFF CACHE BOOL "Build shared Libraries.")
set(BUILD_TESTS OFF CACHE BOOL "Build tests.")
set(BUILD_SAMPLES OFF CACHE BOOL "Build samples.")
add_subdirectory(../casablanca/Release "${CMAKE_CURRENT_BINARY_DIR}/casablanca/Release")

# Get the Casablanca properties from the Casablanca subdirectory
get_directory_property(Casablanca_LIBRARY
    DIRECTORY ../casablanca/Release
    DEFINITION Casablanca_LIBRARY)

get_directory_property(Casablanca_INCLUDE_DIR
    DIRECTORY ../casablanca/Release
    DEFINITION Casablanca_INCLUDE_DIR)

# Need these option or we can't compile with all the advanced c++
add_definitions(-std=c++11)

add_executable(BingRequest bingrequest.cpp)

include_directories (${Casablanca_INCLUDE_DIR})
target_link_Libraries(BingRequest ${Casablanca_LIBRARY})

#install (TARGETS sample DESTINATION bin)
