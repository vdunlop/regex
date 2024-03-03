# How to: Regex Expression Interpretation

This is a tutorial that explains how a specific regular expression (regex) functions by breaking down each part of the expression and describing what it does.

## Summary

The regex function that I will be breaking down today is:

/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/

This expression will match a URL. In this tutorial, I will be going through each part of the expression and explaining what they contain (for example, anchors, quantifiers, etc) and how they will work in finding a URL.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

### Anchors
There are two characters that are anchors in a regex:

1. the caret ^ which signifies the beginning of a string/string part
2. the dollar sign $ which signifies the end of a string/string part

We have two anchors in our regex:

Character 2 is ^. It means start this string with what follows (see walkthrough).

Character 63 is $. It means end this string with what precedes it (see walkthrough).

### Quantifiers
Quantifiers are characters that signify the number of "matching" characters/patterns within a part of or the whole string, including:

1. the star/asterisk * for 0 or more matches 
2. the plus sign + for 1 or more matches
3. the question mark ? for 0 or 1 match (can also mean optional, see xxx)
4. curly brackets {} 

    a. { n } for n matches where n is a digit

    b. { n, } for at least n matches where n is a digit

    c. { n, m } for at least n matches to at most m matches where n and m are digits

Quantifiers are called "greedy" in that they match as many characters as they are allowed. The ? allows only 0 or 1 character/pattern match which is referred to as making a quantifier lazy.

Our regex uses xx quantifiers:

Character 28 is +. It means there should be 1 or more of the string with [\da-z\.-] (see walkthrough).

Character 57 is *. It means there should be 0 or more of the string with [\/\w \.-] (see walkthrough).

Character 59 is *. It means there should be 0 or more of the 

Characters 40 through 44 are {n,m}. It means that there should be between n and m matches of the string with [a-z\.] (see walkthrough).

### Grouping Constructs
Grouping allows us to break a regex into smaller parts called sub-expressions. Parentheses (()) are used to delineate a group, for example:

\d{3}-(\d{3}) the parentheses around the second group of 3 digits indicates that it is a sub-expression. If you put a ? after it, the ? would apply to that sub-expression being optional.

Our regex has several groups:
(https?:\/\/) which is http with an option s and then //

([\da-z\.-]+) which is 1 or more of the pattern of any of these characters (digits, a through z, . and/or -)

([a-z\.]{2,6}) which is 2 to six of the pattern of any characters (a through z and/or .)

([\/\w \.-]*) which is 0 or more of the pattern of any characters (/, ., - and/or words which are characters A through Z, a through z and digits)

See walkthrough for more details.

### Bracket Expressions



### Character Classes

### The OR Operator
The OR operator is the pipe character |. It indicates to allow the characters or strings to either sides of the | and within parentheses () to be matched. For example, to look for a string that has .net, .com or .org in it, use:

\.(net|com|org)

### Flags

### Character Escapes

## Walkthrough


## Author

I am a software engineer. I worked on real-time embedded projects for almost 15 years. Then, I took a hiatus from work to raise my children and care for my disabled mom. Now that the kids are moved out and my mom is in a safe place, I am working on a 6-month Web Programming certificate program through the University of Minnesota with the goal of becoming a backend web programmer working with databases.

http://github.com/vdunlop