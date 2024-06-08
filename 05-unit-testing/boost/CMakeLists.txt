cmake_minimum_required(VERSION 3.5)

# Set the project name
project (boost_unit_test)


# find a boost install with the libraries unit_test_framework
find_package(Boost 1.46.1 REQUIRED COMPONENTS unit_test_framework)

# Add an library for the example classes
add_library(example_boost_unit_test
    Reverse.cpp
    Palindrome.cpp
)

target_include_directories(example_boost_unit_test
    PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}
)

target_link_libraries(example_boost_unit_test
    PUBLIC
        Boost::boost
)

#############################################
# Unit tests

# enable CTest testing
enable_testing()

# Add a testing executable
add_executable(unit_tests unit_tests.cpp)

target_link_libraries(unit_tests
    example_boost_unit_test
    Boost::unit_test_framework
)

# 为unit_tests目标添加编译定义BOOST_TEST_DYN_LINK。这个定义告诉Boost单元测试框架使用动态链接库。
target_compile_definitions(unit_tests
    PRIVATE
        BOOST_TEST_DYN_LINK
)

# test_all是在CTest中定义的一个测试用例名称。
# 通过add_test命令，它与unit_tests可执行文件关联。这意味着当你运行CTest时，可以通过调用test_all来执行unit_tests这个可执行文件，进而运行其中包含的所有单元测试。简而言之，test_all是一个方便的入口，用于启动项目中的全部单元测试。
add_test(test_all unit_tests)
