cmake_minimum_required(VERSION 3.27)

project(polaris-wasm VERSION 0.1 LANGUAGES C CXX)

# 设置语言标准
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
if (WIN32)
        set(CMAKE_C_STANDARD 17)
else()
        set(CMAKE_C_STANDARD 23)
endif()
set(CMAKE_C_STANDARD_REQUIRED ON)

# 设置开启显示详细的构建过程
set(CMAKE_VERBOSE_MAKEFILE ON)

# 启用测试
enable_testing()

# 查找并设置ccache
find_program(CCACHE_PROGRAM ccache)
if (CCACHE_PROGRAM)
    message(STATUS "Found ccache: ${CCACHE_PROGRAM}")
    set_property(GLOBAL PROPERTY RULE_LAUNCH_COMPILE "${CCACHE_PROGRAM}")
endif ()

# 设置生成clangd compile_commands.json文件，方便和IDE集成
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

add_library(polaris-wasm STATIC
    wasm.cpp
    wasm.h
)

add_subdirectory(browser)
add_subdirectory(server)
