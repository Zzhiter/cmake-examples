cmake_minimum_required(VERSION 3.5)

# Set the project name
project (cf_example)

# set a project version
set (cf_example_VERSION_MAJOR 0)
set (cf_example_VERSION_MINOR 2)
set (cf_example_VERSION_PATCH 1)
set (cf_example_VERSION "${cf_example_VERSION_MAJOR}.${cf_example_VERSION_MINOR}.${cf_example_VERSION_PATCH}")

# configure_file 是CMake中的一个功能，用于对模板文件进行变量替换并生成最终的文件。
# 这个过程对于想要根据CMake配置动态生成源代码、配置文件等非常有用。您给出的两个例子展示了如何使用configure_file命令进行变量替换。

# Call configure files on ver.h.in to set the version.
# Uses the standard ${VARIABLE} syntax in the file
# 作用： 将ver.h.in模板文件中的CMake变量（使用${}语法或@@转义@符号）替换为实际值，然后生成ver.h文件到项目的二进制输出目录(${PROJECT_BINARY_DIR})中。
# 模板文件使用： 在ver.h.in中，你可以这样定义变量引用：const char* ver = "${cf_example_VERSION}";。CMake会用cf_example_VERSION变量的实际值（在此项目中为项目版本号）替换${cf_example_VERSION}。
configure_file(ver.h.in ${PROJECT_BINARY_DIR}/ver.h)

# configure the path.h.in file.
# This file can only use the @VARIABLE@ syntax in the file
# 作用： 类似于第一个例子，但是由于使用了@ONLY选项，这意味着在模板文件中只能使用@@（双at符号）包围变量名来进行引用，不允许使用${}形式。这样做后，CMake会忽略所有其他的${}风格变量替换规则，仅替换明确用@@标记的变量。
# 模板文件使用： 在这种情况下，如果你希望包含CMake的变量，如源码目录路径，你应这样编写path.h.in：const char* path = "@CMAKE_SOURCE_DIR@";。生成的path.h文件中的文本将是CMAKE_SOURCE_DIR变量的实际值，即项目源码的顶层目录路径。
configure_file(path.h.in ${PROJECT_BINARY_DIR}/path.h @ONLY)

# Add an executable
add_executable(cf_example
    main.cpp
)

# include the directory with the new files
target_include_directories( cf_example
    PUBLIC
        ${CMAKE_BINARY_DIR}
)
