---
layout: post
title: 'cannot assign to struct field *.* in map'
date: 2019-04-17
author: CodeNerull
tags: go 踩坑
categories: golang踩坑笔记
---

`go`语言代码:

```go
package main

import "fmt"

func main() {
    type User struct {
        Id   int
        Name string
    }

    UserList := make(map[int]User)
    UserList[1] = User{1, "小明"}
    fmt.Printf("UserList value:%+v\n", UserList[1])

    UserList[1].Name = "张小明"
    fmt.Printf("UserList value:%+v\n", UserList[1])
}
```

运行返回`cannot assign to struct field UserList[1].Name in map`错误。

---

#### 解决方案
将`User`变量的地址赋值给`Map`

代码示例:

```go
package main

import "fmt"

func main() {
    type User struct {
        Id   int
        Name string
    }

    UserList := make(map[int]*User)
    UserList[1] = &User{1, "小明"}
    fmt.Printf("UserList value:%+v\n", UserList[1])

    UserList[1].Name = "张小明"
    fmt.Printf("UserList value:%+v\n", UserList[1])
}
```

运行返回:

```bash
UserList value:&{Id:1 Name:小明}
UserList value:&{Id:1 Name:张小明}
```

