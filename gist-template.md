# Title (replace with your title)

Regex Tutorial exercise

## Summary

Describing hex value as: `/^#?([a-f0-9]{6}|[a-f0-9]{3})$/`

This Hex code is used to define a value which begins with a # then followed by a 6 alphanumeric character sequence (numbers 0-9 or letters a-f) followed by a 3 alphanumeric character sequence with the same parameters

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

### Anchors

Anchors belong to the family of regex tokens that don't match any characters, but that assert something about the string or the matching process. Anchors assert that the engine's current position in the string matches a well-determined location: for instance, the beginning of the string, or the end of a line. The ^ and $ in the regex are Anchors, as seen in the beginning and end of the expression: /^([a-z0-9_.-]+)@([\da-z.-]+).([a-z.]{2,6})$/ n our regex above, the beginning ^ and ending $ anchors indicate that the search must match characters defined by the piece of the expression located between the anchors: ([a-z0-9_.-]+)@([\da-z.-]+).([a-z.]{2,6}) We will explain each of these components in their respective sections below.

### Quantifiers

Quantifiers are used to quantify how many times a part of your regular expression should be repeated. If users want to repeat a part in a regular expression such as an individual character, a character class or a sub-expression, they can write a quantifier after it to specify how many times it should be repeated. For example, the regular expression /\d{4}/ matches a four-digit number. It is the same as /\d\d\d\d/. The following list shows some examples of the most common quantifiers: ? (Repeated from 0 to 1 times), \* (Repeated from 0 to Infinity times), + (Repeated from 1 to Infinity times), {N} (Repeated from N to N times), {,N} (Repeated from 0 to N times), {N,} (Repeated from N to Infinity times), and {N,M} (Repeated from N to M times).

### OR Operator

The Alternation Operator ( | or | )

Alternatives match one of a choice of regular expressions: if you put the character(s) representing the alternation operator between any two regular expressions a and b , the result matches the union of the strings that a and b match.

### Character Classes

With a “character class”, also called “character set”, you can tell the regex engine to match only one out of several characters. Simply place the characters you want to match between square brackets. If you want to match an a or an e, use [ae]. You could use this in gr[ae]y to match either gray or grey. Very useful if you do not know whether the document you are searching through is written in American or British English.

A character class matches only a single character. gr[ae]y does not match graay, graey or any such thing. The order of the characters inside a character class does not matter. The results are identical.

You can use a hyphen inside a character class to specify a range of characters. [0-9] matches a single digit between 0 and 9. You can use more than one range. [0-9a-fA-F] matches a single hexadecimal digit, case insensitively. You can combine ranges and single characters. [0-9a-fxA-FX] matches a hexadecimal digit or the letter X. Again, the order of the characters and the ranges does not matter.

Character classes are one of the most commonly used features of regular expressions. You can find a word, even if it is misspelled, such as sep[ae]r[ae]te or li[cs]en[cs]e. You can find an identifier in a programming language with [A-Za-z\_][a-za-z_0-9]\*. You can find a C-style hexadecimal number with 0[xX][a-fa-f0-9]+.

### Flags

Flags are the forward slashes // that begin and end the regex:

/^([a-z0-9_.-]+)@([\da-z.-]+).([a-z.]{2,6})$/

Regular expressions, including our regex above, are generally contained within slashes // that simply delimit the search pattern. Some expressions have specific flags that modify the search parameters, such as making the seach case-insensitive, but our regex just includes standard flags.

### Grouping and Capturing

By placing part of a regular expression inside round brackets or parentheses, you can group that part of the regular expression together. This allows you to apply a quantifier to the entire group or to restrict alternation to part of the regex.

Only parentheses can be used for grouping. Square brackets define a character class, and curly braces are used by a quantifier with specific limits.

### Bracket Expressions

POSIX bracket expressions are a special kind of character classes. POSIX bracket expressions match one character out of a set of characters, just like regular character classes. They use the same syntax with square brackets. A hyphen creates a range, and a caret at the start negates the bracket expression.

### Greedy and Lazy Match

Greedy Match is created when a regex includes a + as we can see twice in our regex below: /^([a-z0-9_.-]+)@([\da-z.-]+).([a-z.]{2,6})$/ The + basically means "as many as possible" of the previous character(s), For example, A+ would match "A", "AA", "AAA", and so on because it will match as many "A"s that may exist in the location.

In our regex above, the characters directly before the @ sign [a-z0-9_.-] and directly after the @ sign [\da-z.-] are both followed by a +. In the context of this regex, it means there is not a limit to how many characters may exist before and after the @ sign.

### Boundaries

The metacharacter \b is an anchor like the caret and the dollar sign. It matches at a position that is called a “word boundary”. This match is zero-length.

There are three different positions that qualify as word boundaries:

Before the first character in the string, if the first character is a word character.
After the last character in the string, if the last character is a word character.
Between two characters in the string, where one is a word character and the other is not a word character.
Simply put: \b allows you to perform a “whole words only” search using a regular expression in the form of \bword\b. A “word character” is a character that can be used to form words. All characters that are not “word characters” are “non-word characters”.

### Back-references

Backreferences match the same text as previously matched by a capturing group. Suppose you want to match a pair of opening and closing HTML tags, and the text in between. By putting the opening tag into a backreference, we can reuse the name of the tag for the closing tag. Here’s how: <([A-Z][a-z0-9]_)\b[^>]_>._?</\1>. This regex contains only one pair of parentheses, which capture the string matched by [A-Z][a-z0-9]_. This is the opening HTML tag. (Since HTML tags are case insensitive, this regex requires case insensitive matching.) The backreference \1 (backslash one) references the first capturing group. \1 matches the exact same text that was matched by the first capturing group. The / before it is a literal character. It is simply the forward slash in the closing HTML tag that we are trying to match.

### Look-ahead and Look-behind

Look-ahead and look-behind matches fall under the "look-around" patterns. Look-around lets you match a group before (look-behind) or after (look-ahead) your main pattern without including it in the result. Negative look-arounds specify a group that can NOT match before or after the pattern.

## Author

This regex tutorial was created by Kenny Ng student of the columbia full stack bootcamp program. My github page can be found at https://github.com/kenng8891.
