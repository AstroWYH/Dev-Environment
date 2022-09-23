# Win平台CMake+Mingw踩坑

```cmake
cmake_minimum_required(VERSION 3.10)

# 这两行没必要，用cmake -G "MinGW Makefiles"就行
# set(CMAKE_C_COMPILER "/d/mingw64/bin/gcc.exe")
# set(CMAKE_CXX_COMPILER "/d/mingw64/bin/g++.exe")

project(DUCK)

include_directories(${CMAKE_SOURCE_DIR}/duck/)
include_directories(${CMAKE_SOURCE_DIR}/behavior/)

set(MAIN_DIR ${CMAKE_SOURCE_DIR})
set(DUCK_DIR ${CMAKE_SOURCE_DIR}/duck)
set(BEHAVIOR_DIR ${CMAKE_SOURCE_DIR}/behavior)

set(SRC_LIST
    ${MAIN_DIR}/main.cpp
    ${DUCK_DIR}/Duck.cpp
    ${DUCK_DIR}/MallardDuck.cpp
    ${BEHAVIOR_DIR}/FlyNoWay.cpp
    ${BEHAVIOR_DIR}/FlyWithWings.cpp
    ${BEHAVIOR_DIR}/QuackMute.cpp
    ${BEHAVIOR_DIR}/QuackSqueak.cpp)

add_executable(main ${SRC_LIST})

# 需要下载win下mingw64，cmake，并分别配置到环境变量
# cmake ..:cmake -G "MinGW Makefiles" .. 设置为mingw的方式。如果使用vs的话，应指定为“NMake Makefiles”
# mingw32-make.exe备份，拷贝为make.exe
# git bash环境确保可正常调用：cmake gcc g++ make等
# make：mingw32-make
```

