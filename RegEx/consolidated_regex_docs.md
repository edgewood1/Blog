# A Basic Introduction to Regular Expressions (Regex)

Regular Expressions (or regex) are powerful tools for pattern matching in text. They allow you to define a search pattern that can be used to find, replace, or validate strings.

## Core Concepts

### 1. Literal Characters

The simplest regex is a literal string. The pattern `cat` will find the exact sequence of characters "cat" in a string.

### 2. Metacharacters

Metacharacters are special characters that have a meaning beyond their literal sense. Here are some of the most common ones:

-   `.` (Dot): Matches any single character except a newline.
-   `*`: Matches the preceding character zero or more times.
-   `+`: Matches the preceding character one or more times.
-   `?`: Matches the preceding character zero or one time. It also makes a quantifier "lazy" (see below).
-   `\`: Escapes a metacharacter, treating it as a literal. For example, `\.` matches a literal dot.
-   `[]`: A "character set." Matches any single character within the brackets.
    -   `[abc]` matches 'a', 'b', or 'c'.
    -   `[a-z]` matches any lowercase letter.
    -   `[^abc]` matches any character that is *not* 'a', 'b', or 'c'.
-   `()`: Groups an expression. The engine treats the grouped expression as a single unit.
-   `|`: Acts as an OR operator. `cat|dog` matches either "cat" or "dog".

### 3. Anchors

Anchors don't match characters but rather positions in the string.

-   `^`: Matches the beginning of the string.
-   `$`: Matches the end of the string.
-   `\b`: Matches a word boundary (the position between a word character and a non-word character).

### 4. Quantifiers

Quantifiers specify how many times a character, group, or character set must be present.

-   `{n}`: Matches exactly *n* times.
-   `{n,}`: Matches *n* or more times.
-   `{n,m}`: Matches between *n* and *m* times.

**Greedy vs. Lazy:** By default, quantifiers are "greedy," meaning they match as many characters as possible. Appending a `?` makes them "lazy," matching as few characters as possible.

### 5. Shorthand Character Classes

-   `\d`: Matches any digit (`[0-9]`).
-   `\w`: Matches any word character (alphanumeric + underscore: `[a-zA-Z0-9_]`).
-   `\s`: Matches any whitespace character (space, tab, newline).
-   `\D`, `\W`, `\S`: Match the *opposite* of their lowercase counterparts.

## Simple Examples

-   **Email Validation**: A simple (but not fully robust) regex for email might be `\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b`. This looks for a word boundary, followed by one or more word characters/symbols, an @ sign, more word characters/symbols, a dot, and then 2 or more letters.
-   **Finding Hex Color Codes**: `#?([a-fA-F0-9]{6}|[a-fA-F0-9]{3})` looks for an optional `#` followed by either 6 or 3 hexadecimal characters.

## How to Use Regex

Regex is supported in almost all programming languages and many text editors. You'll typically find functions like:

-   `match()`: To check if the pattern matches at the beginning of the string.
-   `search()`: To find the first occurrence of the pattern anywhere in the string.
-   `findall()`: To find all occurrences of the pattern.
-   `sub()` or `replace()`: To substitute occurrences of the pattern with a replacement string.

This tutorial covers just the basics. Regex can get much more complex, with features like lookaheads, lookbehinds, and backreferences, but this foundation is enough to get you started!
