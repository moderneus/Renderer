cmake_minimum_required(VERSION 4.2)

set(CMAKE_CXX_COMPILER clang++)
set(CMAKE_C_COMPILER clang)

set(TARGET Renderer)

project(${TARGET})

find_package(Vulkan REQUIRED)

file(GLOB_RECURSE SRC "src/*.cpp")

add_executable(${TARGET} ${SRC})

target_compile_options(${TARGET} PRIVATE --std=c++20 -g -O1 -Wall -Werror)

target_link_libraries(${TARGET} PRIVATE Vulkan::Vulkan)
