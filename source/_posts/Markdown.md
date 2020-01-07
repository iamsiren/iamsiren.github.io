---
title: Markdown
categories: 技术分享
---
## Markdown是什么？
>它实际上是个非常简单、非常容易学习的语法。这个语法简单到每个人都可以在5分钟以内学会。应该是为数不多，你真的可以彻底学会的语言。
更重要的是，Markdown语法所有要素，是与写作的习惯一脉相承的，套用句俗语：仅为写作而生。

## Markdown 的优点如下：
>纯文本，所以兼容性极强，可以用所有文本编辑器打开。
让你专注于文字而不是排版。
格式转换方便，Markdown 的文本你可以轻松转换为 html、电子书等。
Markdown 的标记语法有极好的可读性。

<!--more-->
## Markdown 语法
### 标题
这是最为常用的格式，在平时常用的的文本编辑器中大多是这样实现的：输入文本、选中文本、设置标题格式。
而在 Markdown 中，你只需要在文本前面加上 # 即可，同理、你还可以增加二级标题、三级标题、四级标题、五级标题和六级标题，总共六级，只需要增加 # 即可，标题字号相应降低。例如：
![image.png](https://upload-images.jianshu.io/upload_images/53729-ae322481bef00997.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 列表
列表格式也很常用，在 Markdown 中，你只需要在文字前面加上 - 就可以了。
![image.png](https://upload-images.jianshu.io/upload_images/53729-f98648591c19c7de.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 链接
在 Markdown 中，插入链接不需要其他按钮，你只需要使用 `[显示文本](链接地址)` 这样的语法即可，例如：

在 Markdown 中，插入图片不需要其他按钮，你只需要使用 `![](图片链接地址)` 这样的语法即可，例如：

```
![](http://upload-images.jianshu.io/upload_images/259-0ad0d0bfc1c608b6.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
注：插入图片的语法和链接的语法很像，只是前面多了一个 `！`。*

### 引用

在我们写作的时候经常需要引用他人的文字，这个时候引用这个格式就很有必要了，在 Markdown 中，你只需要在你希望引用的文字前面加上 `>` 就好了，例如：

```
> 一盏灯， 一片昏黄； 一简书， 一杯淡茶。 守着那一份淡定， 品读属于自己的寂寞。 保持淡定， 才能欣赏到最美丽的风景！ 保持淡定， 人生从此不再寂寞。

```

注：`>` 和文本之间要保留一个字符的空格。*

最终显示的就是：

> 一盏灯， 一片昏黄； 一简书， 一杯淡茶。 守着那一份淡定， 品读属于自己的寂寞。 保持淡定， 才能欣赏到最美丽的风景！ 保持淡定， 人生从此不再寂寞。

### 粗体和斜体

Markdown 的粗体和斜体也非常简单，用两个 `*` 包含一段文本就是粗体的语法，用一个 `*` 包含一段文本就是斜体的语法。例如：

```
 *一盏灯*， 一片昏黄；**一简书**， 一杯淡茶。 守着那一份淡定， 品读属于自己的寂寞。 保持淡定， 才能欣赏到最美丽的风景！ 保持淡定， 人生从此不再寂寞。

```

最终显示的就是下文，其中「一盏灯」是斜体，「一简书」是粗体：

*一盏灯*， 一片昏黄；**一简书**， 一杯淡茶。 守着那一份淡定， 品读属于自己的寂寞。 保持淡定， 才能欣赏到最美丽的风景！ 保持淡定， 人生从此不再寂寞。

### 代码引用

需要引用代码时，如果引用的语句只有一段，不分行，可以用 ` 将语句包起来。
如果引用的语句为多行，可以将```置于这段代码的首行和末行。

### 表格

相关代码：

```
| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

```

显示效果：

| Tables | Are | Cool |
| --- | --- | --- |
| col 3 is | right-aligned | $1600 |
| col 2 is | centered | $12 |
| zebra stripes | are neat | $1 |

<p></p>
相关代码：

```
dog | bird | cat
----|------|----
foo | foo  | foo
bar | bar  | bar
baz | baz  | baz

```

显示效果：

| dog | bird | cat |
| --- | --- | --- |
| foo | foo | foo |
| bar | bar | bar |
| baz | baz | baz |

[献给写作者的 Markdown 新手指南](https://www.jianshu.com/p/q81RER "献给写作者的 Markdown 新手指南")

