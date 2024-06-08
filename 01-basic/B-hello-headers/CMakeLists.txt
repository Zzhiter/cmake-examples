# Set the minimum version of CMake that can be used
# To find the cmake version run
# $ cmake --version
cmake_minimum_required(VERSION 3.5)

# Set the project name
project (hello_headers)

# Create a sources variable with a link to all cpp files to compile
set(SOURCES
    src/Hello.cpp
    src/main.cpp
)

# Add an executable with the above sources
add_executable(hello_headers ${SOURCES})

# Set the directories that should be included in the build command for this target
# when running g++ these will be included as -I/directory/path/
target_include_directories(hello_headers
    # PRIVATE关键字确保了包含目录的可见性仅限于目标自身及其直接依赖，而不会影响间接依赖。这样可以保持依赖关系的清晰，并防止不必要的头文件暴露。
    PRIVATE 
        ${PROJECT_SOURCE_DIR}/include
)
