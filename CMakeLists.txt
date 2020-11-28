cmake_minimum_required(VERSION 3.5)

set(NAME Krakatoa)

project(${NAME} CXX)

include_directories($ENV{VK_SDK_PATH}/include)
include_directories(external)

set_property(GLOBAL PROPERTY USE_FOLDERS ON)

set (VULKAN_LIB1 "$ENV{VK_SDK_PATH}/Lib/vulkan-1.lib")
set (GLFW3_LIB "lib/glfw/glfw3")

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set( CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG "${CMAKE_SOURCE_DIR}/bin/" )
set( CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE "${CMAKE_SOURCE_DIR}/bin/" )
set( CMAKE_LIBRARY_OUTPUT_DIRECTORY_DEBUG "${CMAKE_SOURCE_DIR}/bin/" )
set( CMAKE_LIBRARY_OUTPUT_DIRECTORY_RELEASE "${CMAKE_SOURCE_DIR}/bin/" )
set( CMAKE_ARCHIVE_OUTPUT_DIRECTORY_DEBUG "${CMAKE_SOURCE_DIR}/bin/" )
set( CMAKE_ARCHIVE_OUTPUT_DIRECTORY_RELEASE "${CMAKE_SOURCE_DIR}/bin/" )

set(PROJECTS Krakatoa)

file(GLOB RENDERER src/engine/renderer/*.cpp)

add_executable(Krakatoa ${PROJECT_SOURCE} ${PROJECT_HEADER} ${RENDERER})

source_group("src\\engine\\renderer\\" FILES ${RENDERER})

target_link_libraries(Krakatoa ${VULKAN_LIB} ${GLFW3_LIB} ${VULKAN_LIB1})

if ( CMAKE_CXX_COMPILER_ID MATCHES "Clang|AppleClang|GNU" )
    target_compile_options( Krakatoa PRIVATE -Wall -Wextra -Wunreachable-code -Wpedantic)
endif()
if ( CMAKE_CXX_COMPILER_ID MATCHES "Clang" )
    target_compile_options( Krakatoa PRIVATE -Wweak-vtables -Wexit-time-destructors -Wglobal-constructors -Wmissing-noreturn )
endif()
if ( CMAKE_CXX_COMPILER_ID MATCHES "MSVC" )
    target_compile_options( Krakatoa PRIVATE /W4 /w44265 /w44061 /w44062 )
endif()