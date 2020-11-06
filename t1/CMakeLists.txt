project(HELLO)

set(SRC_LIST main.cpp)

message(STATUS "This is BINARY dir " ${HELLO_BINARY_DIR})
message(STATUS "This is SOURCE dir " ${HELLO_SOURCE_DIR})

# 官方这一行有误 为引用变量
add_executable(hello ${SRC_LIST})

