### INCLUDE_DIRECTORIES

```
INCLUDE_DIRECTORIES([AFTER|BEFORE] [SYSTEM] dir1 dir2 ...)
```
向工程添加多个特定的头文件搜索路径，路径之间用空格分割，若路径包含空格，可以使用双引号括起来，默认的行为是追加到当前的头文件搜多路径的后面，可以通过来年各种功能方式来进行控制搜素路径天际的方式：

 - CMAKE_INCLUDE_DIRECTORIES_BEFORE，通过SET这个cmake变量为on，可以将添加的头文件搜索路径放在已有路径的前面
 - 通过AFTER或者BEFORE参数，控制是追加还是置前
 
 ### LINK_DIRECTORIES
 
```
LINK_DIRECTORIES(directory1 directory2 ...)
```
添加非标准的共享库搜索路径，若在工程内部同时存在共享库和可执行二进制，在编译时需要指定一下这些共享库的路径。

### TARGET_LINK_LIBRARIES

```
TARGET_LINK_LIBRARIES(target library1 <debug | optimized> library2 ...)
```
为target添加需要连接的共享库。

### CMAKE\_INCLUDE\_PATH和CMAKE\_LIBRARY\_PATH

用于解决autotools工程中--extra-include-dir等参数的支持，若头文件没有存放在常规路径（/usr/include，/usr/local/include等），可通过这些变量弥补。

使系统环境变量而不是cmake变量，要在bash中用export或者csh中使用set命令设置或者
`CMAKE_INCLUDE_PATH=/home/include cmake ..`等方式

CMAKE\_INCLUDE\_PATH用在FIND_PATH中，CMAKE\_LIBRARY\_PATH用在FIND\_LIBRARY中

### FIND\_PATH和FIND\_LIBRARY

```
FIND_FILE(<VAR> name1 path1 path2 ...)
```

在指定的路径中搜索文件名。

```
FIND_LIBRARY(<VAR> name1 path1 path2 ...)
```
在指定的路径中搜索库。