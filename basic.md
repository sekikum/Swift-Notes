# 常量和变量
let 声明常量，不可变
var 声明变量，可变
```swift
let maximumNumberOfLoginAttempts = 10
var currentLoginAttempt = 0
```
# Type Annotations
welcomeMessage为String类型
```swift
var welcomeMessage : String
welcomeMessage = "Hello"
```
red，green，blue均为double类型
```swift
var red, green, blue : Double
```
在实践中很少需要编写类型注释，如果在定义常量或变量时给它提供了初始值，Swift可自行推断其类型
welcomeMessage没有提供初始值，则使用类型注释指定其类型
# 常量和变量的命名
可以包含unicode字符。不能包含空白字符、数学符号、箭头、专用Unicode标量值或行和框绘制字符。不能以数字开头。
```swift
let π = 3。14159
let 你好 = "你好世界"
let 🐶 = "dog"
```
一旦声明了某个类型的常量或变量，就不能再用相同的名称声明它，也不能将其更改存储为不同类型的值。也不能将常量改为变量，变量改为常量。
在使用关键字作为名称时，使用``将关键字扩起来。尽力避免这种情况
```swift
let `let` = 123
```
# print
```swift
print("Hello World")
print(123)
```
通过使用字符串插值将变量或常量的值添加到字符串文字中
```swift
var name = "Sibby"
print(name)
print("Hello \(name)")      //Hello Sibby
```
使用分隔符separator
以.分隔每个项目
```swift
print("Hello", 2022, "Bob", separator: ".")     //Hello.2022.Bob
```
使用终止符terminator
以空结尾，可达到不换行的效果
```swift
print("Hello ", termiator: "")
print("World!")     //Hello World
```
# 注释
swift中的注释可以嵌套
```swift
/* This is the start of the first multiline comment.
 /* This is the second, nested multiline comment. */
This is the end of the first multiline comment. */
```
# 类型
UInt Int Double Float
```swift
let minValue = UInt8.min    // 0
let maxValue = UInt8.max    // 255

let decimalInteger = 17
let binaryInteger = 0b10001       // 17 in binary notation
let octalInteger = 0o21           // 17 in octal notation
let hexadecimalInteger = 0x11     // 17 in hexadecimal notation
```
十进制数用e表示
1.25e2 means 1.25 x 10^2^, or 125.0
1.25e-2 means 1.25 x 10^-2^, or 0.0125
十六进制用p表示
0xFp2 means 15 x 2^2^, or 60.0
0xFp-2 means 15 x 2^-2^, or 3.75

添加 _ 让数字更好读
```swift
let paddedDouble = 000123.456
let oneMillion = 1_000_000
let justOverOneMillion = 1_000_000.000_000_1
```
需要将类型进行转换才能相加减
```swift
let three = 3
let pointOneFourOneFiveNine = 0.14159
let pi = Double(three) + pointOneFourOneFiveNine    // pi equals 3.14159, and is inferred to be of type Double
```
将浮点类型转换为整型时，总是被“截断”。即4.75 -> 4; -3.2 -> -3
# 类型别名
使用typealias关键字定义类型别名
```swift
typealias AudioSample = UInt16
var maxAmplitudeFound = AudioSample.min
```
# 元组
适合简单的数据组，不适合创建复杂的数据结构
```swift
let http404Error = (404, "Not Found")       // http404Error is of type (Int, String), and equals (404, "Not Found")
```
元组可以包含任意数量的任意类型。如：(Int, Int, Int)  (String, Bool)
打印元组的值
```swift
let (statusCode, statusMessage) = http404Error
print("The status code is \(statusCode)")           // Prints "The status code is 404"
print("The status message is \(statusMessage)")     // Prints "The status message is Not Found"
```
如果只想获取其中一个，可用_代表省略
```swift
let (justTheStatusCode, _) = http404Error
print("The status code is \(justTheStatusCode)")    // Prints "The status code is 404"
```
使用index访问元组
```swift
print("The status code is \(http404Error.0)")       // Prints "The status code is 404"
print("The status message is \(http404Error.1)")    // Prints "The status message is Not Found"
```
在定义元组时给元素命名
```swift
let http200Status = (statusCode: 200, description: "OK")

print("The status code is \(http200Status.statusCode)")     // Prints "The status code is 200"
print("The status message is \(http200Status.description)") // Prints "The status message is OK"
```
# Optional
Use optionals in situations where a value may be absent
convertedNumber的初始化有可能不成功，所以它是一个optional Int而非Int
```swift
let possibleNumber = "123"
let convertedNumber = Int(possibleNumber)
```
nil: 可将一个optional变量设置为无值状态
```swift
var serverResponseCode: Int? = 404
serverResponseCode = nil
```
当定义了一个optional变量但没有提供默认值，这个变量会自动设置为nil
```swift
var surveyAnswer: String?
```
任何optional类型或对象都可以设置为nil, non-optional变量不可以设置为nil
# Forced Unwrapping（强制展开）
在确定一个optional变量不为nil后，可以通过在optional变量名称的末尾加 ! 来访问它的底层值。这被称为Forced Unwrapping
试着用!访问不存在的optional变量会出发运行时错误，在使用前一定确保其不为nil
```swift
if (convertedNumber != nil) {
    print("convertedNumber has an integer value of \(convertedNumber!).")
}
```
# Optional Binding
Use optional binding to find out whether an optional contains a value, and if so, to make that value available as a temporary constant or variable.

If the optional Int returned by Int(possibleNumber) contains a value, set a new constant called actualNumber to the value contained in the optional.
```swift
if let actualNumber = Int(possibleNumber) {
    print("The string \"\(possibleNumber)\" has an integer value of \(actualNumber)")
} else {
    print("The string \"\(possibleNumber)\" couldn't be converted to an integer")
}
// Prints "The string "123" has an integer value of 123"
```
如果在访问它包含的值后不需要引用原始的Optional常量或变量，可用对新的常量或变量使用相同的名称
```swift
let myNumber = Int(possibleNumber)      // Here, myNumber is an optional integer
if let myNumber = myNumber {            // Here, myNumber is a non-optional integer
    print("My number is \(myNumber)")
}
// Prints "My number is 123"
```
上面的代码还可以简写如下
```swift
if let myNumber {
    print("My number is \(myNumber)")
}
// Prints "My number is 123"
```
在if语句中使用Optional Binding创建的常量和变量仅在if语句体中可用