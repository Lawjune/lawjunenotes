
## snippets

.       - Any Character Except New Line
\d      - Digit (0-9)
\D      - Not a Digit (0-9)
\w      - Word Character (a-z, A-Z, 0-9, _)
\W      - Not a Word Character
\s      - Whitespace (space, tab, newline)
\S      - Not Whitespace (space, tab, newline)

\b      - Word Boundary
\B      - Not a Word Boundary
^       - Beginning of a String
$       - End of a String

[]      - Matches Characters in brackets
[^ ]    - Matches Characters NOT in brackets
|       - Either Or
( )     - Group

Quantifiers:
*       - 0 or More
+       - 1 or More
?       - 0 or One
{3}     - Exact Number
{3,4}   - Range of Numbers (Minimum, Maximum)


#### Sample Regexs ####

[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+

## Re Moduel and Raw string in Python

```python
import re

text_to_search = '''
abcdefghijklmnopqurtuvwxyz
ABCDEFGHIJKLMNOPQRSTUVWXYZ
1234567890

Ha HaHa

MetaCharacters (Need to be escaped):
. ^ $ * + ? { } [ ] \ | ( )

coreyms.com

321-555-4321
123.555.1234
123*555*1234
800-555-1234
900-555-1234

Mr. Schafer
Mr Smith
Ms Davis
Mrs. Robinson
Mr. T
'''

sentence = 'Start a sentence and then' \
		   'bring it to an end'
```

## Simple examples using re.compile and finditer

```python
pattern = re.compile(r'abc')

matches = pattern.finditer(text_to_search)

for match in matches:
    print(match)
```
output:
<re.Match object; span=(1, 4), match='abc'>


## Escaping special characters with a backslash

```python
pattern = re.compile(r'\.')
```
output:
<re.Match object; span=(113, 114), match='.'>
<re.Match object; span=(149, 150), match='.'>
<re.Match object; span=(171, 172), match='.'>
<re.Match object; span=(175, 176), match='.'>
<re.Match object; span=(223, 224), match='.'>
<re.Match object; span=(254, 255), match='.'>
<re.Match object; span=(267, 268), match='.'>

```python
pattern = re.compile(r'coreyms.com')
```
output
<re.Match object; span=(142, 153), match='coreyms.com'>

## Use regex to search for patterns. Use of meta-characters.

```python
pattern = re.compile(r'\d')
```
output
<re.Match object; span=(55, 56), match='1'>
<re.Match object; span=(56, 57), match='2'>
<re.Match object; span=(57, 58), match='3'>
<re.Match object; span=(58, 59), match='4'>
......
<re.Match object; span=(215, 216), match='1'>
<re.Match object; span=(216, 217), match='2'>
<re.Match object; span=(217, 218), match='3'>
<re.Match object; span=(218, 219), match='4'>


```python
pattern = re.compile(r'\D')
```
output
<re.Match object; span=(0, 1), match='\n'>
<re.Match object; span=(1, 2), match='a'>
<re.Match object; span=(2, 3), match='b'>
<re.Match object; span=(3, 4), match='c'>
......
<re.Match object; span=(267, 268), match='.'>
<re.Match object; span=(268, 269), match=' '>
<re.Match object; span=(269, 270), match='T'>
<re.Match object; span=(270, 271), match='\n'>

```python
pattern = re.compile(r'\w')
```
output
<re.Match object; span=(1, 2), match='a'>
<re.Match object; span=(2, 3), match='b'>
<re.Match object; span=(3, 4), match='c'>
<re.Match object; span=(4, 5), match='d'>
......
<re.Match object; span=(263, 264), match='n'>
<re.Match object; span=(265, 266), match='M'>
<re.Match object; span=(266, 267), match='r'>
<re.Match object; span=(269, 270), match='T'>


```python
pattern = re.compile(r'\W')
```
output
<re.Match object; span=(0, 1), match='\n'>
<re.Match object; span=(27, 28), match='\n'>
<re.Match object; span=(54, 55), match='\n'>
<re.Match object; span=(65, 66), match='\n'>
......
<re.Match object; span=(264, 265), match='\n'>
<re.Match object; span=(267, 268), match='.'>
<re.Match object; span=(268, 269), match=' '>
<re.Match object; span=(270, 271), match='\n'>


```python
pattern = re.compile(r'\s')
```
output
pycrawler/re_notes/simple.py
<re.Match object; span=(0, 1), match='\n'>
<re.Match object; span=(27, 28), match='\n'>
<re.Match object; span=(54, 55), match='\n'>
<re.Match object; span=(65, 66), match='\n'>
......
<re.Match object; span=(255, 256), match=' '>
<re.Match object; span=(264, 265), match='\n'>
<re.Match object; span=(268, 269), match=' '>
<re.Match object; span=(270, 271), match='\n'>


```python
pattern = re.compile(r'\S')
```
output
<re.Match object; span=(1, 2), match='a'>
<re.Match object; span=(2, 3), match='b'>
<re.Match object; span=(3, 4), match='c'>
<re.Match object; span=(4, 5), match='d'>
......
<re.Match object; span=(265, 266), match='M'>
<re.Match object; span=(266, 267), match='r'>
<re.Match object; span=(267, 268), match='.'>
<re.Match object; span=(269, 270), match='T'>


## Metacharacters continued. Anchors. Word boundaries.

```txt
Ha HaHa
```

```python
pattern = re.compile(r'\bHa')
```
output
<re.Match object; span=(67, 69), match='Ha'>
<re.Match object; span=(70, 72), match='Ha'>


```python
pattern = re.compile(r'\BHa')
```
output
<re.Match object; span=(72, 74), match='Ha'>

## Anchors continued. ^ and $

```python
sentence = 'Start a sentence and then bring it to an end'

pattern = re.compile(r'^Start')

# matches = pattern.finditer(text_to_search)
matches = pattern.finditer(sentence)

for match in matches:
    print(match)
```
output
<re.Match object; span=(0, 5), match='Start'>


```python
pattern = re.compile(r'^a')
```
*No matches!*

```python
pattern = re.compile(r'end$')
```
output
<re.Match object; span=(41, 44), match='end'>

```python
pattern = re.compile(r'a$')
```
*No matches!*


## Practical examples. Matching phone numbers of patterns 123-456-7890 or 123.456.7890

```txt
1234567890

Ha HaHa

MetaCharacters (Need to be escaped):
. ^ $ * + ? { } [ ] \ | ( )

coreyms.com

321-555-4321
123.555.1234
123*555*1234
800-555-1234
900-555-1234
```

## Precise matching using character-set

```python
pattern = re.compile(r'\d\d\d')
```
output
<re.Match object; span=(55, 58), match='123'>
<re.Match object; span=(58, 61), match='456'>
<re.Match object; span=(61, 64), match='789'>
<re.Match object; span=(155, 158), match='321'>
<re.Match object; span=(159, 162), match='555'>
<re.Match object; span=(163, 166), match='432'>
<re.Match object; span=(168, 171), match='123'>
<re.Match object; span=(172, 175), match='555'>
<re.Match object; span=(176, 179), match='123'>
<re.Match object; span=(181, 184), match='123'>
<re.Match object; span=(185, 188), match='555'>
<re.Match object; span=(189, 192), match='123'>
<re.Match object; span=(194, 197), match='800'>
<re.Match object; span=(198, 201), match='555'>
<re.Match object; span=(202, 205), match='123'>
<re.Match object; span=(207, 210), match='900'>
<re.Match object; span=(211, 214), match='555'>
<re.Match object; span=(215, 218), match='123'>

```python
pattern = re.compile(r'\d\d\d.\d\d\d.\d\d\d')
```
output
<re.Match object; span=(155, 166), match='321-555-432'>
<re.Match object; span=(168, 179), match='123.555.123'>
<re.Match object; span=(181, 192), match='123*555*123'>
<re.Match object; span=(194, 205), match='800-555-123'>
<re.Match object; span=(207, 218), match='900-555-123'>


## Character-set only matches one character in the set

```python
pattern = re.compile(r'\d\d\d[-.]\d\d\d[-.]\d\d\d')
```
output
<re.Match object; span=(155, 166), match='321-555-432'>
<re.Match object; span=(168, 179), match='123.555.123'>
<re.Match object; span=(194, 205), match='800-555-123'>
<re.Match object; span=(207, 218), match='900-555-123'>

## Match specific numbers. (800,900 phone numbers)

```python
pattern = re.compile(r'[89]00[-.]\d\d\d[-.]\d\d\d')
```
output
<re.Match object; span=(194, 205), match='800-555-123'>
<re.Match object; span=(207, 218), match='900-555-123'>

## Role of dash(-) within a character set. Used to specify ranges.

```python
pattern = re.compile(r'[1-5]')
```
```python
pattern = re.compile(r'[a-z]')
```
```python
pattern = re.compile(r'[A-Z]')
```
```python
pattern = re.compile(r'[a-zA-Z]')
```
```python
pattern = re.compile(r'[a-zA-Z1-5]')
```
output
<re.Match object; span=(1, 2), match='a'>
<re.Match object; span=(2, 3), match='b'>
<re.Match object; span=(3, 4), match='c'>
<re.Match object; span=(4, 5), match='d'>
......
<re.Match object; span=(26, 27), match='z'>
<re.Match object; span=(28, 29), match='A'>
<re.Match object; span=(29, 30), match='B'>
<re.Match object; span=(30, 31), match='C'>
......
<re.Match object; span=(53, 54), match='Z'>
<re.Match object; span=(55, 56), match='1'>
<re.Match object; span=(56, 57), match='2'>
<re.Match object; span=(57, 58), match='3'>
......


## Role of carets (^) within a character set. Used to negate.

```python
pattern = re.compile(r'[^a-zA-Z1-5]')
```
<re.Match object; span=(0, 1), match='\n'>
<re.Match object; span=(27, 28), match='\n'>
<re.Match object; span=(54, 55), match='\n'>
<re.Match object; span=(60, 61), match='6'>
<re.Match object; span=(61, 62), match='7'>
<re.Match object; span=(62, 63), match='8'>
<re.Match object; span=(63, 64), match='9'>
......



```txt
cat
mat
pat
bat
```

```python
pattern = re.compile(r'[^b]at')
```
output
<re.Match object; span=(272, 275), match='cat'>
<re.Match object; span=(276, 279), match='mat'>
<re.Match object; span=(280, 283), match='pat'>

## Use of quantifiers to match more than one character at once.

```python
pattern = re.compile(r'\d\d\d.\d\d\d.\d\d\d\d')
```
output
<re.Match object; span=(155, 167), match='321-555-4321'>
<re.Match object; span=(168, 180), match='123.555.1234'>
<re.Match object; span=(181, 193), match='123*555*1234'>
<re.Match object; span=(194, 206), match='800-555-1234'>
<re.Match object; span=(207, 219), match='900-555-1234'>


```snippets
Quantifiers:
*       - 0 or More
+       - 1 or More
?       - 0 or One
{3}     - Exact Number
{3,4}   - Range of Numbers (Minimum, Maximum)
```

```python
pattern = re.compile(r'\d{3}.\d{3}.\d{4}')
```
output(*same result*)
<re.Match object; span=(155, 167), match='321-555-4321'>
<re.Match object; span=(168, 180), match='123.555.1234'>
<re.Match object; span=(181, 193), match='123*555*1234'>
<re.Match object; span=(194, 206), match='800-555-1234'>
<re.Match object; span=(207, 219), match='900-555-1234'>


## Groups. Match several different patterns

```txt
Mr. Schafer
Mr Smith
Ms Davis
Mrs. Robinson
Mr. T
```

```python
pattern = re.compile(r'Mr\.')
```
output
<re.Match object; span=(221, 224), match='Mr.'>
<re.Match object; span=(265, 268), match='Mr.'>

```python
pattern = re.compile(r'Mr\.?')
```
output
<re.Match object; span=(221, 224), match='Mr.'>
<re.Match object; span=(233, 235), match='Mr'>
<re.Match object; span=(251, 253), match='Mr'>
<re.Match object; span=(265, 268), match='Mr.'>

```python
pattern = re.compile(r'Mr\.?\s[A-Z]')
```
output
<re.Match object; span=(221, 226), match='Mr. S'>
<re.Match object; span=(233, 237), match='Mr S'>
<re.Match object; span=(265, 270), match='Mr. T'>

```python
pattern = re.compile(r'Mr\.?\s[A-Z]\w+')
```
output
<re.Match object; span=(221, 232), match='Mr. Schafer'>
<re.Match object; span=(233, 241), match='Mr Smith'>

*There is no 'Mr T'*

```python
pattern = re.compile(r'Mr\.?\s[A-Z]\w*')
```
output
<re.Match object; span=(221, 232), match='Mr. Schafer'>
<re.Match object; span=(233, 241), match='Mr Smith'>
<re.Match object; span=(265, 270), match='Mr. T'>

```python
pattern = re.compile(r'M(r|s|rs)\.?\s[A-Z]\w*')
```
<re.Match object; span=(221, 232), match='Mr. Schafer'>
<re.Match object; span=(233, 241), match='Mr Smith'>
<re.Match object; span=(242, 250), match='Ms Davis'>
<re.Match object; span=(251, 264), match='Mrs. Robinson'>
<re.Match object; span=(265, 270), match='Mr. T'>

*Better comprehensive way*
```python
pattern = re.compile(r'(Mr|Ms|Mrs)\.?\s[A-Z]\w*')
```

## Recap of previous concepts with examples. Matching email addresses

```python
emails = '''
CoreyMSchafer@gmail.com
corey.schafer@university.edu
corey-321-schafer@my-work.net
'''

pattern = re.compile(r'[a-zA-Z]+')

matches = pattern.finditer(emails)

for match in matches:
    print(match)
```
output
<re.Match object; span=(1, 14), match='CoreyMSchafer'>
<re.Match object; span=(15, 20), match='gmail'>
<re.Match object; span=(21, 24), match='com'>
<re.Match object; span=(25, 30), match='corey'>
<re.Match object; span=(31, 38), match='schafer'>
<re.Match object; span=(39, 49), match='university'>
<re.Match object; span=(50, 53), match='edu'>
<re.Match object; span=(54, 59), match='corey'>
<re.Match object; span=(64, 71), match='schafer'>
<re.Match object; span=(72, 74), match='my'>
<re.Match object; span=(75, 79), match='work'>
<re.Match object; span=(80, 83), match='net'>


```python
pattern = re.compile(r'[a-zA-Z]+@[a-zA-Z]+')
```
output
<re.Match object; span=(1, 20), match='CoreyMSchafer@gmail'>
<re.Match object; span=(31, 49), match='schafer@university'>
<re.Match object; span=(64, 74), match='schafer@my'>


```python
pattern = re.compile(r'[a-zA-Z]+@[a-zA-Z]+\.com')
```
output
<re.Match object; span=(1, 24), match='CoreyMSchafer@gmail.com'>

```python
pattern = re.compile(r'[a-zA-Z.]+@[a-zA-Z]+\.(com|edu)')
```
<re.Match object; span=(1, 24), match='CoreyMSchafer@gmail.com'>
<re.Match object; span=(25, 53), match='corey.schafer@university.edu'>


## Deciphering existing regular expressions.

```python
pattern = re.compile(r'[a-zA-Z0-9.-]+@[a-zA-Z-]+\.(com|edu|net)')
```
<re.Match object; span=(1, 24), match='CoreyMSchafer@gmail.com'>
<re.Match object; span=(25, 53), match='corey.schafer@university.edu'>
<re.Match object; span=(54, 83), match='corey-321-schafer@my-work.net'>


```python
universal_email_pattern = \
    r'[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+'
pattern = re.compile(universal_email_pattern)

matches = pattern.finditer(emails)
```

## Capturing information from groups. The group method in the match object

```python
urls = '''
https://www.google.com
http://coreyms.com
https://youtube.com
https://www.nasa.gov
'''

pattern = re.compile(r'http')

matches = pattern.finditer(urls)

for match in matches:
    print(match)
```
output
<re.Match object; span=(1, 5), match='http'>
<re.Match object; span=(24, 28), match='http'>
<re.Match object; span=(43, 47), match='http'>
<re.Match object; span=(63, 67), match='http'>

```python
pattern = re.compile(r'https')
```
output
<re.Match object; span=(1, 6), match='https'>
<re.Match object; span=(43, 48), match='https'>
<re.Match object; span=(63, 68), match='https'>


```
?       - 0 or One
```

```python
pattern = re.compile(r'https?')
```
output
<re.Match object; span=(1, 6), match='https'>
<re.Match object; span=(24, 28), match='http'>
<re.Match object; span=(43, 48), match='https'>
<re.Match object; span=(63, 68), match='https'>

```python
pattern = re.compile(r'https?://(www\.)?')
```
output
<re.Match object; span=(1, 13), match='https://www.'>
<re.Match object; span=(24, 31), match='http://'>
<re.Match object; span=(43, 51), match='https://'>
<re.Match object; span=(63, 75), match='https://www.'>

```python
pattern = re.compile(r'https?://(www\.)?\w+\.\w+')
```
output
<re.Match object; span=(1, 23), match='https://www.google.com'>
<re.Match object; span=(24, 42), match='http://coreyms.com'>
<re.Match object; span=(43, 62), match='https://youtube.com'>
<re.Match object; span=(63, 83), match='https://www.nasa.gov'>


## Back reference to reference the captured group. Sub method to perform substitution


**Groupping**
```python
pattern = re.compile(r'https?://(www\.)?(\w+)(\.\w+)')
```

```python
for match in matches:
    print(match)
```
*Same result*

```python
for match in matches:
    print(match.group(0))
```
output
https://www.google.com
http://coreyms.com
https://youtube.com
https://www.nasa.gov

```python
for match in matches:
    print(match.group(1))
```
output
www.
None
None
www.


```python
for match in matches:
    print(match.group(2))
```
output
google
coreyms
youtube
nasa

```python
for match in matches:
    print(match.group(3))
```
.com
.com
.com
.gov

```python
subbed_urls = pattern.sub(r'\2\3', urls)

print(subbed_urls)
```
output
google.com
coreyms.com
youtube.com
nasa.gov

## findall method. Just returns the matches as a list of strings

```python
pattern = re.compile(r'(Mr|Ms|Mrs)\.?\s[A-Z]\w*')

matches = pattern.findall(text_to_search)

for match in matches:
    print(match)
```
output
Mr
Mr
Ms
Mrs
Mr

*Recommend to use group*
```python
for match in matches:
    print(match.group())
```
Mr. Schafer
Mr Smith
Ms Davis
Mrs. Robinson
Mr. T


```python
pattern = re.compile(r'\d{3}.\d{3}.\d{4}')

matches = pattern.findall(text_to_search)

for match in matches:
    print(match)
```
output
321-555-4321
123.555.1234
123*555*1234
800-555-1234
900-555-1234


## match method. Matches at the beginning of string.

```python
sentence = 'Start a sentence and then bring it to an end'

pattern = re.compile(r'Start')

matches = pattern.match(sentence)
print(matches)
print(matches.group())
```
output
<re.Match object; span=(0, 5), match='Start'>
Start

```python
pattern = re.compile(r'sentence')
```
output
None

## search method. Search the entire string. 

```python
sentence = 'Start a sentence and then bring it to an end'

pattern = re.compile(r'sentence')

matches = pattern.search(sentence)
print(matches)
```
output
<re.Match object; span=(8, 16), match='sentence'>


```python
pattern = re.compile(r'donotexit')
```
output
None

##  flags . Examples: ignorecase, multiline, verbose

```python
sentence = 'Start a sentence and then bring it to an end'

pattern = re.compile(r'start', re.IGNORECASE)

matches = pattern.search(sentence)
print(matches)
```
output
<re.Match object; span=(0, 5), match='Start'>

*Equals*
```python
pattern = re.compile(r'start', re.I)
```
































