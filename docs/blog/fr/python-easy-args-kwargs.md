---
title: 'Les *args et **kwargs en Python Simplifiés - Fiche Mémo Python'
description: 'Les args et kwargs peuvent sembler intimidants, mais ils sont faciles à maîtriser et offrent une grande flexibilité à vos fonctions.'
date: 'March 08, 2019'
updated: 'July 1, 2022'
tags: 'python, intermediate'
socialImage: '/blog/kwargs.jpg'
layout: 'article'
---

<route lang="yaml">
meta:
    layout: "article"
    title: "Les *args et **kwargs en Python Simplifiés - Fiche Mémo Python"
    description: "Les args et kwargs peuvent sembler intimidants, mais ils sont faciles à maîtriser et offrent une grande flexibilité à vos fonctions."
    date: "March 08, 2019"
    updated: "July 1, 2022"
    tags: "python, intermediate"
    socialImage: "/blog/kwargs.jpg"
</route>

<blog-title-header :frontmatter="frontmatter" title="Les \*args et \*\*kwargs en Python Simplifiés - Fiche Mémo Python" />

Je ne sais pas pour vous, mais chaque fois que je voyais une fonction avec `*args` et `**kwargs` comme paramètres, j'avais un peu peur. J'ai même "utilisé" ces concepts en faisant du travail backend avec Django sans rien comprendre. Si vous êtes un développeur autodidacte comme moi, je sais que vous êtes passé par là aussi.

Il y a quelques mois, j'ai décidé d'arrêter d'être paresseux et j'ai commencé à faire des recherches. À ma grande surprise, ils étaient faciles à saisir en jouant avec l'interpréteur, mais pas autant en lisant à leur sujet. J'ai écrit cet article pour essayer d'expliquer [args et kwargs](https://labex.io/pythoncheatsheet/fr/#args-and-kwargs) de la manière dont j'aurais aimé qu'on me les explique.

## Bases

La première chose que vous devez savoir est que `*args` et `**kwargs` vous permettent de passer un nombre indéfini d'`arguments` et de `mots-clés` lors de l'appel d'une [fonction](https://labex.io/pythoncheatsheet/fr/#Functions) :

```python
def some_function(*args, **kwargs):
    pass

# appeler some_function avec n'importe quel nombre d'arguments
some_function(arg1, arg2, arg3)

# appeler some_function avec n'importe quel nombre de mots-clés
some_function(key1=arg1, key2=arg2, key3=arg3)

# appeler les deux, arguments et mots-clés
some_function(arg, key1=arg1)

# ou aucun
some_function()
```

Deuxièmement, les mots `args` et `kwargs` sont des conventions. Cela signifie qu'ils ne sont pas imposés par l'interpréteur, mais considérés comme une bonne pratique au sein de la communauté Python :

```python
# Cette fonction fonctionnerait très bien
def some_function(*arguments, **keywords):
    pass
```

<base-warning>
  <base-warning-title>
    Une note sur les conventions
  </base-warning-title>
  <base-warning-content>
    Même si la fonction ci-dessus fonctionne, ne le faites pas. Les conventions sont là pour vous aider à écrire du code lisible pour vous et pour quiconque pourrait être intéressé par votre projet.
    D'autres conventions incluent l'indentation de 4 espaces, les commentaires et les imports. Lire le <a target="_blank" href="https://www.python.org/dev/peps/pep-0008/">PEP 8 -- Style Guide for Python Code</a> est fortement recommandé.
  </base-warning-content>
</base-warning>

Alors, comment Python sait-il que nous voulons que notre fonction accepte plusieurs arguments et mots-clés ? Oui, les réponses sont les opérateurs `*` et `**`.

Maintenant que nous avons couvert les bases, travaillons avec eux 👊.

## args

Nous savons maintenant comment passer plusieurs arguments en utilisant `*args` comme paramètre à nos fonctions, mais comment travailler avec eux ? C'est facile : tous les arguments se trouvent dans la variable `args` sous forme de [tuple](https://labex.io/pythoncheatsheet/fr/#Tuple-Data-Type) :

```python
def some_function(*args):
    print(f'Arguments passés: {args} en tant que {type(args)}')


some_function('arg1', 'arg2', 'arg3')
# Arguments passés: ('arg1', 'arg2', 'arg3') en tant que <class 'tuple'>
```

Nous pouvons itérer dessus :

```python
def some_function(*args):
    for a in args:
        print(a)


some_function('arg1', 'arg2', 'arg3')
# arg1
# arg2
# arg3
```

Accéder aux éléments avec un index :

```python
def some_function(*args):
    print(args[1])


some_function('arg1', 'arg2', 'arg3')  # arg2
```

Trancher (Slice) :

```python
def some_function(*args):
    print(args[0:2])


some_function('arg1', 'arg2', 'arg3')
# ('arg1', 'arg2')
```

Tout ce que vous faites avec un [tuple](https://labex.io/pythoncheatsheet/fr/#Tuple-Data-Type), vous pouvez le faire avec `args`.

## kwargs

Alors que les arguments sont dans la variable args, les mots-clés sont dans `kwargs`, mais cette fois sous forme de [dictionnaire](https://labex.io/pythoncheatsheet/fr/#Dictionaries-and-Structuring-Data) où la clé est le mot-clé :

```python
def some_function(**kwargs):
    print(f'mots-clés: {kwargs} en tant que {type(kwargs)}')


some_function(key1='arg1', key2='arg2', key3='arg3')
# mots-clés: {'key1': 'arg1', 'key2': 'arg2', 'key3': 'arg3'} en tant que <class 'dict'>
```

Encore une fois, nous pouvons faire avec `kwargs` la même chose que nous ferions avec n'importe quel [dictionnaire](https://labex.io/pythoncheatsheet/fr/#Dictionaries-and-Structuring-Data).

Itérer sur :

```python
def some_function(**kwargs):
    for key, value in kwargs.items():
        print(f'{key}: {value}')


some_function(key1='arg1', key2='arg2', key3='arg3')
# key1: arg1
# key2: arg2
# key3: arg3
```

Utiliser la méthode `get()` :

```python
def some_function(key, **kwargs):
    print(kwargs.get(key))


some_function('key3', key1='arg1', key2='arg2', key3='arg3')
# arg3
```

Et bien [plus](https://labex.io/pythoncheatsheet/fr/#Dictionaries-and-Structuring-Data) =).

## Conclusion

`*args` et `**kwargs` peuvent sembler effrayants, mais la vérité est qu'ils ne sont pas si difficiles à saisir et ont le pouvoir de doter vos fonctions de beaucoup de flexibilité. Si vous connaissez les [tuples](https://labex.io/pythoncheatsheet/fr/#Tuple-Data-Type) et les [dictionnaires](https://labex.io/pythoncheatsheet/fr/#Dictionaries-and-Structuring-Data), vous êtes prêt à partir.

Vous voulez jouer avec args et kwargs ? [Ceci](https://mybinder.org/v2/gh/labex-labs/python-cheatsheet/master?filepath=jupyter_notebooks) est un Jupyter Notebook en ligne pour que vous puissiez essayer.

Certains exemples utilisent des `f-strings`, une manière relativement nouvelle de formater des chaînes en Python 3.6+. [Ici](https://labex.io/pythoncheatsheet/fr/#Formatted-String-Literals-or-f-strings) vous pouvez en lire plus à ce sujet.
