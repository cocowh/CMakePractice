### ADD_SUBDIRECTORY

```
ADD_SUBDIRECTORY(source\_dir [binary\_dir] [EXCLUDE\_FROM\_ALL])
```

向当前工程添加存放源文件的子目录，并可以指定中间二进制和目标二进制存放的为止。

`EXCLUDE\_FROM\_ALL`参数用于将这个目录从编译过程中排除，比如，工程的example，可能需要工程构建完成后再进入example目录单独进行构建。

### SUBDIRS

```
SUBDIRS(dir1 dir2 ...)
```
一次添加多个子目录，即使外部编译，子目录体系仍然被保存，已不推荐使用。

### EXECUTABLE\_OUTPUT\_PATH和LIBRARY\_OUTPUT\_PATH

EXECUTABLE\_OUTPUT\_PATH：可执行二进制的输出路径

LIBRARY\_OUTPUT\_PATH：库的输出路径

可通过SET指令重新定义

### INSTALL和CMAKE\_INSTALL\_PREFIX

INSTALL：定义安装规则，安装的内容可以包括二进制、动态库、静态库以及文件、目录、脚本等

CMAKE\_INSTALL\_PREFIX：类似于configure脚本的-prefix

常见的使用方法`cmake -DCMAKE_INSTALL_PREFIX=/usr .`

若没指定CMAKE\_INSTALL\_PREFIX，默认定义是/usr/local

#### INSTALL目标文件的安装

```
INSTALL(TARGETS targets ...  
    [[ARCHIVE|LIBRARY|RUNTIME]  
        [DESTINATION <dir>]  
        [PERMISSIONS permissions...]  
        [CONFIGURATIONS [Debug|Release|...]]  
        [COMPONENT <component>]  
        [OPTIONAL]  
    ] [...])
```
TARGETS后面跟通过`ADD\_EXECUTABLE`或者`ADD\_LIBRARY`定义的目标文件，可能是可执行二进制、动态库、静态库。

目标类型：ARCHIVE指静态库、LIBRARY指动态库、RUNTIME指可执行目标二进制

DESTINATION定义安装的路径，若以/开头则是绝对路径，`CMAKE_INSTALL_PREFIX`无效，否则安装路径是${CMAKE\_INSTALL\_PREFIX}/<DESTINATION定义的路径>

example：

```example
INSTALL(TARGETS myrun mylib mystaticlib
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION libstatic
)
```
#### INSTALL普通文件的安装

```
INSTALL(FILES files... DESTINATION <dir>
    [PERMISSIONS permissions...]
    [CONFIGURATIONS [Debug|Release|...]]
    [COMPONENT <component>]
    [RENAME <name>] [OPTIONAL])
```

用于安装一般的文件，并可以指定访问权限，文件名是此指令所在路径下的相对路径。

若不定义权限PERMISSIONS，安装后的权限为：OWNER_WRITE，OWNER_READ，GROUP_READ和WORLD_READ，即644权限。


#### INSTALL非目标文件的可执行程序安装(如脚本)

```
INSTALL(PROGTAMS files... DESTINATION <dir>
    [PERMISSIONS permissions...]
    [CONFIGURATIONS [Debug|Release|...]]
    [COMPONENT <component>]
    [RENAME <name>] [OPTIONAL])
```

若不定义权限PERMISSIONS，安装后权限为：OWNER_EXECUTE，GROUP_EXECUTE和WORLD_EXECUTE
，即755权限。

#### INSTALL目录的安装

```
INSTALL(DIRECTORY dires... DESTINATION <dir>
    [FILE_PERMISSIONS permissions...]
    [USE_SOURCE_PERMISSIONS]
    [CONFIGURATIONS [Debug|Release...]]
    [COMPONENT <component>]
    [[PATTERN <pattern> | REGEX <regex>] [EXCLUDE] [PERMISSIONS permissions ...]]
    [...])
```

DIRECTORY：所在Source目录的相对路径，以abc/和abc结尾有不同，若以abc结尾则目录被安装为目标路径下的abc，若以abc/结尾则代表将这个目录中的内容安装到目标路径，但不包括这个目录本身。

PATTERN：用于使用正则表达式进行过滤

PERMISSIONS：用于指定PATTERN过滤后的文件权限。

example:

```
INSTALL(DIRECTORY icons scripts/ DESTINATION share/myproj
    PATTERN "CVS" EXCLUDE
    PATTERN "scripts/*"
    PERMISSIONS OWNER_EXECUTER OWNER_WRITE OWNER_REASD GROUP_EXECUTE GROUP_READ)
```
将icons目录安装<prefix>/share/myproj，将scripts/中的内容安装到<prefix>/share/myproj

不包含目录名为CVS的目录，对于scripts/*文件指定权限为OWNER_EXECUTER OWNER_WRITE OWNER_REASD GROUP_EXECUTE GROUP_READ

#### 安装时CMAKE脚本的执行

```
INSTALL([[SCRIPT <file>] [CODE <code>]] [...])
```

SCRIPT：在安装时调用cmake脚本文件(即<abc>.cmake文件)

CODE：执行CMAKE指令，必须以双引号括起来。

example：`INSTALL(CODE "MESSAGE("Sample install message.")")`


#### INSTALL_FILES

过时安装指令