### ADD\_LIBRARY

```
ADD_LIBRARY(libname [SHARED|STATIC|MODULE]
    [EXCLUDE_FROM_ALL]
        source1 source2 ... sourceN)
```
不需要写全libhello.so，只需要填写hello即可，cmake系统会自动生成libhello.x

类型：

 - SHARED：动态库
 - STATIC：静态库
 - MODULE：在使用dyld的系统有效，若不支持dyld，则被当作SHARED对待
 
EXCLUDE_FROM_ALL：标识此库不会被默认构建，除非有其他的组件依赖或者手工构建

> 不可通过此命令创建同名静态库和动态库

### SET\_TARGET\_PROPERTIES

```
SET_TARGET_PROPERTIES(target1 target2 ...
    PROPERTIES prop1 value1 prop2 values ...)
```

设置目标的属性，对于动态库可用来指定动态库版本和API版本

### GET\_TARGET\_PROPERTY

```
GET_TARGET_PROPERTY(VAR target property)
```

从一个目标中获取一个属性值，若没有这个属性定义，则返回NOTFOUND。