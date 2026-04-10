---
title: 'Python *args e **kwargs Simplificados - Guia Rápido Python'
description: '*args e kwargs podem parecer intimidantes, mas na verdade não são difíceis de entender e dão muita flexibilidade às suas funções.'
date: 'March 08, 2019'
updated: 'July 1, 2022'
tags: 'python, intermediate'
socialImage: '/blog/kwargs.jpg'
layout: 'article'
---

<route lang="yaml">
meta:
    layout: "article"
    title: "Python *args e **kwargs Simplificados - Guia Rápido Python"
    description: "*args e kwargs podem parecer intimidantes, mas na verdade não são difíceis de entender e dão muita flexibilidade às suas funções."
    date: "March 08, 2019"
    updated: "July 1, 2022"
    tags: "python, intermediate"
    socialImage: "/blog/kwargs.jpg"
</route>

<blog-title-header :frontmatter="frontmatter" title="Python \*args e \*\*kwargs Simplificados - Guia Rápido Python" />

Eu não sei sobre você, mas toda vez que eu via alguma função com `*args` e `**kwargs` como parâmetros, eu ficava um pouco assustado. Eu até "usei" eles ao fazer algum trabalho de backend com Django sem entender nada. Se você é um desenvolvedor autodidata como eu, sei que você já passou por isso também.

Alguns meses atrás, decidi parar de ser preguiçoso e comecei a pesquisar sobre isso. Para minha surpresa, eles eram fáceis de entender ao brincar com o interpretador, mas não tanto ao ler sobre eles. Escrevi esta postagem tentando explicar [args e kwargs](https://labex.io/pythoncheatsheet/pt/#args-and-kwargs) da maneira que eu gostaria que alguém tivesse me explicado.

## Fundamentos

A primeira coisa que você precisa saber é que `*args` e `**kwargs` permitem que você passe um número indefinido de `arguments` e `keywords` ao chamar uma [function](https://labex.io/pythoncheatsheet/pt/#Functions):

```python
def some_function(*args, **kwargs):
    pass

# chama some_function com qualquer número de argumentos
some_function(arg1, arg2, arg3)

# chama some_function com qualquer número de palavras-chave
some_function(key1=arg1, key2=arg2, key3=arg3)

# chama ambos, argumentos e palavras-chave
some_function(arg, key1=arg1)

# ou nenhum
some_function()
```

Em segundo lugar, as palavras `args` e `kwargs` são convenções. Isso significa que elas não são impostas pelo interpretador, mas são consideradas boas práticas na comunidade Python:

```python
# Esta função funcionaria perfeitamente
def some_function(*arguments, **keywords):
    pass
```

<base-warning>
  <base-warning-title>
    Uma nota sobre convenções
  </base-warning-title>
  <base-warning-content>
    Mesmo que a função acima funcione, não o faça. As convenções existem para ajudá-lo a escrever código legível para você e para qualquer pessoa que possa se interessar pelo seu projeto.
    Outras convenções incluem a indentação de 4 espaços, comentários e imports. Ler o <a target="_blank" href="https://www.python.org/dev/peps/pep-0008/">PEP 8 -- Style Guide for Python Code</a> é altamente recomendado.
  </base-warning-content>
</base-warning>

Então, como o Python sabe que queremos que nossa função aceite múltiplos argumentos e palavras-chave? Sim, as respostas são os operadores `*` e `**`.

Agora que cobrimos os fundamentos, vamos trabalhar com eles 👊.

## args

Agora sabemos como passar múltiplos argumentos usando `*args` como um parâmetro para nossas funções, mas como trabalhamos com eles? É fácil: todos os argumentos estão dentro da variável `args` como uma [tuple](https://labex.io/pythoncheatsheet/pt/#Tuple-Data-Type):

```python
def some_function(*args):
    print(f'Arguments passed: {args} as {type(args)}')


some_function('arg1', 'arg2', 'arg3')
# Arguments passed: ('arg1', 'arg2', 'arg3') as <class 'tuple'>
```

Podemos iterar sobre eles:

```python
def some_function(*args):
    for a in args:
        print(a)


some_function('arg1', 'arg2', 'arg3')
# arg1
# arg2
# arg3
```

Acessar os elementos com um índice:

```python
def some_function(*args):
    print(args[1])


some_function('arg1', 'arg2', 'arg3')  # arg2
```

Fatiamento (Slice):

```python
def some_function(*args):
    print(args[0:2])


some_function('arg1', 'arg2', 'arg3')
# ('arg1', 'arg2')
```

Tudo o que você faz com uma [tuple](https://labex.io/pythoncheatsheet/pt/#Tuple-Data-Type), você pode fazer com `args`.

## kwargs

Enquanto os argumentos estão na variável args, as palavras-chave estão dentro de `kwargs`, mas desta vez como um [dictionary](https://labex.io/pythoncheatsheet/pt/#Dictionaries-and-Structuring-Data) onde a chave é a palavra-chave:

```python
def some_function(**kwargs):
    print(f'keywords: {kwargs} as {type(kwargs)}')


some_function(key1='arg1', key2='arg2', key3='arg3')
# keywords: {'key1': 'arg1', 'key2': 'arg2', 'key3': 'arg3'} as <class 'dict'>
```

Novamente, podemos fazer com `kwargs` o mesmo que faríamos com qualquer [dictionary](https://labex.io/pythoncheatsheet/pt/#Dictionaries-and-Structuring-Data).

Iterar sobre:

```python
def some_function(**kwargs):
    for key, value in kwargs.items():
        print(f'{key}: {value}')


some_function(key1='arg1', key2='arg2', key3='arg3')
# key1: arg1
# key2: arg2
# key3: arg3
```

Usar o método `get()`:

```python
def some_function(key, **kwargs):
    print(kwargs.get(key))


some_function('key3', key1='arg1', key2='arg2', key3='arg3')
# arg3
```

E muito [mais](https://labex.io/pythoncheatsheet/pt/#Dictionaries-and-Structuring-Data) =).

## Conclusão

`*args` e `**kwargs` podem parecer assustadores, mas a verdade é que eles não são tão difíceis de entender e têm o poder de conceder muita flexibilidade às suas funções. Se você conhece [tuples](https://labex.io/pythoncheatsheet/pt/#Tuple-Data-Type) e [dictionaries](https://labex.io/pythoncheatsheet/pt/#Dictionaries-and-Structuring-Data), você está pronto para começar.

Quer brincar com args e kwargs? [Este](https://mybinder.org/v2/gh/labex-labs/python-cheatsheet/master?filepath=jupyter_notebooks) é um Jupyter Notebook online para você experimentar.

Alguns exemplos fazem uso de `f-strings`, uma maneira relativamente nova de formatar strings no Python 3.6+. [Aqui](https://labex.io/pythoncheatsheet/pt/#Formatted-String-Literals-or-f-strings) você pode ler mais sobre isso.
