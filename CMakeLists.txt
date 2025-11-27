cmake_minimum_required(VERSION 3.30)

project(CPP_CODE)

set(CMAKE_CXX_STANDARD 11)
# # 强制使用 GCC
# set(CMAKE_C_COMPILER "gcc")
# set(CMAKE_CXX_COMPILER "g++")

# 设置不同构建类型的输出目录
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_DEBUG ${CMAKE_CURRENT_SOURCE_DIR}/build/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_DEBUG ${CMAKE_CURRENT_SOURCE_DIR}/build/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG ${CMAKE_CURRENT_SOURCE_DIR}/build/bin)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_RELEASE ${CMAKE_CURRENT_SOURCE_DIR}/release/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_RELEASE ${CMAKE_CURRENT_SOURCE_DIR}/release/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE ${CMAKE_CURRENT_SOURCE_DIR}/release/bin)

file(GLOB SRC ${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp)


# 如果没有指定构建类型，默认为Debug
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Debug)
endif()

add_executable(main ${SRC})

# 使用现代的方式设置头文件目录
target_include_directories(main PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include)

# 为不同构建类型设置编译选项
target_compile_definitions(main PRIVATE
    $<$<CONFIG:Release>:NDEBUG>
)

target_compile_options(main PRIVATE
    $<$<CONFIG:Release>:-O3 -march=native>
    $<$<CONFIG:Debug>:-O0 -g3 -ggdb>
)

# 设置Release模式下的链接选项
target_link_options(main PRIVATE
    $<$<CONFIG:Release>:-s>
)

# # 配置 Debug 版本
# cmake -B build_debug -G "MinGW Makefiles" -D CMAKE_BUILD_TYPE=Debug
# # 构建 Debug 版本
# cmake --build build_debug

# # 配置 Release 版本
# cmake -B build_release -G "MinGW Makefiles" -D CMAKE_BUILD_TYPE=Release
# # 构建 Release 版本
# cmake --build build_release