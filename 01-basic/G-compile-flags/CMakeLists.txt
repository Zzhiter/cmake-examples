cmake_minimum_required(VERSION 3.5)

# Set a default C++ compile flag
set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DEX2" CACHE STRING "Set C++ Compiler Flags" FORCE)

# Set the project name
project (compile_flags)

# Add an executable
add_executable(cmake_examples_compile_flags main.cpp)

# 当编译cmake_examples_compile_flags目标时，会添加一个名为EX3的预处理器宏定义。
# 这个定义只对cmake_examples_compile_flags及其直接依赖的目标可见。
target_compile_definitions(cmake_examples_compile_flags 
    PRIVATE EX3
)
