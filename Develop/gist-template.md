# How to: Regex Expression Interpretation
This is a tutorial that explains how a specific regular expression (regex) functions by breaking down each part of the expression and describing what it does. This tutorial will be found in Gist.

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
Anchors in regex are characters that specify a position of a string/string part/character. 
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

Our regex uses 4 quantifiers:

Character 28 is +. It means there should be 1 or more of the string with [\da-z\.-] (see walkthrough).

Character 57 is *. It means there should be 0 or more of the string with [\/\w \.-] (see walkthrough).

Character 59 is *. It means there should be 0 or more of the 

Characters 40 through 44 are {n,m}. It means that there should be between n and m matches of the string with [a-z\.] (see walkthrough).

### Grouping Constructs
Grouping allows us to break a regex into smaller parts called sub-expressions. Parentheses (()) are used to delineate a sub-expression/group, for example:

\d{3}-(\d{3}) the parentheses around the second group of 3 digits indicates that it is a sub-expression. If you put a ? after it, the ? would apply to that sub-expression being optional.

Our regex has several groups:
(https?:\/\/) which is http with an option s and then //

([\da-z\.-]+) which is 1 or more of the pattern of any of these characters (digits, a through z, . and/or -)

([a-z\.]{2,6}) which is 2 to six of the pattern of any characters (a through z and/or .)

([\/\w \.-]*) which is 0 or more of the pattern of any characters (/, ., - and/or words which are characters A through Z, a through z and digits)

See walkthrough for more details.

### Bracket Expressions
For bracket expressions, we are referencing square brackets ([]). The characters within [] are the characters that we are looking for in our string search. The hyphen (-) is a special character used inside [] to indicate a range of alphanumeric characters.

Our regex has several uses of bracket expressions:

character 18 and 27 wraps around a group of characters that we are looking for in this position of a string. Notice the - being used as a range indicator and a literal - (see walkthrough for details)

character 33 and 39; character 47 and 56 do the same as above

### Character Classes
Character classes define which character(s) we are looking for. We are using several character classes in our regex:

1. \w represents A through Z, a through z and 0 through 9. 
2. \d represents digits, 0 through 9.

Our regex has a couple of character classes in use:

characters 19 and 20 mean match any digit in this position

characters 50 and 51 mean match any capital letters, small letters or digit in this position

### The OR Operator
The OR operator is the pipe character |. It indicates to allow the characters or strings to either sides of the | and within parentheses () to be matched. For example, to look for a string that has .net, .com or .org in it, use:

\.(net|com|org)

### Flags
Flags are an additional indicator tacked on after the final / indicating end of string. Our regex doesn't have any flags.

Flags in general are a character put after the final /. Each flag extends the search in a different way:
1. g search globally
2. i ignore case during the search
3. m treat the multi-line input string as multiple lines

### Character Escapes
You'll notice in regex that some characters have multiple meanings. For example the - can be a literal -, but it can also represent a range of characters with []. If you want to look for a literal character like -, you would escape that character.

The \ in front of a - means that you are looking for the literal -.

## Walkthrough
This is a walkthrough of the characters and what they are doing in our regex example. 

We are looking for the URL markdownguide.org/basic-syntax/

Our regex begins and ends with the forward slash (**/**) because it is a literal.

The **^** says that we want to see the next pattern at the beginning of our string.

Our next pattern could be **http** with an optional **s** (because of the **?** after s) and then **:** and then **//** (shown with character escapes **\\/\\/**). BUT, since this is all wrapped in parentheses **()**, it is a group. This group is followed by a **?**, so our entire string may begin with **http://** or **https://** but it is optional.

**https://**

Moving on to the next pattern wrapped in **()**. We will look at the characters wrapped in **[]**. Square brackets signify a bracket expression, so we are allowing the characters within the [] to be in the search. **\d** means digits 0 through 9. **a-z** mean the small letters a through z are allowed. **\.** escapes the **.** so we are also including .  **-** at the end means we will include **-**. And finally, **+** tells us that we will match 1 or more of these characters.

**markdownguide**

We now see a **\.** which means we are requiring a . to follow the above pattern.

**.**

The next pattern is also wrapped in **()**. First let's look at the characters wrapped in the **[]**. **a-z** is any lower case letter and **\.** is the literal **.**. The **{2,6}** following the [] means that we are searching for these characters in the [], but only the first **2** to **6** characters (a word containing a through z and/or . of 2 to 6 characters in length).

**.org**

The last pattern wrapped in **()** also has characters wrapped in **[]** that will be included in the search. These letters are the **/** which is escaped **\\/**; the **\w** (any alphanumeric characters); a **space**; a **.** which is escaped **\.**; and a **-**. Since the [] are followed by a **\***, you can have 0 or more of these characters and since the () are also followed by a **\***, you can have 0 or more of these patterns.

**/basic-syntax**

Finally, the **\\/\?** means that after all of the above we are looking for an optional (?) \. 

**/**

And last but not least, the **$** means we are finishing our search string at the optional \.

**/basic-syntax/**

## Author
I am a software engineer. I worked on real-time embedded projects for almost 15 years. Then, I took a hiatus from work to raise my children and care for my disabled mom. Now that the kids are moved out and my mom is in a safe place, I am working on a 6-month Web Programming certificate program through the University of Minnesota with the goal of becoming a backend web programmer working with databases.

http://github.com/vdunlop