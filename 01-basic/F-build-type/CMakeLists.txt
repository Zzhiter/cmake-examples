# Set the minimum version of CMake that can be used
# To find the cmake version run
# $ cmake --version
cmake_minimum_required(VERSION 3.5)

# build type（构建类型）在CMake中是一个关键概念，用于定义项目编译时的配置，主要包括优化等级、是否包含调试信息等。不同的构建类型适用于不同的开发阶段和需求：

# Debug：此配置下，编译器不会对代码进行大量优化，便于调试。它会包含完整的调试信息，如变量名、行号等，使得使用调试器时能获得更好的调试体验。
# Release：优化等级高，编译器会进行各种优化以提高程序运行速度和减小二进制文件大小。但一般不包含调试信息，或只有有限的调试信息，适合于最终发布给用户的版本。
# MinSizeRel（Minimum Size Release）：类似Release模式，但更侧重于减小生成的二进制文件大小，可能牺牲一点点运行效率。
# RelWithDebInfo（Release with Debug Information）：结合了Release的优化和Debug的调试信息，使得程序既运行高效又可以用于调试。适用于需要分析运行时性能同时又不希望放弃调试能力的场景。

# Set a default build type if none was specified
if(NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
  message("Setting build type to 'RelWithDebInfo' as none was specified.")
  set(CMAKE_BUILD_TYPE RelWithDebInfo CACHE STRING "Choose the type of build." FORCE)
  # Set the possible values of build type for cmake-gui
  set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS "Debug" "Release"
    "MinSizeRel" "RelWithDebInfo")
endif()

# Set the project name
project (build_type)

# Add an executable
add_executable(cmake_examples_build_type main.cpp)
