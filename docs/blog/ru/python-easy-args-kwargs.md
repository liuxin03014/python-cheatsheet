---
title: 'Python *args и **kwargs: Простое Руководство'
description: 'args и kwargs могут показаться сложными, но на самом деле их легко понять. Они придают вашим функциям большую гибкость.'
date: 'March 08, 2019'
updated: 'July 1, 2022'
tags: 'python, intermediate'
socialImage: '/blog/kwargs.jpg'
layout: 'article'
---

<route lang="yaml">
meta:
    layout: "article"
    title: "Python *args и **kwargs: Простое Руководство"
    description: "args и kwargs могут показаться сложными, но на самом деле их легко понять. Они придают вашим функциям большую гибкость."
    date: "March 08, 2019"
    updated: "July 1, 2022"
    tags: "python, intermediate"
    socialImage: "/blog/kwargs.jpg"
</route>

<blog-title-header :frontmatter="frontmatter" title="Python \*args и \*\*kwargs: Простое Руководство" />

Я не знаю как вы, но каждый раз, когда я видел функцию с параметрами `*args` и `**kwargs`, мне становилось немного страшно. Я даже "использовал" их при работе с бэкендом на Django, ничего не понимая. Если вы такой же самоучка, как и я, я знаю, что вы тоже через это проходили.

Несколько месяцев назад я решил перестать лениться и начал исследовать этот вопрос. К моему удивлению, их было легко понять, играя с интерпретатором, но не так просто, когда читаешь о них. Я написал этот пост, пытаясь объяснить [args и kwargs](https://labex.io/pythoncheatsheet/ru/#args-and-kwargs) так, как мне хотелось бы, чтобы мне их объяснили.

## Основы

Первое, что вам нужно знать, это то, что `*args` и `**kwargs` позволяют передавать неопределенное количество `arguments` (аргументов) и `keywords` (ключевых слов) при вызове [функции](https://labex.io/pythoncheatsheet/ru/#Functions):

```python
def some_function(*args, **kwargs):
    pass

# вызов some_function с любым количеством аргументов
some_function(arg1, arg2, arg3)

# вызов some_function с любым количеством ключевых слов
some_function(key1=arg1, key2=arg2, key3=arg3)

# вызов обоих, аргументов и ключевых слов
some_function(arg, key1=arg1)

# или ни одного
some_function()
```

Во-вторых, слова `args` и `kwargs` — это соглашения. Это означает, что они не навязываются интерпретатором, но считаются хорошей практикой среди сообщества Python:

```python
# Эта функция будет работать совершенно нормально
def some_function(*arguments, **keywords):
    pass
```

<base-warning>
  <base-warning-title>
    Примечание о соглашениях
  </base-warning-title>
  <base-warning-content>
    Даже если приведенная выше функция работает, не делайте этого. Соглашения существуют для того, чтобы помочь вам писать читаемый код для себя и для всех, кто может заинтересоваться вашим проектом.
    Другие соглашения включают отступы в 4 пробела, комментарии и импорты. Настоятельно рекомендуется прочитать <a target="_blank" href="https://www.python.org/dev/peps/pep-0008/">PEP 8 -- Style Guide for Python Code</a>.
  </base-warning-content>
</base-warning>

Итак, как Python узнает, что мы хотим, чтобы наша функция принимала несколько аргументов и ключевых слов? Да, ответы — операторы `*` и `**`.

Теперь, когда мы рассмотрели основы, давайте поработаем с ними 👊.

## args

Мы уже знаем, как передавать несколько аргументов, используя `*args` в качестве параметра нашим функциям, но как с ними работать? Это просто: все аргументы находятся в переменной `args` в виде [кортежа](https://labex.io/pythoncheatsheet/ru/#Tuple-Data-Type):

```python
def some_function(*args):
    print(f'Arguments passed: {args} as {type(args)}')


some_function('arg1', 'arg2', 'arg3')
# Arguments passed: ('arg1', 'arg2', 'arg3') as <class 'tuple'>
```

Мы можем перебирать их:

```python
def some_function(*args):
    for a in args:
        print(a)


some_function('arg1', 'arg2', 'arg3')
# arg1
# arg2
# arg3
```

Получить доступ к элементам по индексу:

```python
def some_function(*args):
    print(args[1])


some_function('arg1', 'arg2', 'arg3')  # arg2
```

Срез:

```python
def some_function(*args):
    print(args[0:2])


some_function('arg1', 'arg2', 'arg3')
# ('arg1', 'arg2')
```

Все, что вы можете делать с [кортежем](https://labex.io/pythoncheatsheet/ru/#Tuple-Data-Type), вы можете делать и с `args`.

## kwargs

В то время как аргументы находятся в переменной args, ключевые слова находятся в `kwargs`, но на этот раз в виде [словаря](https://labex.io/pythoncheatsheet/ru/#Dictionaries-and-Structuring-Data), где ключ — это ключевое слово:

```python
def some_function(**kwargs):
    print(f'keywords: {kwargs} as {type(kwargs)}')


some_function(key1='arg1', key2='arg2', key3='arg3')
# keywords: {'key1': 'arg1', 'key2': 'arg2', 'key3': 'arg3'} as <class 'dict'>
```

Опять же, мы можем делать с `kwargs` то же самое, что и с любым [словарем](https://labex.io/pythoncheatsheet/ru/#Dictionaries-and-Structuring-Data).

Перебор:

```python
def some_function(**kwargs):
    for key, value in kwargs.items():
        print(f'{key}: {value}')


some_function(key1='arg1', key2='arg2', key3='arg3')
# key1: arg1
# key2: arg2
# key3: arg3
```

Использование метода `get()`:

```python
def some_function(key, **kwargs):
    print(kwargs.get(key))


some_function('key3', key1='arg1', key2='arg2', key3='arg3')
# arg3
```

И многое [другое](https://labex.io/pythoncheatsheet/ru/#Dictionaries-and-Structuring-Data) =).

## Заключение

`*args` и `**kwargs` могут показаться пугающими, но правда в том, что их не так уж сложно понять, и они дают вашим функциям большую гибкость. Если вы знаете о [кортежах](https://labex.io/pythoncheatsheet/ru/#Tuple-Data-Type) и [словарях](https://labex.io/pythoncheatsheet/ru/#Dictionaries-and-Structuring-Data), вы готовы к работе.

Хотите поиграть с args и kwargs? [Этот](https://mybinder.org/v2/gh/labex-labs/python-cheatsheet/master?filepath=jupyter_notebooks) онлайн-блокнот Jupyter Notebook для вас, чтобы попробовать.

Некоторые примеры используют `f-strings`, относительно новый способ форматирования строк в Python 3.6+. [Здесь](https://labex.io/pythoncheatsheet/ru/#Formatted-String-Literals-or-f-strings) вы можете прочитать о них больше.
