cmake_minimum_required(VERSION 4.2)

set(CMAKE_CXX_COMPILER clang++)
set(CMAKE_C_COMPILER clang)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(TARGET Renderer)

project(${TARGET})

find_package(Vulkan REQUIRED)

file(GLOB_RECURSE INTERFACES CONFIGURE_DEPENDS "modules/*.cppm")
file(GLOB_RECURSE IMPLEMENTATION CONFIGURE_DEPENDS "modules/*.cpp")

add_executable(${TARGET} src/Main.cpp)

target_sources(${TARGET}
  PRIVATE
    ${IMPLEMENTATION}
  PUBLIC
  FILE_SET CXX_MODULES
  BASE_DIRS modules 
  FILES
    ${INTERFACES}

)

target_compile_options(${TARGET} PRIVATE --std=c++23 -fmodules -g -O1 -Wall -Werror)

target_link_libraries(${TARGET} PRIVATE Vulkan::Vulkan)
