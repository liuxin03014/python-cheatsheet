---
title: 'args y kwargs en Python Simplificados - Hoja de Trucos'
description: 'args y kwargs pueden parecer intimidantes, pero son fáciles de entender y otorgan gran flexibilidad a tus funciones.'
date: 'March 08, 2019'
updated: 'July 1, 2022'
tags: 'python, intermediate'
socialImage: '/blog/kwargs.jpg'
layout: 'article'
---

<route lang="yaml">
meta:
    layout: "article"
    title: "args y kwargs en Python Simplificados - Hoja de Trucos"
    description: "args y kwargs pueden parecer intimidantes, pero son fáciles de entender y otorgan gran flexibilidad a tus funciones."
    date: "March 08, 2019"
    updated: "July 1, 2022"
    tags: "python, intermediate"
    socialImage: "/blog/kwargs.jpg"
</route>

<blog-title-header :frontmatter="frontmatter" title="args y kwargs en Python Simplificados - Hoja de Trucos" />

No sé ustedes, pero cada vez que veía alguna función con `*args` y `**kwargs` como parámetros, me daba un poco de miedo. Incluso las he "usado" mientras hacía algo de trabajo de backend con Django sin entender nada. Si eres un desarrollador autodidacta como yo, sé que tú también has estado ahí.

Hace unos meses, decidí dejar de ser perezoso y comencé a investigar. Para mi sorpresa, eran fáciles de entender cuando jugaba con el intérprete, pero no tanto al leer sobre ellos. Escribí esta publicación tratando de explicar [args y kwargs](https://labex.io/pythoncheatsheet/es/#args-and-kwargs) de la manera en que me hubiera gustado que alguien me los explicara.

## Conceptos Básicos

Lo primero que necesitas saber es que `*args` y `**kwargs` te permiten pasar un número indefinido de `arguments` (argumentos) y `keywords` (palabras clave) al llamar a una [function](https://labex.io/pythoncheatsheet/es/#Functions):

```python
def some_function(*args, **kwargs):
    pass

# llama a some_function con cualquier número de argumentos
some_function(arg1, arg2, arg3)

# llama a some_function con cualquier número de palabras clave
some_function(key1=arg1, key2=arg2, key3=arg3)

# llama a ambos, argumentos y palabras clave
some_function(arg, key1=arg1)

# o ninguno
some_function()
```

Segundo, las palabras `args` y `kwargs` son convenciones. Esto significa que no son impuestas por el intérprete, sino consideradas buenas prácticas entre la comunidad de Python:

```python
# Esta función funcionaría perfectamente
def some_function(*arguments, **keywords):
    pass
```

<base-warning>
  <base-warning-title>
    Una nota sobre las convenciones
  </base-warning-title>
  <base-warning-content>
    Incluso si la función anterior funciona, no lo hagas. Las convenciones están ahí para ayudarte a escribir código legible para ti y para cualquiera que pueda estar interesado en tu proyecto.
    Otras convenciones incluyen la indentación de 4 espacios, comentarios e imports. Se recomienda encarecidamente leer el <a target="_blank" href="https://www.python.org/dev/peps/pep-0008/">PEP 8 -- Style Guide for Python Code</a>.
  </base-warning-content>
</base-warning>

Entonces, ¿cómo sabe Python que queremos que nuestra función acepte múltiples argumentos y palabras clave? Sí, las respuestas son los operadores `*` y `**`.

Ahora que hemos cubierto lo básico, trabajemos con ellos 👊.

## args

Ahora sabemos cómo pasar múltiples argumentos usando `*args` como parámetro a nuestras funciones, pero ¿cómo trabajamos con ellos? Es fácil: todos los argumentos están dentro de la variable `args` como una [tuple](https://labex.io/pythoncheatsheet/es/#Tuple-Data-Type):

```python
def some_function(*args):
    print(f'Arguments passed: {args} as {type(args)}')


some_function('arg1', 'arg2', 'arg3')
# Arguments passed: ('arg1', 'arg2', 'arg3') as <class 'tuple'>
```

Podemos iterar sobre ellos:

```python
def some_function(*args):
    for a in args:
        print(a)


some_function('arg1', 'arg2', 'arg3')
# arg1
# arg2
# arg3
```

Acceder a los elementos con un índice:

```python
def some_function(*args):
    print(args[1])


some_function('arg1', 'arg2', 'arg3')  # arg2
```

Slicing:

```python
def some_function(*args):
    print(args[0:2])


some_function('arg1', 'arg2', 'arg3')
# ('arg1', 'arg2')
```

Todo lo que hagas con una [tuple](https://labex.io/pythoncheatsheet/es/#Tuple-Data-Type), puedes hacerlo con `args`.

## kwargs

Mientras que los argumentos están en la variable args, las palabras clave están dentro de `kwargs`, pero esta vez como un [dictionary](https://labex.io/pythoncheatsheet/es/#Dictionaries-and-Structuring-Data) donde la clave es la palabra clave:

```python
def some_function(**kwargs):
    print(f'keywords: {kwargs} as {type(kwargs)}')


some_function(key1='arg1', key2='arg2', key3='arg3')
# keywords: {'key1': 'arg1', 'key2': 'arg2', 'key3': 'arg3'} as <class 'dict'>
```

De nuevo, podemos hacer con `kwargs` lo mismo que haríamos con cualquier [dictionary](https://labex.io/pythoncheatsheet/es/#Dictionaries-and-Structuring-Data).

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

Usar el método `get()`:

```python
def some_function(key, **kwargs):
    print(kwargs.get(key))


some_function('key3', key1='arg1', key2='arg2', key3='arg3')
# arg3
```

Y mucho [más](https://labex.io/pythoncheatsheet/es/#Dictionaries-and-Structuring-Data) =).

## Conclusión

`*args` y `**kwargs` pueden parecer aterradores, pero la verdad es que no son tan difíciles de entender y tienen el poder de otorgar a tus funciones mucha flexibilidad. Si conoces las [tuples](https://labex.io/pythoncheatsheet/es/#Tuple-Data-Type) y los [dictionaries](https://labex.io/pythoncheatsheet/es/#Dictionaries-and-Structuring-Data), estás listo para empezar.

¿Quieres jugar con args y kwargs? [Este](https://mybinder.org/v2/gh/labex-labs/python-cheatsheet/master?filepath=jupyter_notebooks) es un Jupyter Notebook en línea para que lo intentes.

Algunos ejemplos hacen uso de "f-strings", una forma relativamente nueva de formatear cadenas en Python 3.6+. [Aquí](https://labex.io/pythoncheatsheet/es/#Formatted-String-Literals-or-f-strings) puedes leer más al respecto.
