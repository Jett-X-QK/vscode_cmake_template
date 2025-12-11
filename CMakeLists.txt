cmake_minimum_required(VERSION 3.29)

project(CPP_CODE)

# 设置 C 和 C++ 标准
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 11)

# 收集所有 C 和 C++ 源文件
file(GLOB C_SRC ${CMAKE_CURRENT_SOURCE_DIR}/src/*.c)
file(GLOB CPP_SRC ${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp)

# 合并所有源文件
set(ALL_SRC ${C_SRC} ${CPP_SRC})

# 设置输出目录
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")

# 创建目录（确保目录存在）
file(MAKE_DIRECTORY "${CMAKE_RUNTIME_OUTPUT_DIRECTORY}")

add_executable(main ${ALL_SRC})

# 设置头文件目录
target_include_directories(main PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include)


# # 配置 Debug 版本
# cmake -B build -G "MinGW Makefiles" -DCMAKE_BUILD_TYPE=Debug
# # 构建 Debug 版本
# cmake --build build
# # 可执行文件会在 build/bin/main.exe（Windows）或 build/bin/main（Linux/Mac）

# # 配置 Release 版本
# cmake -B build_release -G "MinGW Makefiles" -DCMAKE_BUILD_TYPE=Release
# # 构建 Release 版本
# cmake --build build_release
