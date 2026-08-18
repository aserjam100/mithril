cmake_minimum_required(VERSION 3.20)
project(mithril CXX C)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Debug)
endif()

add_compile_options(-Wall -Wextra -Wpedantic)
if(CMAKE_BUILD_TYPE STREQUAL "Debug")
  add_compile_options(-fsanitize=address,undefined)
  add_link_options(-fsanitize=address,undefined)
endif()

include(FetchContent)
FetchContent_Declare(
  glfw
  GIT_REPOSITORY https://github.com/glfw/glfw.git
  GIT_TAG 3.4
)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(glfw)

add_library(glad STATIC third_party/src/gl.c)
target_include_directories(glad PUBLIC third_party/include)

add_executable(mithril src/main.cpp)
target_link_libraries(mithril PRIVATE glfw glad)

if(APPLE)
  target_link_libraries(mithril PRIVATE
    "-framework Cocoa"
    "-framework IOKit"
    "-framework CoreVideo"
    "-framework OpenGL"
  )
endif()
