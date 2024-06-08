cmake_minimum_required(VERSION 3.5)

# Set the project name
project (third_party_include)


# find a boost install with the libraries filesystem and system
# COMPONENTS - The list of components to find in the library.
# 该函数用于查找并加载Boost库的文件系统和系统组件，要求Boost版本不低于1.46.1，且这两个组件是必需的。
find_package(Boost 1.46.1 REQUIRED COMPONENTS filesystem system)

# check if boost was found
# Most included packages will set a variable XXX_FOUND, 
# which can be used to check if the package is available on the system.
# Boost_FOUND 是由 find_package(Boost ...) 函数执行后设置的CMake变量。
# 如果CMake成功找到了Boost库，它会将此变量设为TRUE；否则，变量保持未定义或设为FALSE。上述代码段检查 Boost_FOUND 的值来确定是否成功找到了Boost库，并根据结果打印相应的消息或终止配置过程。
if(Boost_FOUND)
    message ("boost found")
else()
    message (FATAL_ERROR "Cannot find Boost")
endif()

# Add an executable
add_executable(third_party_include main.cpp)

# link against the boost libraries
target_link_libraries( third_party_include
    PRIVATE
    # Boost::filesystem引用了通过find_package(Boost ...)找到的Boost库的文件系统组件，这是一种现代CMake的导入库语法
        Boost::filesystem
)
