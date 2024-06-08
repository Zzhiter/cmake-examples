cmake_minimum_required(VERSION 3.5)

project(hello_library)

############################################################
# Create a library
############################################################

# Generate the static library from the library sources
add_library(hello_library STATIC 
    src/Hello.cpp
)

# ${PROJECT_SOURCE_DIR}/include目录设置为hello_library库的公共包含目录
# 这意味着：

# 编译库本身：当编译hello_library的源文件时，编译器会查找这个目录。
# 链接到库的目标：任何链接到hello_library的额外目标（如可执行文件）在编译时也会包含这个目录。
# 提示： 
# 对于公共头文件，建议在include目录下使用命名空间子目录，以避免头文件冲突。
# 例如，头文件组织如下：
# #include "static/Hello.h"
# 这样，即使项目中使用了多个库，头文件路径的命名空间也可以帮助减少潜在的命名冲突。
target_include_directories(hello_library
    PUBLIC 
        ${PROJECT_SOURCE_DIR}/include
)


############################################################
# Create an executable
############################################################

# Add an executable with the above sources
add_executable(hello_binary 
    src/main.cpp
)

# link the new hello_library target with the hello_binary target
target_link_libraries( hello_binary
    PRIVATE 
        hello_library
)
