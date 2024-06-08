# Set the project name
project (sublibrary1)

# Add a library with the above sources
add_library(${PROJECT_NAME} src/sublib1.cpp)
# 在这里给这个模块起了个别名，方便引用
add_library(sub::lib1 ALIAS ${PROJECT_NAME})

target_include_directories( ${PROJECT_NAME}
    PUBLIC ${PROJECT_SOURCE_DIR}/include
)
