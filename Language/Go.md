## Go

网站：https://golang.google.cn/

GitHub： https://github.com/golang/go

> Go（又称 Golang）是 Google 的 Robert Griesemer，Rob Pike 及 Ken Thompson 开发的一种静态强类型、编译型语言。Go 语言语法与 C 相近，但功能上有：内存安全，GC（垃圾回收），结构形态及 CSP-style 并发计算。
>

### 目录
* 介绍
* [优点和缺点](#优点和缺点)

### 介绍

Go is an open source programming language that makes it easy to build simple, reliable, and efficient software.

1. 下载： Windows 下载 .msi的文件，如go1.13.4.windows-amd64.msi

    地址： https://golang.google.cn/dl/

2. 安装

    安装目录： C:\Go\
    
    Path环境变量： c:\Go\bin （安装的时候自动添加了）
    
    安装测试： 
    ```text
    1. 在工作目录(D:\Projects\GoLandProjects\helloworld)  创建helloworld.go
    2. helloworld.go 内容
    
    package main
    
    import "fmt"
    
    func main() {
       fmt.Println("Hello, World!")
    }
    
    3. 使用 go 命令执行以上代码输出结果如下：
    
    D:\Projects\GoLandProjects\helloworld>go run helloworld.go
    Hello, World!
    ```

### 优点和缺点

优点： 

1. 性能，快，高效。

缺点：

1. 缺少框架
2. 错误处理。通过函数和预期的调用代码简单地返回错误，很容易丢失错误发生的范围