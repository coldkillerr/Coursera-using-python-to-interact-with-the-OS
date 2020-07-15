<h1> Regular Expressions </h1>

<h2> Definition </h2>

A regular expression, also known as regex or regexp,
is essentially a search query for text that's expressed by string pattern.
When you run a search against a particular piece of text,
anything that matches a regular expression pattern you specified,
is returned as a result of the search. 

Regular expressions allow us to search for strings matching specific pattern in a text block .

Module used :  `re`

<h2> Using grep </h2>



`grep` works by printing
out any line that matches the query that we pass it.
So for a simplest query of passing a plain old string,
grep will print any lines
containing that string in the file that we give it.

```shell

nishit  SHITBOT  ~  grep thon /usr/share/dict/words

Anthony
Anthony's
Johnathon
Johnathon's
Jonathon
Jonathon's
Marathon
Marathon's
Phaethon
Phaethon's
Python
Python's
diphthong
diphthong's
diphthongs
marathon
marathon's
marathoner
marathoner's
marathoners
marathons
python
python's
pythons
telethon
telethon's
telethons
thong
thong's
thongs
```

`grep` is case sensitive . If we want to match with all cases (upper , lower , mixed ) , you should use `-i`

```shell
nishit  SHITBOT  ~  grep python /usr/share/dict/words -i

Python
Python's
python
python's
pythons
```
<h3> Reserved Characters </h3>

It's these characters that allow us to do more
advanced matching than just
checking for a literal string. 

For example, a dot(`.`) matches any character.

```shell
nishit  SHITBOT  ~  grep p.th.n /usr/share/dict/words -i
Python
Python's
diphthong
diphthong's
diphthongs
python
python's
pythons
```

Other easy examples of
special characters that we can use in
a irregular expressions are the caret,
or circumflex and the dollar sign anchor characters.
These tell us where in the line
the regex should match from.
The circumflex (`^`) indicates the beginning (finding patterns that starts-with)
and the dollar sign (`$`) indicates the end of the line (finding patterns that ends-with). 

```shell
nishit  SHITBOT  ~  grep ^fruit /usr/share/dict/words -i
fruit
fruit's
fruitcake
fruitcake's
fruitcakes
fruited
fruitful
fruitfully
fruitfulness
fruitfulness's
fruitier
fruitiest
fruiting
fruition
fruition's
fruitless
fruitlessly
fruitlessness
fruitlessness's
fruits
fruity
```
```shell
nishit  SHITBOT  ~  grep fruit$ /usr/share/dict/words -i
breadfruit
fruit
grapefruit
```
<h2> Using search() </h2>

```python3
>>> result=re.search(r'aza','plaza')
>>> print(result)
<re.Match object; span=(2, 5), match='aza'>
>>> 
```

The `re.search()` function returns the span and match if the match is found in the target text.
The span can be found using `result.span()` method.

```python3
>>> print(result.span())
(2, 5)
>>> 
```
The result is `None` if match is not found
```python3
>>> result=re.search(r'aze','plaza')
>>> print(result)
None
>>> 
```
<h3> Matching using special characters </h3>

```python3
>>> print(re.search(r'^a' , 'apple'))
<re.Match object; span=(0, 1), match='a'>
>>> print(re.search(r'a$' , 'ba'))
<re.Match object; span=(1, 2), match='a'>
>>> print(re.search(r'a.' , 'apple'))
<re.Match object; span=(0, 2), match='ap'>
>>> print(re.search(r'a..' , 'apple'))
<re.Match object; span=(0, 3), match='app'>
>>> 
```

If we want the match to be insensitive use `re.IGNORECASE` in the `re.search()` function.

```python3
>>> print(re.search(r'a..l' , 'Apple',re.IGNORECASE))
<re.Match object; span=(0, 4), match='Appl'>
>>> 
```

<h3> Character Classes </h3>

Character classes are written inside square brackets and
let us list the characters we want to match inside of those brackets. 

Example :
```python3
>>> re.search(r'[aA]way','the away is k')
<re.Match object; span=(4, 8), match='away'>
>>> 
```

Inside the square brackets, we can also define a range of characters using a dash.

Example :
```python3
>>> re.search(r'[a-z]way','the sway is k')
<re.Match object; span=(4, 8), match='sway'>
>>> re.search(r'[a-z]way','the tway is k')
<re.Match object; span=(4, 8), match='tway'>
>>> re.search(r'[a-u]way','the tway is k')
<re.Match object; span=(4, 8), match='tway'>
```
We can also search for multiple character classes at a time.

Example :
```python3
>>> re.search(r'[a-zA-Z]way','the tway is k')
<re.Match object; span=(4, 8), match='tway'>
>>> re.search(r'[a-zA-Z]way','the Tway is k')
<re.Match object; span=(4, 8), match='Tway'>
>>> re.search(r'[a-zA-Z]way','the Sway is k')
<re.Match object; span=(4, 8), match='Sway'>
>>> re.search(r'cloud[A-Z0-9a-z]','cloudy')
<re.Match object; span=(0, 6), match='cloudy'>
>>> re.search(r'cloud[A-Z0-9a-z]','cloud9')
<re.Match object; span=(0, 6), match='cloud9'>
>>> 
```
We can also match any characters that aren't in a group.
To do that, we use a circumflex (`^`) inside the square brackets.

Example :

```python
>>> print(re.search(r'cloud[^A-Z]','cloudy cloud9'))
<re.Match object; span=(0, 6), match='cloudy'>
>>> print(re.search(r'cloud[^0-9]','cloudy cloud9'))
<re.Match object; span=(0, 6), match='cloudy'>
>>> 
```
The pipe `|` lets us match the text with one out of many options (it acts like an or).
Example:

```python3
>>> print(re.search(r'cat|dog','I like cats'))
<re.Match object; span=(7, 10), match='cat'>
>>> print(re.search(r'cat|dog','I like dogss'))
<re.Match object; span=(7, 10), match='dog'>
>>> print(re.search(r'cat|dog|snake','I like snakes'))
<re.Match object; span=(7, 12), match='snake'>
>>> 
```
The search function finds only the first instance of a match . 

```python3
>>> print(re.search(r'cat|dog|snake','I like cats, dogs, and snakes'))
<re.Match object; span=(7, 10), match='cat'>
>>> 
```

But if we use the `findall()` function it finds all matches from a text .

```python3
>>> print(re.findall(r'cat|dog|snake','I like cats, dogs, and snakes'))
['cat', 'dog', 'snake']
```

<h3> Repetition Qualifiers </h3>

Repetition qualifiers are used to match a character multiple times . For this we use repeated matches. A dot `.` followed by a `*` means that it matches any character repeated as many times as possible including zero. 

Example :

```python3
>>> print(re.search(r'py.*n','I like python'))
<re.Match object; span=(7, 13), match='python'>
>>> print(re.search(r'py.*n','I like pythonian'))
<re.Match object; span=(7, 16), match='pythonian'>
```
The Star takes as many characters as possible.
In programming terms, we
say that this behavior is greedy. 

