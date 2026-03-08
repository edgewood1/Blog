REG EX



\ - backslash - escape character - notification that a character is coming



Identifiers: 



\d — any number

\D - anything but a number

\s - space

\S - anything but a space

\w any character

\W - anything but a charaxcter



. [period] - is any character except a new line



\b - whitespace around words

\. - a period



Modifiers: 



{1, 3} - length we’re expecting - number of digits 1-3. eg, \d {1-3}



\+ - if there’s 1 or more

? - match 0 or 1 

- match 0 or more 

$ - the end of a string matched

^ beginning 



| - pipe - either or — \d {1-3} | \d {304=5}

[] range / variance— [1-5a-qA-Z]

{x} - expecting x amount



White space characters



\n - new line

\s space

\t tab

\e escape

fr form feed

\r return



Dont forget



. + * ? {} [] $ ^ () |\ = to use these you must escape them



import re



example = ‘’’ 

Jessica is 15 years old, and Danilel is 27 years old. 

Edward is 97, an dhis grandfather, Oscar, is 102. 

‘’

, - comma seprates search parameter and location



ages = re.findall(r’\d{1,3}’, example

name = re.findall(r’[A-Z][a-z]*’, example) - first letter cap, rest anything



- \- just 1 of first and as many of 2nd as possible, but as soon as anyting not a letter appears, parsing stops. 



r - announces evaluation starts

\ - backslash

\s* - if you find any number of space characters, let us know

(\s*) - group and include what your searching for

(s*) - includes ’s’ as an item in list





? - matches previous expression 1 or 0 times