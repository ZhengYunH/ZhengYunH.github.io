# JSON

[reference1]: http://www.json.org	"Introducing JSON"

## 简介

**JSON**(JavaScript Object Notation) 是一种轻量级的数据交换格式。 易于人阅读和编写。同时也易于机器解析和生成。 JSON采用完全独立于语言的文本格式，但是也使用了类似于C语言家族的习惯（包括C, C++, C#, Java, JavaScript, Perl, Python等）。 这些特性使JSON成为理想的数据交换语言。

## 数据结构

JSON建构于两种数据结构： 

- “名称\值”对的集合，也就是对象 
- 值的有序列表，也就是数组 

## 形式

### 对象 object

以 `{` 开始， `}` 结束。每个**名称**后面跟一个 `:`，**键值对**之间使用  `,`分割

![img](assets/object.gif)

+ object
  + {}
  + { members }
+ member
  + pair
  + pair , members
+ pair
  + string : value

### 数组 array

以`[`开始，`]`结束，值之间用`,`分割

![img](assets/array.gif)

+ array
  + []
  + [ elements ]
+ elements
  + value
  + value , elements

### 值 value

![img](assets/value.gif)

### 字符串 string

字符串（*string*）是由双引号包围的任意数量Unicode字符的集合，使用反斜线转义

![img](assets/string.gif)

+ string
  + ""
  + " chars "
+ chars
  + char
  + char chars
+ char
  + any Unicode character except : `" \ control_character`
  + control_character
    + \"
    + \\
    + \/
    + \b
    + \f
    + \n
    + \r
    + \t
    + \u four-hex-digits

### 数值 number

![img](assets/number.gif)

+ number
  + int
  + int frac
  + int exp
  + int frac exp
+ int
  + digit
  + digit digits
  + \- digit
  + \- digit digits
+ frac
  + .digits
+ exp
  + e digits
+ digits
  + digit
  + digit digits
+ e
  + e
  + e+
  + e-
  + E
  + E+
  + E-