# Regex Tutorial for Matching a URL

This tutorial explains how a regular expression (regex) for matching a URL functions, breaking down each component of the expression and describing what it does.

## Summary

This tutorial describes the regex, or sequence of characters that defines the specific search pattern of a URL, ```/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/```. The characters used in this specific search pattern are called metacharacters, which instead of indicating a literal character, indicates a more generalized pattern. Regex are frequently used to validate input, as when included in code or search algorithms, regex can be used to find certain patterns of characters in a string, or find and replace a character or sequence of characters within a string.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Character Classes](#character-classes)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy Match](#greedy-match)

## Regex Components
Components of a regex matching a URL include:
* Anchors ```^``` ```$```
* Quantifiers ```*``` ```+``` ```?``` ```{}```
* Character classes ```\d``` ```\w``` ```.```
* Grouping and capturing ```()```
* Bracket expressions ```[]```
* Greedy match ```*```

### Anchors
Anchors match the start(^) and end($) of a given string. For example, ```^The end$``` is an exact string match that starts and ends with __The end__.

In the URL regex, we see two slashes at the start and end, as seen in ```/jkl/```, which flags, or delimits the beginning and end of a regex pattern. We then see ```^``` and ```$``` at those two ends to signify the search pattern found in between those characters.

### Quantifiers
Quantifiers denote the number of characters that belong in the string. ```*``` is a quantifier that matches a string that includes __0 or more__ of the character preceding the ```*``` metacharacter. For example, ```jkl*``` matches a string that has ```jk``` followed by 0 or more ```l```.


```+``` is a quantifier that matches a string that has __1 or more__ of the character preceding the ```+``` metacharacter. ```jkl+``` matches a string that has ```jk``` followed by 1 or more ```l```. 


```?``` is a quantifier that matches a string that has __0 or 1__ of the character preceding ```?``` metacharacter, as in ```jkl?```, which matches a string where ```jk``` is followed by 0 or 1 ```l```. This quanitifier can be found in the first capturing group of the URL regex, ```(https?:\/\/)```, after the "s" character to indicate that the "s" after "http" is optional. It is also found after the first capturing group, ```/^(https?:\/\/)```__?__```([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/```, to denote that the entire first capturing group is optional. Lastly, it is found at the very end of the regex ```/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/```__?__```$/``` to denote the optionally escaped ```/``` at the end of the URL.

```{}``` is a quantifier that matches a string that contains the character preceding the ```{}``` the amount of times delineated in the curled brackets. For example, ```jkl{2}``` matches a string that has ```jk``` followed by 2 ```l```. 

Other ways ```{}``` can be used is with a ```,``` following the number in ```{}```, as in ```jkl{5,}``` which matches a string that has ```jk``` followed by __5 or more__ ```l```. ```jkl{5,10}``` matches a string that has ```jk``` followed by __5 up to 10__ ```l```.

Characters may also be grouped in ```()``` to denote a specific sequence that follows a specific number of times, depending on the quantifier used, as in ```j(kl)*```, which matches a string that has ```j``` followed by __0 or more__ copies of the sequence ```kl```. Used in conjunction with ```{}```, ```j(kl){5,10}``` matches a string that has ```j``` followed by __5 up to 10__ copies of the sequence ```kl```. 

### Character Classes
The character class ```\d``` matches a single character that is a digit, from __0 to 9__. 

The character class ```\w``` matches a single word character which can be __alphanumeric__ or __underscore__.

```.``` matches __any__ character. When escaped with a backslash, as in ```\.```, the regex identifies a literal ```.```.

### Grouping and Capturing
Parentheses ```j(kl)``` create a capturing group with the value ```kl```. In ```j(?:kl)```, we disable the capturing group to only capture the letters outside the parentheses. In ```j(?<foo>kl)```, we assign a name ```foo``` to the capturing group.

The first capturing group of the URL regex, ```(https?:\/\/)```, includes a pattern that matches an "h", "t, "t", "p", optional "s" character followed by a ":", two escaped "/", and a ```?``` quantifier, indicating 0 or 1 of the preceding capturing group. The URL may or may not include an ```http://``` or ```https://```.

The second capturing group, ```([\da-z\.-]+)```, includes a bracketed character set ```[\da-z\.-]``` which matches any character including a digit character ```\d```, a character from a-z, case-sensitive, an escaped ```.```, and/or ```-```. This character set is followed by the ```+``` quantifier, indicating 1 or more of the preceding character set. This second capturing group is then followed by an escaped ```\.```. The URL includes at least 1 or more of the bracketed character set, followed by a ```.```, as in ```google.``` or ```www.google.``` in  ```www.google.com```.

The third capturing group, ```([a-z\.]{2,6})```, includes a bracketed character set ```[a-z\.]``` which matches any character including an a-z character, case-sensitive, and an escaped ```\.```. This is found 2 and up to 6 times as indicated by the ```{2,6}``` quantifier. Examples of this capturing group include ```.com```, ```.net``` and ```.gov```.

The fourth capturing group, ```([\/\w \.-]*)``` includes a bracketed character set ```[\/\w \.-]``` which matches any character including an escaped ```\/```, an escaped alphanumeric or underscore word character ```\w```, an escaped ```\.```, and/or ```-``` character. This set is followed by the ```*``` quantifier, indicating a match of 0 or more of the preceding character set. This entire fourth capturing group is then matched 0 or more times, as indicated by the ```*``` quantifier following the fourth capturing group, meaning this entire portion of the URL is optional or can have as many additions as delineated. An example of this may be a specific route on a website, such as ```youtube.com```__/feed/explore/__.

An escaped ```\/``` and ```?``` quantifier then follows the fourth capturing group, indicating an optional ```/``` after the URL.  Thus concludes the URL regex search pattern!

### Bracket Expressions
The bracket metacharacter ```[]``` is a character set, and matches a string that has any character or combination of characters within the character set, for example, ```[jkl]``` matches a string that has a __j__, or __j k__, or __jl__. It is also the same as ```j|k|l```, or ```[j-l]```.

### Greedy Match
The quantifier metacharacters ```*``` ```+``` and ```{}``` are greedy operators which expand the match as far as possible through the string. For example, ```<.+>``` matches this entire string ```<div>A div with divs in a div</div>```.

The URL regex uses the all of these metacharacters to quantify the number of matches of a particular string.
