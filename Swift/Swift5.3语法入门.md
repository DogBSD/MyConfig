# Swift5.3语法入门

# 1. 基础内容

## 1.1 常量、变量

```swift
# 变量 var
# 常量 let
在SWIFT中声明常量、变量必须使用关键字

let x = 3, y = 2, z = 1 //需要声明多个变量时，可以一行连续申请，使用逗号隔开

# 类型标注
var x, y, z: Int  //此时xyz只能存入Int类型的值


# 栗子：给Number赋值为11，并丢改其值为 3，使用类型标记

var number: Int = 11
number = 3
print(number)   // print是一个输出全局函数

>> 3

# 字符插值
let age = 18
print("My age is \(age)")  //print输入字符串使用双引号，把声明的常量前使用反斜杠，并括号括起来
```

## 1.2 注释

```swift
# 在SWIFT中，注释部分不会做任何编译，只是方便Coder阅读

# 单行注释
// print(xxx)

# 多行注释

/* 我是内容！  //
我是内容！
我是内容！
我是内容！  */

# 多行注释内嵌其他注释

/* 这是第一个多行注释的开头
/* 这是第二个嵌套在内的注释块 */
这是第一个注释块的结尾 */
```

## 1.3 分号

在很久很久很久`x3`以前学习C语言时，每一个语句结尾处必须用分号`;`，但是在SWIFT并没有这种硬性规定，可有可无，建议不添加

```swift
print(xxx);
```

## 1.3 整数

没有小数点的数都是整数，在任何编程语言中，整数都是存在范围的。

```swift
# 整数范围

# 通过，max、min属性打印Int8整数类型的范围

let number1 = Int8.max, number2 = Int8.min
print(number1, number2)

>> 127 -128   //  (2^8)/2

尽量在代码中使用 Int 作为你的整数的值类型。这样能提高代码的统一性和兼容性，即使在 32 位的平台上， Int 也可以存 -2,147,483,648 到 2,147,483,647 之间的任意值，对于大多数整数区间来说完全够用了。

UInt 是swift提供的无符号Int类型，就是非负数的整数，0～...
```

## 1.4 浮点数

浮点数的范围比整数更大，

- Double代表 64 位的浮点数；至少 15 位数字的精度，`推荐！`
- Float 代表 32 位的浮点数，6 位数字的精度

## 1.5 类型推断

因为Swift是类型安全型语言，所以在编译时，编译器都是会检查类型是否正确，确保传入的值对应相应的类型；正应有类型推断的存在，编写代码过程中就可以少些很多`类型标注`。

Swift 在推断浮点数时总是推断为 Double而不是 Float。

## 1.6 数字型字面量

内容见：https://www.cnswift.org/the-basics#spl-12

## 1.7 数字类型转换

```swift
# 整数转换

let twoThousand: UInt16 = 2_000
let one: UInt8 = 1 //范围没有UInt16大，Unit16的范围32767 -32768
let twoThousandAndOne = twoThousand + UInt16(one) //将UInt8转换为UInt16

# 整数与浮点数转换
let three = 3
let pointOneFourOneFiveNine = 0.14159
let pi = Double(three) + pointOneFourOneFiveNine //需要将3转换为浮点数3.0，如果是0.14159转换为Int类型，会出现数字截断的情况，从而变为0
```

## 1.8 类型别名

*类型别名*可以为已经存在的类型定义了一个新的可选名字。用 typealias 关键字定义类型别名。

```swift
# 关键字 typealias
typealias AudioSample = UInt16  // 现在给UInt16添加一个别名为AudioSample
var maxAmplitudeFound = AudioSample.min //跟UInt16.min是一样的
```

## 1.9 布尔值

布尔值只有两种形式，true与false。布尔类型大多数用于if语句的判断使用。

```swift
# example

let door = true

if door {
  print("门是开着的")
} else {
  print("门是关着的")
}
```

## 1.10 元组

*元组*把多个值合并成单一的复合型的值。元组内的值可以是任何类型，而且可以不必是同一类型。

```swift
let http404Error = (404, "Not Found") //可看作（Int，String）

# 拆分的方式访问
let (statusCode, _) = http404Error  //拆分元组时不需要的部分可以用_忽略。
print("The status code is \(statusCode)")
// prints "The status code is 404"

# 利用从零开始的索引数字访问元组中的单独元素
print("The status code is \(http404Error.0)")
// prints "The status code is 404"

# 可以在定义元组的时候给其中的单个元素命名：
let http200Status = (statusCode: 200, description: "OK")

print(The status code is \(http200Status.statusCode)")
```

## 1.11 可选项

可以利用*可选项*来处理值可能缺失的情况。类似：这里有值，为8，或者，这里没有值。

```swift
# example
let possibleNumber = "123"
let convertedNumber = Int(possibleNumber) //一部分String可以转换为Int类型，但是不确定一定可以转换，编译后返回一个可选Int值，即为Int？
print(convertedNumber)

>> Optional(123)
```

