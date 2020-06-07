# perf

## perf 配合 FlameGraph 生成火焰图

1. 记录进程调用栈

    ```bash
    perf record -F 99 -p <pid> -g -- sleep 30
    ```

    * `-F 99`: 每秒 99 次
    * `-p <pid>`: 进程号
    * `-g`: 记录调用栈
    * `sleep 30`: 持续 30 秒
2. 读取 perf.data 并将记录的调用栈写入 out.perf

    ```bash
    perf script -i perf.data > out.perf
    ```

3. 转化 out.perf 为火焰图

    ```bash
    cat out.perf | ./stackcollapse-perf.pl --all | ./flamegraph.pl --hash > example-perf.svg
    ```

## 实时查看性能统计数据

```bash
sudo perf top -p <pid>
```

这里一定要用加 sudo 用 root 身份运行
