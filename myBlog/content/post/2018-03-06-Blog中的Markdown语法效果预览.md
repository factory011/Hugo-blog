---
title: "Blog中的Markdown语法效果预览"
date: 2018-03-06T16:01:23+08:00
draft: false
tags: ["markdown"]
categories: ["markdown"]

weight: 1 # 置顶功能

---

## 1 md引用：`> + （space or enter）`显示效果

>To the world you may be one person, but to one person you may be the world
>
>对于世界而言，你是一个人；但是对于某个人，你是他的整个世界。

## 2 md无序列表：`* + space`显示效果

* No need to have a reason to love you. Anything can be a reason not to love you
* 喜欢你，不需要理由；不喜欢你，什么都可以成为理由。

## 3 md有序列表：`num. + space`显示效果

1. Three solutions to every problem: accept it, change it, leave it. If you can't accept it, change it. If you can't change it, leave it.
2. 有三个方法可以解决所有的问题。接受，改变，放开。不能接受那就改变，不能改变，那就放开

## 4 md代码块：

```
// markdown语法，部分符号标题里呈现不出来，所以放在代码块中了
（```html or ```css or ```scss or ```js） + enter
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<p> Because the things you're scared of are usually the most worthwhile</p>
	<p> 每天都尝试去一件你害怕的事情，因为，你所害怕的事情，往往是最值得的。</p>
</body>
</body>
</html>
```

```scss
{
width:100px;
height:100px;
background:red;
animation:myfirst 5s;
-webkit-animation:myfirst 5s; /* Safari and Chrome */
}

@-webkit-keyframes myfirst /* Safari and Chrome */
{
from {background:red;}
to {background:yellow;}
}
```

```js
async function getStockPriceByName(name) {
  const symbol = await getStockSymbol(name);
  const stockPrice = await getStockPrice(symbol);
  return stockPrice;
}

getStockPriceByName('goog').then(function (result) {
  console.log(result);
});
```

## 5 md公式：

```
// markdown语法
$$ + enter
```


$$
E=mc2
$$

## 6 md标题：`（# or ## or ### or #### or ##### or ######）+ space+ 文字 + enter`显示效果

```
// 标题就不展示了，影响右侧的目录结构
# The Maxwell's Equations

## Euler's Identity

### Newton's Second Law of Motion

#### Pythagorean Theorem
##### Mass–energy Equivalence
###### The Schrödinger Equation
```



## 7 md链接：`[显示说明](链接url) + enter`显示效果

[google](https://www.google.com/)

## 8 md表格：

```
// markdown语法
| 表头 | 表头 | 表头 |
| ---- | :--: | ---: |
| 内容 | 内容 | 内容 |
| 内容 | 内容 | 内容 |
```



| 表头 | 表头 | 表头 |
| ---- | :--: | ---: |
| 内容 | 内容 | 内容 |
| 内容 | 内容 | 内容 |

## 9 md分割线：`--- + enter or <hr />`显示效果

---



## 10 md图片：`![显示说明](图片url) + enter`显示效果

![wechat](/img/reward/wechat.png)
