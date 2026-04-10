---
title: 'Python *args 和 **kwargs 轻松掌握 - Python 速查表'
description: '*args 和 **kwargs 概念可能令人望而生畏，但实际上它们并不难理解，能为您的函数带来极大的灵活性。'
date: 'March 08, 2019'
updated: 'July 1, 2022'
tags: 'python, intermediate'
socialImage: '/blog/kwargs.jpg'
layout: 'article'
---

<route lang="yaml">
meta:
    layout: "article"
    title: "Python *args 和 **kwargs 轻松掌握 - Python 速查表"
    description: "*args 和 **kwargs 概念可能令人望而生畏，但实际上它们并不难理解，能为您的函数带来极大的灵活性。"
    date: "March 08, 2019"
    updated: "July 1, 2022"
    tags: "python, intermediate"
    socialImage: "/blog/kwargs.jpg"
</route>

<blog-title-header :frontmatter="frontmatter" title="Python \*args 和 \*\*kwargs 轻松掌握 - Python 速查表" />

我不知道你怎么样，但每次我看到带有 `*args` 和 `**kwargs` 作为参数的函数时，我都会有点害怕。即使在用 Django 做后端工作时，我也“使用”过它们，但却一无所知。如果你像我一样是自学成才的开发者，我知道你也有过同样的经历。

几个月前，我决定不再懒惰并开始研究它。令我惊讶的是，在解释器中把玩时它们很容易理解，但在阅读关于它们的内容时却没那么容易。我写了这篇文章，试图以我希望别人向我解释的方式来解释 [args 和 kwargs](https://labex.io/pythoncheatsheet/zh/#args-and-kwargs)。

## 基础知识 (Basics)

你需要知道的第一件事是 `*args` 和 `**kwargs` 允许你在调用 [函数](https://labex.io/pythoncheatsheet/zh/#Functions) 时传递**未定义数量**的 `arguments`（参数）和 `keywords`（关键字参数）：

```python
def some_function(*args, **kwargs):
    pass

# 使用任意数量的参数调用 some_function
some_function(arg1, arg2, arg3)

# 使用任意数量的关键字参数调用 some_function
some_function(key1=arg1, key2=arg2, key3=arg3)

# 同时调用，参数和关键字参数
some_function(arg, key1=arg1)

# 或者不调用任何参数
some_function()
```

其次，`args` 和 `kwargs` 这两个词是约定俗成的名称。这意味着它们不是由解释器强制要求的，而是 Python 社区中被认为是良好的实践：

```python
# 这个函数可以正常工作
def some_function(*arguments, **keywords):
    pass
```

<base-warning>
  <base-warning-title>
    关于约定的说明
  </base-warning-title>
  <base-warning-content>
    即使上面的函数可以工作，也不要这样做。约定是为了帮助你为你和任何可能对你的项目感兴趣的人编写可读的代码。
    其他约定包括 4 个空格的缩进、注释和导入。强烈建议阅读 <a target="_blank" href="https://www.python.org/dev/peps/pep-0008/">PEP 8 -- Python 代码风格指南</a>。
  </base-warning-content>
</base-warning>

那么，Python 是如何知道我们希望函数接受多个参数和关键字参数的呢？是的，答案是 `*` 和 `**` 运算符。

现在我们已经涵盖了基础知识，让我们来实战一下 👊。

## args

我们现在知道如何使用 `*args` 作为函数的参数来传递多个参数，但我们如何使用它们呢？这很简单：所有参数都包含在 `args` 变量中，形式为一个 [元组](https://labex.io/pythoncheatsheet/zh/#Tuple-Data-Type)：

```python
def some_function(*args):
    print(f'Arguments passed: {args} as {type(args)}')


some_function('arg1', 'arg2', 'arg3')
# Arguments passed: ('arg1', 'arg2', 'arg3') as <class 'tuple'>
```

我们可以遍历它们：

```python
def some_function(*args):
    for a in args:
        print(a)


some_function('arg1', 'arg2', 'arg3')
# arg1
# arg2
# arg3
```

使用索引访问元素：

```python
def some_function(*args):
    print(args[1])


some_function('arg1', 'arg2', 'arg3')  # arg2
```

切片：

```python
def some_function(*args):
    print(args[0:2])


some_function('arg1', 'arg2', 'arg3')
# ('arg1', 'arg2')
```

任何你可以对 [元组](https://labex.io/pythoncheatsheet/zh/#Tuple-Data-Type) 做的事情，你都可以对 `args` 做。

## kwargs

参数在 `args` 变量中，而关键字参数在 `kwargs` 中，但这次是以 [字典](https://labex.io/pythoncheatsheet/zh/#Dictionaries-and-Structuring-Data) 的形式，其中键是关键字：

```python
def some_function(**kwargs):
    print(f'keywords: {kwargs} as {type(kwargs)}')


some_function(key1='arg1', key2='arg2', key3='arg3')
# keywords: {'key1': 'arg1', 'key2': 'arg2', 'key3': 'arg3'} as <class 'dict'>
```

同样，我们可以对 `kwargs` 做任何我们对任何 [字典](https://labex.io/pythoncheatsheet/zh/#Dictionaries-and-Structuring-Data) 会做的事情。

遍历：

```python
def some_function(**kwargs):
    for key, value in kwargs.items():
        print(f'{key}: {value}')


some_function(key1='arg1', key2='arg2', key3='arg3')
# key1: arg1
# key2: arg2
# key3: arg3
```

使用 `get()` 方法：

```python
def some_function(key, **kwargs):
    print(kwargs.get(key))


some_function('key3', key1='arg1', key2='arg2', key3='arg3')
# arg3
```

还有更多 [内容](https://labex.io/pythoncheatsheet/zh/#Dictionaries-and-Structuring-Data) =)。

## 结论 (Conclusion)

`*args` 和 `**kwargs` 可能看起来很吓人，但事实是它们并不难理解，并且有能力为你的函数带来很大的灵活性。如果你了解 [元组](https://labex.io/pythoncheatsheet/zh/#Tuple-Data-Type) 和 [字典](https://labex.io/pythoncheatsheet/zh/#Dictionaries-and-Structuring-Data)，你就准备好了。

想玩玩 args 和 kwargs 吗？[这里](https://mybinder.org/v2/gh/labex-labs/python-cheatsheet/master?filepath=jupyter_notebooks) 是一个在线 Jupyter Notebook 供你尝试。

有些示例使用了 `f-strings`，这是 Python 3.6+ 中一种相对较新的格式化字符串的方式。[在这里](https://labex.io/pythoncheatsheet/zh/#Formatted-String-Literals-or-f-strings) 你可以阅读更多相关信息。
