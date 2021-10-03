cmake_minimum_required(VERSION 3.15)

project(qluacpp_test)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

include( FetchContent )

FetchContent_Declare(
    Catch2
    GIT_REPOSITORY https://github.com/catchorg/Catch2.git
    GIT_TAG        v2.13.7
    )

FetchContent_MakeAvailable(Catch2)

FetchContent_Declare(
    luacpp
    GIT_REPOSITORY https://github.com/scripter-v/luacpp.git
    GIT_TAG        v1.0.0
    )

FetchContent_MakeAvailable(luacpp)

find_package(Lua REQUIRED)
message ("Lua library: ${LUA_LIBRARIES}")
message ("Lua include dir: ${LUA_INCLUDE_DIR}")
message ("Lua version: ${LUA_VERSION_STRING}")

get_filename_component(TOP_DIR "${CMAKE_CURRENT_SOURCE_DIR}" PATH)
set(SRC "${TOP_DIR}/src")

include_directories(
  ${TOP_DIR}/include
  ${LUA_INCLUDE_DIR}
)

set(TEST_SOURCES
  qluacpp_test.cpp)

add_executable(qluacpp_test
  ${TEST_SOURCES})

target_compile_definitions(qluacpp_test PUBLIC "CATCH_CONFIG_MAIN")

target_link_libraries(qluacpp_test ${LUA_LIBRARIES})
target_link_libraries(qluacpp_test Catch2::Catch2)
target_link_libraries(qluacpp_test luacpp)

add_test(CommonTests qluacpp_test)
