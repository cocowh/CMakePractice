cmake_minimum_required(VERSION 3.17)

project(NEWHELLO)

add_subdirectory(src)

ADD_TEST(mytest ${PROJECT_BINARY_DIR}/bin/main)

ENABLE_TESTING()