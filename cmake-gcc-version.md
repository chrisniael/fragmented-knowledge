# CMake 指定使用的 Gcc 版本

1. 使用环境变量

```bash
CC=/usr/local/bin/gcc-7 CXX=/usr/local/bin/g++-7 cmake path/to/your/source
```

2. 使用 CMake -D

```bash
cmake -D CMAKE_C_COMPILER=/usr/local/bin/gcc-7 -D CMAKE_CXX_COMPILER=/usr/local/bin/g++-7 path/to/your/source
```

3. 使用 set() (不推荐)

```cmake
set(CMAKE_C_COMPILER /usr/local/bin/gcc-7)
set(CMAKE_CXX_COMPILER /usr/local/bin/g++-7)
project("YourProjectName")
```
