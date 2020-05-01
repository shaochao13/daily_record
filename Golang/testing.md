#### 覆盖率
1. 查看测试代码的覆盖率：`go test -cover`
2. 将覆盖率的日志文件输出到文件：`go test -cover -coverprofile=c.out`
3. 以html方式打开生成的覆盖率文件：`go tool cover -html=c.out`

### 单元测试

```go
//方法名以Test开头，参数必须为*testing.T
func TestSplit(t *testing.T){
    //填写测试代码
}
```

### 基准测试 (BenchmarkXxx)

```go
// 方法名以Benchmark开头，参数为*testing.B
func BenchmarkSplit(b *testing.B){
    //填写测试代码
}
```