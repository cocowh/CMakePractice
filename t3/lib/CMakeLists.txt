set(LIBHELLO_SRC hello.cpp)

# 添加共享库（动态库）
add_library(hello SHARED ${LIBHELLO_SRC})
# 指定共享库的生成位置
#set(LIBRARY_OUTPUT_PATH libhello)

# 添加静态库
add_library(hello_static STATIC ${LIBHELLO_SRC})

# 修改静态库名称
set_target_properties(hello_static PROPERTIES OUTPUT_NAME "hello")
# 获取静态库的名称属性
get_target_property(OUTPUT_VALUE hello_static OUTPUT_NAME)
message(STATUS "This is the hello_static OUTPUT_NAME:" ${OUTPUT_VALUE})

#
set_target_properties(hello PROPERTIES CLEAN_DIRECT_OUTPUT 1)
set_target_properties(hello_static PROPERTIES CLEAN_DIRECT_OUTPUT 1)

# 动态库版本号  VERSION指代动态库版本，SOVERSION指代API版本
set_target_properties(hello PROPERTIES VERSION 1.2 SOVERSION 1)


# 安装路径
install(TARGETS hello hello_static
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib
        )

install(FILES hello.h DESTINATION include/hello)

