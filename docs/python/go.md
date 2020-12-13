变量声明

var 声明全局变量
`var vname1, vname2, vname3 type`
`var vname1 type = value`

分组声明
```
var (
   ToBe bool = false
   MaxInt uint64     = 1<<64 - 1
	z      complex128 = cmplx.Sqrt(-5 + 12i)
)
```

函数内部的变量可以通过`简洁赋值:=`

```
func main() {
   a, b := 1, 2
}
```

const 声明常量

数据类型

bool 默认值 false
int  默认值 0
string 默认值 ""

类型转换

需要显示转换`T()` eg `unit(f)`

循环

for循环

```go
func main() {
   sum := 0
   for i:=0; i< 10; i++ {
      sum += i
   }
   return sum
}
```

遍历切片或者映射

range形式

当使用 `for` 循环遍历切片时，每次迭代都会返回两个值。第一个值为当前元素的下标，第二个值为该下标所对应元素的一份副本

可以使用`_`来忽略一个值

```go
package main

import 'fmt'

var pow = []int{1,2,4,8,16,32,64,128}

func main() {
	for i, v:= range pow {
    fmt.Printf("2**%d = %d\n", i, v)
	}
  for i, _:= range pow {
    fmt.Printf("2**%d = %d\n", i)
	}
}
```



判断语句

```
func pow(x, n, lim float64) float64 {
   if v < 10 {
      return v
   }
   if v:= math.Pow(x, n); v < lim {
      return v
   } else {
      return n
   }
}
```

```
func main() {
	fmt.Print("Go runs on ")
	switch os := runtime.GOOS; os {
	case "darwin":
		fmt.Println("OS X.")
	case "linux":
		fmt.Println("Linux.")
	default:
		// freebsd, openbsd,
		// plan9, windows...
		fmt.Printf("%s.\n", os)
	}
}
```

defer语句
defer 语句会将函数推迟到外层函数返回之后执行。

推迟调用的函数其参数会立即求值，但直到外层函数返回前该函数都不会被调用。

推迟的函数调用会被压入一个栈中。当外层函数返回时，被推迟的函数会按照后进先出的顺序调用。
```
func main() {
	fmt.Println("counting")

	for i := 0; i < 10; i++ {
		defer fmt.Println(i)
	}

	fmt.Println("done")
}
```

指针

go拥有指针。 指针保存了值的内存地址

类型`*T`是指向T类型值的指针。 其零值为`nil`

`&`操作符会生成一个指向其操作数的指针

```
i := 42
p = &i
```

`*`操作符表示指针指向的底层值

`*p = 21` 可以通过指针p来设置i

`struct` 结构体 （一组字段）

```
type Vertex struct {
	X int
	Y int
}

func main() {
	fmt.Println(Vertext{1, 2})
}
```

结构体字段通过点号来访问

```
func main() {
	v := Vertext{1, 2}
	v.X = 4
	fmt.Println(v.X)
}
```

数组

类型`[n]T`表示拥有n个T类型的值的数组

`var a [10] int`

切片

`a[low:high]`

`a := make([]int, 5)`

切片并不存储任何数据，它只是描述了底层数组中的一段。

更改切片的元素会修改其底层数组中对应的元素

切片的默认行为:

1. 下界为0
2. 上界为该切片的长度

长度：包含的元素个 数 `len(s)`

容量：从第一个元素开始数, 到底层数组元素末尾的个数 `cap(s)`

`append(s []T, T)` 为切片追加新的元素

+ 第一个参数s是一个元素类型为T的切片, 其余类型为T的值将会追加到该切片的末尾
+ 返回一个包含原切片所有元素加上新添加元素的切片

```go
package main

import 'fmt'

func main() {
  primes := [6]int{2,3,5,7,11,13}
  var s []int = primes[1:4]
  fmt.Println(s)
  
  // append切片
  var n []int
  printSlice(n)
  
  n = append(n, 1)
  printSlice(n)
  
  n = append(n, 2,3,4)
  printSlice(n)
}

func printSlice(s []int) {
	fmt.Printf("len=%d cap=%d %v\n", len(s), cap(s), s)
}
```

