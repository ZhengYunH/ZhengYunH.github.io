# <span id="Title">Markdown 语法</span>
## 区块元素
### 标题

# 一级标题 `# 一级标题` 

## 二级标题 `## 二级标题` 

### 三级标题 `### 三级标题`

 ... 以此类推，直到六级  

### 区块引用 blockquote	>

    > This is a blockquote with two paragraphs.
    > The first one
    > 
    > and the second one.
    > 
    > > This is nested blockquote.
    > >
    > > This is the second level.
    > 
    > Back to the first level
> This is a blockquote with two paragraphs.
> The first one
>
> and the second one.
>
> > This is nested blockquote.
> >
> > This is the second level.
>
> Back to the first level

### 列表

#### 无序(任意一个符号都可以)

```
* star1
* star2
* star3

+ plus

- minus

typora中如果要离开无序列表，要用回车。退格只是删去小黑点，不是退出无序列表
```

* star1 
* star2 
* star3



* plus 



* minus

#### 有序

```
1. Blue
2. Red
3. Green

注意1. 和Blue之间有个空格，同样的typora中，用回车离开有序列表
```

  1. Blue
  2. Red
  3. Green
### 代码区块 ```
```
#include<iostream>
int main(){
    return 0;
}
```
### 分割线（任意一种都可以）

```
* * *
***
*****
- - -
```

* * *
***
*****
- - -
## 区段元素
### 链接

```
This link is linked to the [source](http://www.appinn.com/markdown/) .
```

This link is linked to the [source](http://www.appinn.com/markdown/) .
This links to the [update_list](../update_list.md/) .
### 强调

```
*underscores*
_underscores_
**underscores**
__double underscores__
```



*underscores*
_underscores_
**underscores**
__double underscores__

### 代码

```
Use the `printf()` function.
```

Use the `printf()` function.

### 图片

```
![picture](https://gss2.bdstatic.com/9fo3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike180%2C5%2C5%2C180%2C60/sign=d997317c11ce36d3b6098b625b9a51e2/00e93901213fb80ef9ceac7132d12f2eb938947d.jpg)

typora中直接复制粘贴即可，注意一下路径
```



![picture](https://gss2.bdstatic.com/9fo3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike180%2C5%2C5%2C180%2C60/sign=d997317c11ce36d3b6098b625b9a51e2/00e93901213fb80ef9ceac7132d12f2eb938947d.jpg)
## 其他
### 自动链接
[My github]<https://github.com/ZhengYunH>

### 页内链接
[Title](#Title)