### 1.11.1 nil

`nil` 不能用于非可选的常量或者变量，如果代码中变量或常量需要作用于特定条件下的值缺失，可以给他声明为相应类型的可选项。

```swift
var serverResponseCode: Int? = 404
// serverResponseCode contains an actual Int value of 404
serverResponseCode = nil
// serverResponseCode now contains no value

# 相对于上面的这种赋予Int?为nil，最好的方式就是直接声明为可选项，默认为空值。

var serverResponseCode: Int?
```

### 1.11.2 If 语句以及强制展开

通过if语句对需要判断是否为空值的条件进行选择，使用（== 或者 !+）进行。

```swift
if convertedNumber != nil {
    print("convertedNumber has an integer value of \(convertedNumber!)")
}

# \(convertedNumber!)的！表示，确认有值，强制进行展开。如果没有!就会返回为Optional(123)。
```

### 1.11.3 可选项绑定

可以使用*可选项绑定*来判断可选项是否包含值，如果包含就把值赋给一个临时的常量或者变量。可选绑定可以与 if 和while 的语句使用来检查可选项内部的值，并赋值给一个变量或常量。 

```swift
# example
if let constantName = someOptional { 
    statements 
} 

# 使用可选项绑定就不需要使用强制展开
if let actualNumber = Int(possibleNumber) {
    print("\'\(possibleNumber)\' has an integer value of \(actualNumber)")
} else {
    print("\'\(possibleNumber)\' could not be converted to an integer")
}

解读代码：如果  Int(possibleNumber)  返回的可选 Int 包含一个值，将这个可选项中的值赋予一个叫做 actualNumber 的新常量。
如果转换成功，常量 actualNumber 就可以用在 if 语句的第一个分支中，他早已被可选内部的值进行了初始化，所以这时就没有必要用 ! 后缀来获取里边的值。在这个栗子中 actualNumber 被用来输出转换后的值。
```

### 1.11.4 隐式展开可选项

有时在一些程序结构中可选项一旦被设定值之后，就会一直拥有值。在这种情况下，就可以去掉检查的需求，也不必每次访问的时候都进行展开，因为它可以安全的确认每次访问的时候都有一个值。

这种类型的可选项被定义为*隐式展开可选项*。通过在声明的类型后边添加一个叹号（ String! ）而非问号（ String? ） 来书写隐式展开可选项。与在使用可选项时在名称后加一个叹号不同的是，声明的时候要把叹号放在类型的后面。

```swift
let possibleString: String? = "An optional string."
let forcedString: String = possibleString! // requires an exclamation mark

let assumedString: String! = "An implicitly unwrapped optional string."
// 有显式的非可选 String 类型
let implicitString: String = assumedString // no need for an exclamation mark
>> An implicitly unwrapped optional string.

// 没有显式写明类型所以它是普通可选项
let optionalString = assumedString
>> Optional("An implicitly unwrapped optional string.")
# 解释：把隐式展开可选项当做在每次访问它的时候被给予了自动进行展开的权限，你可以在声明可选项的时候添加一个叹号而不是每次调用的时候在可选项后边添加一个叹号。
```

## 1.12 错误处理

在程序执行阶段，你可以使用*错误处理*机制来为错误状况负责。

相比于可选项的通过值是否缺失来判断程序的执行正确与否，而错误处理机制能允许你判断错误的形成原因，在必要的情况下，还能将你的代码中的错误传递到程序的其他地方。

通过在函数声明过程当中加入 throws 关键字来表明这个函数会抛出一个错误。当你调用了一个可以抛出错误的函数时，需要在表达式前预置 try 关键字。

```swift
func canThrowAnError() throws {
    // this function may or may not throw an error
}
```

## 1.13 断言和先决条件

详细见：https://www.cnswift.org/the-basics#spl-23

`断言和先决条件的不同之处在于他们什么时候做检查`：断言只在 debug 构建的时候检查，但先决条件则在 debug 和生产构建中生效。在生产构建中，断言中的条件不会被计算。这就是说你可以在开发的过程当中随便使用断言而无需担心影响生产性能。

### 1.13.1 断言

```swift
# 关键字：assert
# 断言判断条件为true时，程序继续执行；反之，触发断言，终止程序执行
let age = -3
assert(age >= 0, "A person's age cannot be less than zero") //断言不一定需要，返回什么预留信息
// this causes the assertion to trigger, because age is not >= 0

使用assertionFailure来检查断言失败，当所有条件都被正常检查以后
```

### 1.13.2 强制先决条件

在你代码中任何条件`可能潜在为假但必须*肯定* 为真才能继续执行的地方使用先决条件。比如说，使用先决条件来检测下标没有越界，或者检测函数是否收到了一个合法的值。

```swift
# 关键字：precondition
# 当条件为 false时会触发先决条件
// In the implementation of a subscript...
precondition(index > 0, "Index must be greater than zero.")
```



-----



