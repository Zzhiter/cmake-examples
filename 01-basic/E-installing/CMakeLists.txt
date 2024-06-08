cmake_minimum_required(VERSION 3.5)

project(cmake_examples_install)

############################################################
# Create a library
############################################################

#Generate the shared library from the library sources
add_library(cmake_examples_inst SHARED
    src/Hello.cpp
)

target_include_directories(cmake_examples_inst
    PUBLIC 
        ${PROJECT_SOURCE_DIR}/include
)

############################################################
# Create an executable
############################################################

# Add an executable with the above sources
add_executable(cmake_examples_inst_bin
    src/main.cpp
)

# link the new hello_library target with the hello_binary target
target_link_libraries( cmake_examples_inst_bin
    PRIVATE 
        cmake_examples_inst
)

############################################################
# Install
############################################################

# Binaries
install (TARGETS cmake_examples_inst_bin
    DESTINATION bin)

# Library
# Note: may not work on windows
install (TARGETS cmake_examples_inst
    LIBRARY DESTINATION lib)

# Header files
# 这行命令告诉CMake将${PROJECT_SOURCE_DIR}/include/目录下的所有文件和子目录安装到目标系统的include目录下。
# ${PROJECT_SOURCE_DIR}是一个CMake变量，代表项目源代码的根目录。这样做的目的是使得在系统中安装项目后，其他项目可以通过标准的#include语句找到并使用这个项目提供的头文件。
install(DIRECTORY ${PROJECT_SOURCE_DIR}/include/ 
    DESTINATION include)

# Config
# 这条命令安装单个文件cmake-examples.conf到目标系统的etc目录。在Unix-like系统中，etc目录通常用于存放配置文件。、
# 这意味着在安装完成后，cmake-examples.conf将作为配置文件可供用户或系统使用。
install (FILES cmake-examples.conf
    DESTINATION etc)
