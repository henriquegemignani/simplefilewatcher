# Test for minimum required CMake version 2.8.12
cmake_minimum_required(VERSION 2.8.12 FATAL_ERROR)

project(simplefilewatcher)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14")

include_directories(include)

set(HEADERS
    include/FileWatcher/FileWatcher.h
    include/FileWatcher/FileWatcherImpl.h
    include/FileWatcher/FileWatcherLinux.h
    include/FileWatcher/FileWatcherOSX.h
    include/FileWatcher/FileWatcherWin32.h
)

set(SOURCES
    source/FileWatcher.cpp
    source/FileWatcherLinux.cpp
    source/FileWatcherOSX.cpp
    source/FileWatcherWin32.cpp
    ${HEADERS}
)

add_library(simplefilewatcher STATIC ${SOURCES})

add_executable(simple-demo SimpleDemo.cpp)
target_link_libraries(simple-demo simplefilewatcher)