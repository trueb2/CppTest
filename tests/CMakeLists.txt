cmake_minimum_required(VERSION 3.8)


project(Test)

project(Bar)

include(CTest)

enable_testing()

include(${CMAKE_SOURCE_DIR}/DownloadProject/DownloadProject.cmake)
download_project(
        PROJ                googletest
        GIT_REPOSITORY      https://github.com/google/googletest.git
        GIT_TAG             master
        UPDATE_DISCONNECTED 1
)

add_subdirectory(${googletest_SOURCE_DIR} ${googletest_BINARY_DIR} EXCLUDE_FROM_ALL)

set(test_SRCS foo_tests/bar.cpp)
add_executable(runUnitTests gtest.cpp ${test_SRCS})
target_link_libraries(runUnitTests gtest gmock core)
