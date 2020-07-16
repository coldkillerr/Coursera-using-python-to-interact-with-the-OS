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

If we wanted the pattern to match a specific class we should've used a character class instead.

For eg.

```python
>>> print(re.search(r'py[a-z]*n','I like pythonian'))
<re.Match object; span=(7, 16), match='pythonian'>
>>> print(re.search(r'py[a-z]*n','I like pyn'))
<re.Match object; span=(7, 10), match='pyn'>
>>> 

```
<b>Note : As we see in the above example the pattern matches for any number of times even zero.</b>

The plus `+` character matches
one or more occurrences
of the character that comes before it.

Example :

```python3
>>> print(re.search(r'o+n+','I like pythoooonian'))
<re.Match object; span=(11, 16), match='oooon'>
>>> print(re.search(r'o+n+','oooonnnnnoooooonnnn'))
<re.Match object; span=(0, 9), match='oooonnnnn'>
>>> print(re.findall(r'o+n+','oooonnnnnoooooonnnn'))
['oooonnnnn', 'oooooonnnn']
>>> 
```

The question mark `?` qualifier matches for either zero or
one occurrence of the character before it

```python3
 >>> print(re.search(r'p?each','I like ppeaches'))
<re.Match object; span=(8, 13), match='peach'>
>>> print(re.search(r'p?each','I like each'))
<re.Match object; span=(7, 11), match='each'>
>>> 
```
<h3> Matching Special Characaters </h3>

We can match special characters using backslash `\`
Example :

```python3
>>> print(re.search(r'\.com','github.com'))
<re.Match object; span=(6, 10), match='.com'>
<re.Match object; span=(6, 10), match='.com'>
>>> print(re.search(r'\*com','A star*com'))
<re.Match object; span=(6, 10), match='*com'>
>>> print(re.search(r'\?com','A question mark ?*com'))
None
>>> print(re.search(r'\?com','A question mark ?com'))
<re.Match object; span=(16, 20), match='?com'>
>>> 

```
<b>Note : When we see a pattern that includes a backslash,
it could be escaping a special regex character
or a special string character. </b> 

Using raw strings, like we've been doing,
helps avoid some of these possible confusion because
the special characters won't be
interpreted when generating the string.
They will only be interpreted
when parsing the regular expression.

Python also uses the backslash `\` for
a few special sequences that we can use
to represent predefined sets of characters.
For example, `\w` matches
any alphanumeric character including
letters, numbers, and underscores. 

```python3
>>> print(re.search(r'\w.*','An example'))
<re.Match object; span=(0, 10), match='An example'>
>>> print(re.search(r'\w.*','Another_example'))
<re.Match object; span=(0, 15), match='Another_example'>
>>> print(re.search(r'\w.','Another_example'))
<re.Match object; span=(0, 2), match='An'>
>>> print(re.search(r'\w','Another_example'))
<re.Match object; span=(0, 1), match='A'>
>>> 
```
There's also `\d` for `matching digits`,
`\s` for `matching whitespace characters` like space,
tab or new line,
`\b` for `word boundaries` and a few others. 

<h3> Use of regex irl </h3>

```python
>>> pattern=r"^[A-Za-z_].*$"
>>> print(re.search(pattern,'this_is_a_valid_variable_name'))
<re.Match object; span=(0, 29), match='this_is_a_valid_variable_name'>
>>> print(re.search(pattern,'9this_is_a_valid_variable_name'))
None
>>> print(re.search(pattern,'_this_is_a_valid_variable_name'))
<re.Match object; span=(0, 30), match='_this_is_a_valid_variable_name'>
>>> print(re.search(pattern,'_this is_a_valid_variable_name'))
<re.Match object; span=(0, 30), match='_this is_a_valid_variable_name'>
>>> pattern=r"^[A-Za-z_][A-Za-z0-9_]*$"
>>> print(re.search(pattern,'_this is_a_valid_variable_name'))
None
>>> 
```
In the above example I tried to make a regex for a valid variable name.

<h3> How to escape greedy behaviour </h3>

```python3
>>> s = '<html><head><title>Title</title>'
>>> len(s)
32
>>> print(re.match('<.*>', s).span())
(0, 32)
>>> print(re.match('<.*>', s).group())
<html><head><title>Title</title>
```

The RE matches the '<' in '<html>', and the .* consumes the rest of the string. In this case, the solution is to use the non-greedy qualifiers *?, +?, ??, or {m,n}?, which match as little text as possible. 
 
```python3
>>> print(re.match('<.*?>', s).group())
<html>
```
<h1> Advanced Regular Expressions </h1>

<h2> Capturing Groups </h2>

Capturing groups are portions of the pattern that are enclosed in parentheses.Capturing groups are portions of the pattern that are enclosed in parentheses.

Example :

```python
>>> result=(re.search(r'^(\w*), (\w*)$','Jain, Nishit'))
>>> print(result.group())
Jain, Nishit
>>> print(result[0])
Jain, Nishit
>>> print(result[1])
Jain
>>> print(result[2])
Nishit
>>> print('{} {}'.format(result[2],result[1])
... )
Nishit Jain
>>> 
```
<h2> Numeric Repetition Qualifiers </h2>

Python also offers numeric repetition qualifiers.
These are written between curly brackets and
can be one or two numbers specifying a range. 

Example :

```python
>>> print(re.search(r'[a-zA-Z]{3,6}','A GhOsT'))
<re.Match object; span=(2, 7), match='GhOsT'>
>>> print(re.search(r'[a-zA-Z]{3,6}','A GhOsTs'))
<re.Match object; span=(2, 8), match='GhOsTs'>
>>> print(re.search(r'[a-zA-Z]{3,6}','A big GhOsTs'))
<re.Match object; span=(2, 5), match='big'>
>>> 

```
In the above example the match is for a string of length in the range 3 to 6
