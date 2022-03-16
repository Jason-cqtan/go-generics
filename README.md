# go 1.18 泛型

1. 在没有泛型前，同一个功能要支持不同类型传参，得重复写多次


2. 实现泛型，声明函数时，通过声明类型参数(type parameters)；
同时调用函数时，指定泛型函数的类型参数对应的类型实参(type arguments)
```go
// 申明
func SumIntsOrFloats[K comparable, V int64 | float64](m map[K]V) V {
    var s V
    for _, v := range m {
        s += v
    }
    return s
}

// 调用
SumIntsOrFloats[string, int64](ints)
```

3. 声明类型限制，把函数声明类型参数以接口(interface)的形式做定义；Go通常(不是一定)可以根据你的代码推断出类型实参
```go
type Number interface {
	int64 | float64
}

func SumNumbers[K comparable, V Number](m map[K]V) V {
    var s V
    for _, v := range m {
        s += v
    }
    return s
}

SumNumbers(ints)
```