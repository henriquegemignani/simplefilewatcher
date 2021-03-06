cmake_minimum_required(VERSION 2.8.12 FATAL_ERROR)

project(simplefilewatcher)

if((NOT ${CMAKE_CURRENT_SOURCE_DIR} STREQUAL ${CMAKE_CURRENT_BINARY_DIR}) AND (NOT EXISTS "${CMAKE_CURRENT_BINARY_DIR}/.gitignore"))
    # Don't polute the git repository with the generated files for out-of-source builds
    file(WRITE ${CMAKE_CURRENT_BINARY_DIR}/.gitignore "*")
endif()

option(SIMPLEFILEWATCHER_BUILD_DEMO "Build demo application" OFF)

set(SIMPLEFILEWATCHER_HEADERS
    include/FileWatcher/FileWatcher.h
    include/FileWatcher/FileWatcherImpl.h
    include/FileWatcher/FileWatcherLinux.h
    include/FileWatcher/FileWatcherOSX.h
    include/FileWatcher/FileWatcherWin32.h
)

set(SIMPLEFILEWATCHER_SOURCES
    source/FileWatcher.cpp
    source/FileWatcherLinux.cpp
    source/FileWatcherOSX.cpp
    source/FileWatcherWin32.cpp
    ${SIMPLEFILEWATCHER_HEADERS}
)

add_library(simplefilewatcher STATIC ${SIMPLEFILEWATCHER_SOURCES})
target_include_directories(simplefilewatcher PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/include")

if(SIMPLEFILEWATCHER_BUILD_DEMO)
    add_executable(simplefilewatcher-simple-demo SimpleDemo.cpp)
    target_link_libraries(simplefilewatcher-simple-demo simplefilewatcher)
endif()