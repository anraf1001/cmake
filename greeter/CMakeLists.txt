cmake_minimum_required(VERSION 3.10)
project(greeter VERSION 1.0)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(FLAGS -Wall -Wextra -Werror -Wconversion -pedantic -O3)

add_library(${PROJECT_NAME}-lib STATIC greeter.cpp person.cpp)

add_executable(${PROJECT_NAME} main.cpp)
add_executable(${PROJECT_NAME}-ut test/greeter.ut.cpp)
target_compile_options(${PROJECT_NAME} PRIVATE ${FLAGS})
target_compile_options(${PROJECT_NAME}-ut PRIVATE ${FLAGS})
target_compile_options(${PROJECT_NAME}-lib PRIVATE ${FLAGS})

target_link_libraries(${PROJECT_NAME} ${PROJECT_NAME}-lib)
target_link_libraries(${PROJECT_NAME}-ut ${PROJECT_NAME}-lib)

enable_testing()
add_test(NAME someTest COMMAND ${PROJECT_NAME}-ut)
