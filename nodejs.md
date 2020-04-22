# Node.js

## package.json 中库的版本号前缀

版本命名规则：MAJOR,MINOR.PATCH

* ^ : 更新到当前 MINOR version 的最新版本

    ^3.3.4 := >=3.3.4 <4.0.0

* ~ : 更新到当前 MAJOR version 的最新版本

    ~1.15.2 :=  >=1.15.2 <1.16.0
