### PROJECT

```
PROJECT(projectname [CXX] [C] [Java])
```
定义工程名称，指定工程支持的语言

隐式定义\<projectname\>\_BINARY\_DIR和\<projectname\>\_SOURCE\_DIR

cmake系统帮助预定义PROJECT\_BINARY\_DIR和PROJECT\_SOURCE\_DIR，值与上面一致

### SET

```
SET(VAR [VALUE] [CACHE TYPE DOCSTRING] [FORCE])
```
显示的定义变量


### MESSAGE

```
MESSAGE([SEND\_ERROR | STATUS | FATAL\_ERROR] "message to display" ...)
```

向终端输出用户定义的信息

 * SEND\_ERROR：产生错误，生成过程被跳过
 * STATUS：输出前缀为-的信息
 * FATAL\_ERROR：立即终止所有cmake过程

### ADD_EXECUTABLE

```
ADD_EXECUTABLE(binName ${SRC_LIST} [file.cpp])
```

生成文件名为binName的可执行文件，源文件是 ${SRC_LIST}定义的源文件列表或多个源文件。

### 基本语法规则

 - 变量使用括弧括起，但是在ID控制语句中直接使用变量名，若赋值间有空格，需用双引号
 - 指令(参数1 参数2 ...)，参数之间使用空格或分号分开
 - 指令是大小写无关的，参数和变量大小写相关
 
 
 ### 清理工程
 
同autotools使用make clean

cmake不支持make distclean


### 内部构建与外部构建

内部构建:
 > 在代码根目录执行`cmake .`命令，生产大量临时文件。

可通过`make VERBOSE=1`或`VERBOSE=1 make`命令查看make构建的详细过程。

外部构建:
 > 通过在源文件夹外创建一个新的用于放置编译中间文件的文件夹，所有生成的工程管理临时文件、编译临时文件、编译最终生成文件都在该文件夹中。

一般创建build目录，然后在build目录下执行`cmake <工程全路径>`，最后运行make构建工程