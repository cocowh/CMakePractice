# 绝对路径引入
#include_directories(/usr/local/include/hello)
# 通过设置系统环境变量export CMAKE_INCLUDE_PATH=/usr/local/include/hello
find_path(myHeader hello.h)
if (myHeader)
    include_directories(${myHeader})
endif (myHeader)

add_executable(main main.cpp)

# 链接接静态库 没安装到系统默认头文件搜索路径和默认库路径，需用绝对路径
#target_link_libraries(main /usr/local/lib/libhello.a)

# 链接动态库 没安装到系统默认头文件搜索路径和默认库路径，需用绝对路径
#target_link_libraries(main /usr/local/lib/libhello.dylib)

# 通过设置系统环境变量export CMAKE_LIBRARY_PATH=/usr/local/lib
find_library(myLib libhello.a)
if (myLib)
    target_link_libraries(main ${myLib})
endif (myLib)
