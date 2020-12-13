## swift

为什么要学swift？

想整个游戏项目。 有点想法

### 基础

### 基础数据类型

Int, Float, Double, Bool, String

变量的声明 var

常量的声明 let

类型的判断 type(of: )

输出语句 print()， 可传多个参数

拼接字符串 

1. **+** eg: `a + b`
2. \() eg: `"asdasdas\(c)"` c是一个变量

声明数组 声明字典 `[]`

```
var shoppingList = ["catfish", "water", "tulips"]
shoppingList[1] = "bottle of water"

var occupations = [
    "Malcolm": "Captain",
    "Kaylee": "Mechanic",
]
occupations["Jayne"] = "Public Relations"
```

循环
```
let individualScores = [75, 43, 103, 87, 12]
var teamScore = 0
for score in individualScores {
    if score > 50 {
        teamScore += 3
    } else {
        teamScore += 1
    }
}
print(teamScore)
// Prints "11"
```
