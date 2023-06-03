---
layout: post
title:  easyGin 开源心得
date:   2019-07-30
categories: go
---
自上次在v2ex发了一篇，关于我对从php转go的心得，发了自己的开源(https://github.com/xiangdong1987/easyGin)[https://github.com/xiangdong1987/easyGin]感觉反响挺大，被骂的挺惨的，不过我也从中学习了很多东西。今天来总结一下，顺便看看大家还有没有新的意见和建议。

## Go mod
* 官方支持的包管理工具自，从golang 1.11 新加的特性
* 好处：go run 时自动引入依赖包  存储在 $GOPATH/src/pkg 目录
* 使用方式：
    * 更新到新版go
    * 设置如下配置
    
    ```
    //开启mod
    export GO111MODULE=on
    
    //设置代理
    export GOPROXY=https://gocenter.io
    ```
    
> 只能说谁用谁知道

## Go template 
* 提供了模板渲染 方便灵活
* 使用方式

```
type CurdTemplate struct {
	LowerName  string
}
routerTemplate=`lower:{{.LowerName}}`
t := template.New("router")
curdStrut := CurdTemplate{strings.ToLower("Person")}
//解析内容到模板
t, err = t.Parse(routerTemplate)
if err != nil {
    log.Fatal("Parse:", err)
}
//将数据用到模板中
buf := new(bytes.Buffer)
if err = t.Execute(buf, curdStrut); err != nil {
    log.Fatal("Execute:", err)   
} else {
    result = buf.String()
}
fmt.Println(result)
```

## Go convey代码测试及代码覆盖
* 这个库提供了代码测试的重新封装，使用友好，还可以提供页面展示代码覆盖率自动测试功能。程序规范化典范（感觉又要挨骂了）

```go
func TestInitRouter(t *testing.T) {
	Convey("model 路由", t, func() {
		InitDB("company")
		err := InitRouter("Person", "D:/data/go/src/easyGin/router/")
		Convey("model 生成", func() {
			So(err, ShouldEqual, nil)
		})
	})
}
```

## 性能测试
* 使用ab进行测试，毕竟我们是api接口
* 测试环境：
    * 虚拟机 2G 内存 单核  
    * 数据库 测试环境单机
    * 量100 并发 10000 请求
* 测试结果：
![测试结果](https://github.com/xiangdong1987/easyGin/raw/master/static/ab.png)    
## 总结
我觉得大家的批评都挺好的，指出了我的不足，然后让我不断进步，感觉这就是开源的乐趣吧！希望各位大神多给点意见，不吝赐教。还有最好有人能提pr大家一起维护，做一个有用的工具而不是玩具。在这在募集一波大神。    
