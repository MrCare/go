## 我们在数据库操作的时候，比如 dao 层中当遇到一个 sql.ErrNoRows 的时候，是否应该 Wrap 这个 error，抛给上层。为什么，应该怎么做请写出代码？

需要包装 error，再抛给上层，有如下原因：
1. `sql.ErrNoRows` 并不会对具体产生错误的代码上下文作出说明，包装后有助于上层做更高级的处理。

dao:
```go
return errors.Wrapf(code.NotFound, fmt.Sprintf("sql: %s error: %v", sql, err))
```
biz:
```go
if errors.Is(err, code.NotFound} {

}
```
