cmake_minimum_required(VERSION 3.14)
project(ds_lib LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include(FetchContent)
FetchContent_Declare(
  googletest
  URL C:/libs/googletest-1.14.0.zip
  DOWNLOAD_EXTRACT_TIMESTAMP true
)
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

add_library(dslib INTERFACE)
target_include_directories(dslib INTERFACE include)

enable_testing()
add_executable(tests tests/smoke_test.cpp)
target_link_libraries(tests PRIVATE dslib GTest::gtest_main)

include(GoogleTest)
gtest_discover_tests(tests)