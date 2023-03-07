##1.Standard
- `make` automatically finding Makefile | use `make -f {Pointing file}`
- ```make
    Target : Reliance
    [tab] command
    ```
##2.Grammer
```make
CXX = g++
TARGET = hello
OBJ = main.o factorial.o printhello.o
CXXFLAG = -c -Wall
...
```
当Makefile有多个生成目标
  1. 默认寻找第一个目标
  2. 寻找第一个目标需要的依赖
  3. 生成依赖
  4. 完成第一个目标
可指定目标`make xxx`
- 快捷方式
  - `$@` -- Target 
  - $^ -- All of the Reliance
  - $< -- The first of Reliance
  - %.o : %.cpp -- 全局适用


- .PHONY: clean
  - 当clean文件存在时 若不加会导致`make clean` 无法执行
  - .PHONY 将 clean 文件忽略， 直接执行clean命令

##More Convenient
```make
SRC = $(wildcard %.cpp)
OBJ = $(patsubst#路径替换 %.cpp, %.o, $(SRC))
```
- wildcard : 通配符展开
  - `$(wildcard PATTERN)`
- patsubst : 将C中的a类型文件替换成b类型文件
  - `$(patsubst a, b, $C)`