typescript

### 定义

TS更能适应项目规模不断扩大的场景，一个更强大的生产工具。

TS拥有自身编译器, 可使用最新的js特性，类似babel，由于TS带来类型, 所以IDE可以更好的理解你的代码。

特征

+ 性能安全
+ 完善的工具链
+ 下一代js特性
+ 

### 配置

`compilerOptions`

定义编译选项

+ `target: 'es5'` 制定ECMAScript目标版本 es5 | es3
+  `module: []` 指定使用模块 
+  `lib: []` 指定要包含在编译中的库文件，
+  `allowJs: true` 允许编译js文件

`include:[]` 指定需要包含的文件

`exclude: []` 指定需要排除的文件



### 声明空间

#### 类型声明空间

包含用来当作类型注解的内容

比如 `class` `interface` `type`

#### 变量声明空间

包含可用作变量的内容



### 模块

全局模块

通过declare来声明一个全局模块

`declare var` 声明全局变量

`declare function` 声明全局方法

`declare class` 声明全局枚举类型

`declare enum`  声明全局枚举类型

`declare namespace`  声明（含有子属性的）全局对象

`declare module` 扩展模块

`declare global` 扩展全局变量

`interface` 声明全局类型

`type`  声明全局类型

文件模块

包含import或者export， 会在这个文件中创建一个本地的作用域

通过使用`namespace`来确保创建的变量不会泄露至全局命名空间



#### 注解

基本注解

+ `number`
+ `string`
+ `boolean`
+ `<T>[]`

##### 接口interface

接口可以合并多个类型声明至一个类型声明

```typescript
interface Name {
	first: string,
	age: number
}
```



##### 内联类型注解

```typescript
let name: {
	first: string,
	age: number
}
```



##### 特殊类型

+ `any`
+ `null`
+ `undefined`
+ `void` 表示函数没有一个返回值



##### T 泛型

根据传入的类型来决定T的类型



##### 联合类型

通过|来声明联合类型, 也就是可以是多种类型

```typescript
function formatCommandline(command: string[] | string) {

}
```



##### 元祖类型

通过使用`[type1, type2]`来为元组添加类型注解

```typescript
let nameNumber: [string, number];
```



##### 类型别名

通过type 来为类型注解设置别名

```typescript
type StrOrNum = string | number

let sample: StrOrNum;
```



类实现接口

类通过implements来使用定义好的数据结构

```
interface Point {
	x: number,
	y: number,
	z: number
}

class MyPoint implements Point {
	x: number,
	y: number,
	// Error missing member z
}
```



枚举

枚举是组织收集有关联变量的一种方式, 通过enum来定义

```
enum Job {
	Jianshi,
	Dunpai
}

let Jobs = Job.Jianshi


```



#### 类型断言

覆盖TS的类型推断, 并且它不会发生错误

使用

```typescript
INTERFACE Foo {
	bar: number;
	bas: string;
}

const foo = {} as Foo;
foo.bar = 123;
foo.bas = 'hello';
```



#### 操作符

关于typeof 和 instanceof

在条件块使用时，TS会推导出在条件块中的变量类型

```typescript
function doSome(x: number | string) {
	if(typeof x === 'string') {
		console.log(x.subtr(1));
		console.log(x.substr(1));
	}
}
```



通过if来推导else

```typescript
class Foo {
  foo = 123;
}

class Bar {
  bar = 123;
}

function doStuff(arg: Foo | Bar) {
  if (arg instanceof Foo) {
    console.log(arg.foo); // ok
    console.log(arg.bar); // Error
  } else {
    // 这个块中，一定是 'Bar'
    console.log(arg.foo); // Error
    console.log(arg.bar); // ok
  }
}

doStuff(new Foo());
doStuff(new Bar());
```



in

in操作符可以安全的检查一个对象上是否存在一个属性, 被作为类型保护使用

```
interface A {
	x: number;
}

interface B {
	y: number;
}

function doStuff(q: A | B) {
	if ('x' in q) {
		// q: A
	} else {
	  // q: B
	}
}
```



自定义类型保护

is

```
interface Foo {
	foo: number;
	common: string;
}

interface Bar {
	bar: number;
	common: string;
}

function isFoo(arg: Foo | Bar): arg is Foo {
	return (arg as Foo).foo !== undefined;
}
```



字面量类型

string

`type Direction = 'North' | 'East' | 'South' | 'West'`

number

`type OneToFive = 1 | 2 | 3 | 4 | 5`

boolean  

`type Bools = true | false`



##### readonly 和 Readonly

readonly 标识某个属性为只可读

Readonly接收一个泛型 表示泛型的所有属性都是只可读类型



##### 函数重载

根据函数参数不同，使用不同的函数

```typescript
declare function test(a: string): string;
declare function test(a: number): number;

const resS = test('Hello World'); // 推断出是string
const resN = test(12); //推断出是number
```



##### 映射类型

内置映射类型

`Partial  Readonly   Record   Pick  ThisType  Exclude   Extract   NonNullable  ReturnType   InstanceType`

keyof 可以拿到对象key的类型

---

[巧用TS](https://jkchao.cn/article/5bb9c63963a5d23d5ce3091b)

[Typescript入门教程](https://ts.xcatliu.com/basics/declaration-files)