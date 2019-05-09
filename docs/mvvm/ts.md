## TypeScript

扩展名`.ts`

### 类型

`string ` 字符串

`boolean` 布尔值

`number` 数字

数组 

1. `number[]` 
2. `Array<number>`

元组

元组类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同. 如果操作的方法和类型不符合, 会报错

`any` 不希望ts进行类型检查

`void` 表示没有任何类型, 比如一个函数没有返回

```
function a():void {
  
}
```

`null`

`undefined`

`object` 非原始类型`number string symbol null undefined`

### 类型断言

你清楚地知道一个实体具有比它现有类型更确切的类型,ts会假设你已经进行了必须的检查

```
let someValue: any = "this is a string";

let strLength: number = (<string>someValue).length;
```

`readonly` 只读属性

### 接口

我们通过接口来描述一个拥有`A`和`B`的对象

```typescript
interface Word {
  A: string,
  B: string
}
// writeWord的输入得包含Word接口要求的结构
function writeWord(word: Word){
  return word.A + word.B;
}
```

### 类

在构造函数的参数上使用`public`等同于创建了同名的成员变量

