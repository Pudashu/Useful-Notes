# Cmake

```cmake
CMAKE_MINIMUM_REQUIRED(VERSION 3.16)

PROJECT(PROJECTNAME)
#SETTING
SET()

#
ADD_EXECUTABLE(project_name file)
```
## SET
SET(VAR [value] [cache type doc string [force]] )

## Environmental Path
$CMAKE_BINARY_DIR  #Compiling directory
$CMAKE_SOURCE_DIR  #Source
$CMAKE_CURRENT_BINARY_DIR #SubCompiling directory
$CMAKE_CURRENT_SOURCE_DIR #Sub Program's source dir
$EXECUTABLE_OUTPUT_PATH
$PROJECT_NAME # def by PROJECT

## Command
```cmake
  # 第一条
CMAKE_MINIMUM_REQUIRED(VERSION xxx)
  # 处理获取源文件
$AUX_SOURCE_DIRECTORY(dir VAR)
  # 生成可执行文件
ADD_EXECUTABLE(<name> [src])
  # 添加子目录
$ADD_SUBDIRECTORY(Dir)


# 构建库
$ADD_LIBRARY(库名 [STATIC|SHARED|MODULE] 所有需要的文件) # 通常用$AUX_SOURCE_DIRECTORY 获取变量
# 链接库
$TARGET_LINK_LIBRARIES(exec libraries)#将项目生成的可执行程序与库链接


# 增加编译依赖
ADD_DEPENDENCIES(target-name depend-target1 ...) depended targets should be compiled first
# 增加编译选项
ADD_DEFINITIONS(-Dxxx) 定义宏
# 对库的编译
ADD_LIBRARIES(<name> [STATIC|SHARED|MODULE] [source1][source2]...)


# 对程序进行测试 Test
ENABLE_TESTING()
ADD_TEST(testname Exename arg1...)


# 在编译中执行命令，并不在makefile中执行
EXEC_PROGRAM(Executable [directory in which to run]
                [ARGS <arguments to executable>]
                [OUTPUT_VARIABLE <var>]
                [RETURN_VALUE <var>])
# 用于在指定的目录运行某个程序,通过 ARGS 添加参数,如果要获取输出和返回值,可通过OUTPUT_VARIABLE 和 RETURN_VALUE 分别定义两个变量.
# 这个指令可以帮助你在 CMakeLists.txt 处理过程中支持任何命令,比如根据系统情况去修改代码文件等等。

# 对文件进行操作
FILE()

# 对目标文件的信息处理 [Detailed / Elaborated information](https://zhuanlan.zhihu.com/p/82244559)
INCLUDE_DIRECTORIES([AFTER|BEFORE] dir1,dir2...) 
# 将指定目录添加到编译器的头文件搜索路径之下，指定的目录被解释成当前源码路径的相对路径。
# 每次调用include_directories命令时使用AFTER或BEFORE选项来指定是将目录添加到列表的前面或者后面
不如直接使用TARGET_INCLUDE_DIRECTORIES
LINK_LIBRARIES 


TARGET_INCLUDE_DIRECTORIES(<target> [SYSTEM] [AFTER|BEFORE]
  <INTERFACE|PUBLIC|PRIVATE> [items1...]
  [<INTERFACE|PUBLIC|PRIVATE> [items2...] ...])
Specifies include directories to use when compiling a given target.
The named <target> must have been created by a command such as add_executable() or add_library() and must not be an ALIAS target.
指定目标包含的头文件路径 / 必须在target被构建后
By using AFTER or BEFORE explicitly, you can select between appending and prepending, independent of the default.

TARGET_LINK_LIBRARIES()：指定目标链接的库
The INTERFACE, PUBLIC and PRIVATE keywords are required to specify the scope of the following arguments.

PRIVATE 是在对外头文件中没有引用库而只在新建库内的.c or .cxx 文件中引用库的
INTERFACE 是对外头文件引用而.c不引用
PUBLIC = PRIVATE+INTERFACE
E.G.: 
TARGET_LINK_LIBRARIES(lib-helloworld [PRIVATE|INTERFACE|PUBLIC] hello) 
TARGET_INCLUDE_DIRECTORIES(lib-helloworld [PRIVATE|INTERFACE|PUBLIC] hello)

# 查找外部库 和外部包
FIND_LIBRARY(<VAR> name|NAMES name1 name2... [path1 path2]) # name 可用库全称，去除lib和后缀...
如果找到库，<VAR>获得正常库值 没有 则赋值<VAR>-NOTFOUND 在第一次赋值完VAR非空后，就不会再更改

FIND_PACKAGE
```

 # 库的搜索路径
