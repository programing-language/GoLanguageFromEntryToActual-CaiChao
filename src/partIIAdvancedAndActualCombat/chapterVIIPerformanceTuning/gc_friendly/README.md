# GC 友好的代码
## 避免内存分配和复制
• 复杂对象尽量传递引⽤
  • 数组的传递
  • 结构体传递
### 打开 GC ⽇志
只要在程序执⾏之前加上环境变量 GODEBUG=gctrace=1
```
GODEBUG=gctrace=1 go test -bench=.
GODEBUG=gctrace=1 go run main.go
```
⽇志详细信息参考： https://godoc.org/runtime
### go tool trace
#### 普通程序输出 trace 信息
```
package main
import (
"os"
"runtime/trace"
)
func main() {
f, err := os.Create("trace.out")
if err != nil {
 panic(err)
}
defer f.Close()
err = trace.Start(f)
 if err != nil {
panic(err)
}
defer trace.Stop()
// Your program here
}
```
#### 测试程序输出 trace 信息
```
go test -trace trace.out
```
#### 可视化 trace 信息
```
go tool trace trace.out
```
## 避免内存分配和复制
• 初始化⾄合适的⼤⼩
  • ⾃动扩容是有代价的
• 复⽤内存
