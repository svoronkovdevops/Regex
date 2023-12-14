# Regex

## Content

[Test regexs](#test-regexs)

[String](#string)

[Metacharacter](#metacharacter)

[Character set](#character-set)

[Repetition metacharacters](#repetition-metacharacters)

[Grouping and Alternation Expressions](#grouping-and-alternation-expressions)

[Anchored Expressions](#anchored-expressions)

[Capturing Groups and Backreferences](#capturing-groups-and-backreferences)

[Lookaround Assertions](#lookaround-assertions)

[Unicode and Multibyte Characters](#unicode-and-multibyte-characters)

[Useful Regular Expressions](#useful-regular-expressions)


## Test regexs

Open `regexpal/index.html` in any brouwser

`/car/` - means type `car` to regex input

`/car/i` - - means type `car` to regex input and select flag case insensitive `i`

!!! By default case-sensitive

`/car/g` - - means type `car` to regex input and select flag global `g`

!!! Standart(non-global) earliest always prefered "pizzazz" /zz/(first) for global matches all


`/car/s` - - means type `car` to regex input and select flag dot matches all `s`

!!! `.` means any character except newline eith flag dot matches all `.` means any character


`/^[a-z ]+/m` -- means type `^[a-z ]+` with multiline anchors (check lines)

[Content](#content)

## String

Regex:  /car/

String: "car"

Regex: /car/

String: "carnival"


### Case-sensitivity matters

Regex:  /car/

String: "Carnival"

Regex: /car/i 

String: "Carnival"

Regex:  /Car/i 

String: "carnival"


### Whitespace matters

Regex:  /car/ (doesn't match)

String: "c a r"


### Global modifier

Regex:  /zz/ (only first zz)

String: "pizzazz"

Regex:  /zz/g (both zz match)

String: "pizzazz"

Regex:  /cat/ (only cat match)

String: "The cow, camel, and cat communicated."

Regex:  /cat/g (match cat and  cat in communicated)

String: "The cow, camel, and cat communicated."


#### Notice the syntax coloring

Regex: . * + [abc] ^ $ | ? (abc) \d{2,3}

[Content](#content)


## Metacharacter

### wildcard

`.` means any character except newline

Regex:  /h.t/g (all except heat)

String: "hat hot hit heat hzt h t h#t h:t"

Regex:  /.a.a.a/

String: "banana papaya abacab"

Regex:  /a.a.a./

String: "banana papaya abacab"

Write a regex that matches all three words:
String: "silver sliver slider"

answer: `s...er`


### escaping

`\` escape the next character 

allows use of metacharacters as literal characters(`\\` match backslash`\`)

only for metacaracters(literal should never be escaped)

quotation marks are not metacharacters

Regex:  `9\.00`g (mutch only first)

String: "9.00 9500 9-00"

String: "his_export.txt her_export.txt"

Regex:  `h.._export.txt`g (both)

Regex:  `h.._export\.txt`g (both)

String: "resume1.txt resume2.txt resume3_txt.zip"

Regex:  `resume..txt`g (all)

Regex:  `resume.\.txt`g (first and second)


Also may need to escape `/`

String: "/home/user/document.txt"

Regex:  `home/user/document\.txt` (match)

Regex:  `\/home\/user\/document\.txt` (match)


### space

` `

Regex:  /c a t/ (match)

String: "c a t"

### tab 

`\t`

Regex:  `a\tb` (match)

String: "a  b"

### line returns

`\r` `\n` `\r\n`

Regex:  `c\nd` (match)

String: "abc
def"



### non-printable characters

`\a` bell

`\e` escape

`\f` form feed

`\v` vertical tab


### ASCII or ANSI codes

codes that control apperance of a text terminal

`0A9 = \xA9`


[Content](#content)

## Character set

`[` begin a character set

`]` end a character set

Any one of several character
- but only one character
- order of characters does not matter



### Matches single, lowercase vowels

Regex:  /[aeiou]/g (matches any one vowel)

String: "Bananas Peaches Apples"

Regex: /gr[ea]y/g (both matches)

String: "grey gray"

Regex: /gr[ea]t/ (doesn't match)

String: "great"

Regex: /gr[ea][ea]t/ (all much)

String: "great graet greet graat"

### Uppercase

Regex: /[ABCDEFGHIJKLMNOPQRSTUVWXYZ]ello/

String: "Hello"

### Character ranges

`-` range of characters - represents all characters between two characters

Only a metacharacter inside a character set, a literal dash otherwise

[0-9]

[A-Za-z]

[a-ek-ou-y]

!!! Caution

[50-99] is not all numbers from 50 to 99, it is the same as [0-9]


Regex: /[A-Z]ello/ (mutch)

String: "Hello"

Regex: /[A-Za-z]/ (mutch)

String: "Hello"


#### Phone number

String: "555-666-7890" (mutch)

Regex: /[0-9][0-9][0-9]-[0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]/


#### Postal codes

String: "90210" (mutch)

Regex:  /[0-9][0-9][0-9][0-9][0-9]/

String: "WC2H 9AW" (mutch)

Regex:  "[0-9A-Z][0-9A-Z][0-9A-Z][0-9A-Z] [0-9A-Z][0-9A-Z][0-9A-Z]"

### Negative character set

`^` negate a character set

Not any one of several characters
- add `^` as the first character inside a character set
- still represents one character

Example

/[^aeiou]/ matches any one consonant(non-vowel)

/see[^mn]/ matches "seek" and "sees" but not "seem" or "seen"

!!! Caution

/see[^mn]/ matches "see " but not "see" 



Regex:  /[^a-z]/g (match N and spaces and dot)

String: "Now we know how to make negative character sets."


#### Negates the entire character set

Regex:  /[^a-zA-Z]/g (match dot and spaces)

String: "Now we know how to make negative character sets."


#### Only matches a single character

Regex:  /[^aeiou]/

String: "It seems I see the sea I seek."

Regex:  /see[^mn]/ (sea or global seek also)

String: "It seems I see the sea I seek."


#### Must match one character (which may be a space or punctuation)

Regex:  /see[^mn]/

String: "It seems I see the sea I see"

Regex:  /see[^mn]/

String: "It seems I see the sea I see."



### Metacharacters inside character sets

Metacharacters inside character sets are already escaped
- do not need to escape them again
- /h[abc.xyz]t/ matches "hat'' and "h.t", but not "hot"

Exceptions
- `] - ^ \`

Examples
- /var[[(][0-9][\])]/
- /2003[-/]10[-/]05/ nay not require escaping
- /file[0-\_]1/ does require escaping

Regex:  /h[abc.xyz]t/g (exclude hot)

String: "hat hot h.t"

Regex:  /var[[(][0-9][\])]/g (both match)

Regex:  /var[[(]\d[\])]/g (both match)

String: "var(3) var[4]"

#### May not require escaping

Regex:  /2003[-/]10[-/]05/g (both match)

String: "2003/10/05 2003-10-05"

Regex:  /file[0-\_]1/g (exclude file-1)

Regex:  /file[0\-\_]1/g (exclude file\1)

Regex:  /file[0\-\\_]1/g (all)

String: "file01 file-1 file\1 file_1"

### Shorthand characters sets


`\d` - digit    - [0-9]

/\d\d\d\d/ matches 1984 but not text

`\w` - word character    - [a-zA-Z0-9_]

/\w\w\w\w/ matches text 

/[\w\-]/ matches as word character or hyphen

`\s` - whitespace    - [ \t\r\n]

/\w\s\w\w/ matches "I am" but not "Am I"

/[\d\s]/ matches any digit or whitespace character

/[^\d]/ the same as /\D/ or /[^0-9]/

`\D` - Not digit    - [^0-9]

`\W` - Not word character    - [^a-zA-Z0-9_]

`\S` - Not whitespace    - [^ \t\r\n]

!!! Caution
- /[^\d\s]/ is not [\D\S]
- /[^\d\s]/ = NOT digit OR space character
- /[\D\S]/ = EITHER NOT digit OR NOT space character

Regex:  /\d\d\d\d/ (matches 1984)

String: "1984 text"

Regex:  /\w\w\w\w/ (all matches )

String: "1984 text 1_5W"

Regex:  /[\w\-]/g (all)

String: "blue-green paint"

Regex:  /[\d\s]/g (without abc)

String: "123 456 789 abc"


#### Be careful when using negatives

Regex:  /[^\d\s]/g (only abc)

String: "123 456 789 abc"

Regex:  /[\D\S]/g (all)

String: "123 456 789 abc"

### posix bracket expressions


| POSIX      | Description                                                | ASCII           | Unicode                        | Shorthand | Java      |
|------------|------------------------------------------------------------|-----------------|--------------------------------|-----------|-----------|
| [:alnum:]  | Alphanumeric characters                                    | [a-zA-Z0-9]     | [\p{L}\p{Nl}\p{Nd}]           |           | \p{Alnum} |
| [:alpha:]  | Alphabetic characters                                      | [a-zA-Z]        | \p{L}\p{Nl}                   |           | \p{Alpha} |
| [:ascii:]  | ASCII characters                                           | [\x00-\x7F]     | \p{InBasicLatin}               |           | \p{ASCII} |
| [:blank:]  | Space and tab                                              | [ \t]           | [\p{Zs}\t]                    | \h        | \p{Blank} |
| [:cntrl:]  | Control characters                                         | [\x00-\x1F\x7F] | \p{Cc}                         |           | \p{Cntrl} |
| [:digit:]  | Digits                                                     | [0-9]           | \p{Nd}                         | \d        | \p{Digit} |
| [:graph:]  | Visible characters (anything except spaces and ctrl chars) | [\x21-\x7E]     | [^\p{Z}\p{C}]                  |           | \p{Graph} |
| [:lower:]  | Lowercase letters                                          | [a-z]           | \p{Ll}                         | \l        | \p{Lower} |
| [:print:]  | Visible chars and spaces (anything except ctrl chars)      | [\x20-\x7E]     | \P{C}                          |           | \p{Print} |
| |                                     |  |  |           | |
| [:space:]  | All whitespace chars incl. line breaks                     | [ \t\r\n\v\f]   | [\p{Z}\t\r\n\v\f]             | \s        | \p{Space} |
| [:upper:]  | Uppercase letters                                          | [A-Z]           | \p{Lu}                         | \u        | \p{Upper} |
| [:word:]   | Word chars (letters, numbers, underscores)                 | [A-Za-z0-9_]    | [\p{L}\p{Nl}\p{Nd}\p{Pc}]     | \w        | \p{IsWord}|
| [:xdigit:] | Hexadecimal digits                                         | [A-Fa-f0-9]     | [A-Fa-f0-9]                    |           | \p{XDigit}|


[:punct:]  Punctuation and symbols [!"\#$%&'()*+,\-./:;<=>?@\[\\\]^_`{|}~]      \p{P}        \p{Punct} |



#### Using 

- Correct: [[:alpha:]] or [^[:alpha:]]
- Incorrect: [:alpha:] 

Don't mix POSIX sets and shorthand sets

POSIX
- Yes: Perl, PHP, Ruby, Unix
- No: Java, JS, .NET, Python

#### This command only works on Unix


ps aux | grep --regexp="s[[:digit:]]"



[Content](#content)



## Repetition metacharacters

`*` preceding item zero or more times

`+` preceding item one or more times

`?` preceding item zero or one time



Regex:  /apples*/g (all)

String: "apple apples applesssssss" (not contain or contain)

Regex:  /apples+/g (2d,3d)(contain s or ss)

String: "apple apples applesssssss"

Regex:  /apples?/g (first, second, part 3d apples)(not contain or contain one time)

String: "apple apples applesssssss"


Regex:  /\d\d\d\d*/  (1st,2d,3d)(match 3 digit or more)

String: "123456789 1234 123 12"

Regex:  /\d\d\d+/ (1st,2d,3d)(match 3 digit or more)

String: "123456789 1234 123 12"


Regex:  /[a-z]+\d[a-z]*/

String: "abc9xyz" (match)

String: "a9xyz" (match)

String: "9xyz" (doesn't)

Regex:  /[a-z]+\d[a-z]*/

String: "abc9xyz" (match)

String: "abc9z"   (match)

String: "abc9"   (match)


#### Optional letter "u"

Regex:  /colou?r/ (both)

String: "color colour"


#### Find any word that ends in "s"

Regex:  /\w+s/ (match apples)

String: "We picked apples."


### Quantified repetition

`{` start quantified repetition of preceding item

`}` end quantified repetition or preceding item

`{min, max}` min and max are positive, min must always be included and can be zero, max is optional

`\d{4,8}` matches numbers with 4 or 8 digits

`\d{4}` matches numbers with exactly 4 digits (min is max)

`\d{4,}` matches numbers with 4 or more digits (max is infinite)


\d{0,} is the same as \d*

\d{1,} is the same as \d+

/\d{3}-\d{3}-\d{4}/ matches most US phone numbers

/A{1,2} bonds/ matches "A bonds" and "AA bonds", not "AAA bonds"

Regex:  /\w{5}\s/

String: 
Shall I compare thee to a summer's day?
Thou art more lovely and more temperate:
Rough winds do shake the darling buds of May,
And summer's lease hath all too short a date.

Regex:  /\w{2,5}\s/
Regex:  /\w{5,}\s/


Regex:  /\d{3}-\d{3}-\d{4}/

String: 555-867-5309

Regex:  /A{1,2} bonds/

String: "A bonds AA bonds AAA bonds"


Regex:  /\w+_\d+-\d+/

String: "report_1997-04 budget_03-04 memo_712539-100"

Regex:  /\w+_\d{2,4}-\d{2}/

String: "report_1997-04 budget_03-04 memo_712539-100"


### Greedy expressions

Expression tries to match the longest possible string

/\d+\w+\d+/ match  01_FY_07_report_99.xls

/".+", ".+"/ match "Milton", "Waddams", "Initech, Inc."

".+" can match whole string "Milton", "Waddams", "Initech, Inc."

/.+\.jpg/ matches "filename.jpg"


Regex:  /.+\.jpg/

String: "filename.jpg"

Regex:  /.*[0-9]+/

String: "Page 266"

/.*/ matches "Page 26" while /[0-9]+/ matches "6"


Regex:  /\d+\w+\d+/

String: "01_FY_07_report_99.xls"

Regex:  /".+", ".+"/

String: "Milton", "Waddams", "Initech, Inc."

### GLazy expressions

Lazy strategy mach as little as possible before giving control to the next expression part. (Opposite greedy)

Still defers to overall mach. 

Not necessarily faster or slower

Not supported by unix tools like BRE, ERE

`?` make preceding quantifier lazy

Syntax
- `*?`
- `+?`
- `{min,max}?`
- `??`

Remove the ? from each regex and watch the changes.

Regex:  /\w*?\d{3}/

String: "image_294"

Regex:  /[A-Za-z-.]+?\./

String: "Dr. Roberts, M.D."

Regex:  /.{4,8}_.{2,6}?/

String: "last_qtr_report.xls"

Regex:  /apples??/

String: "We picked apples."

Regex:  /\d+\w+?\d+/

String: "01_FY_07_report_99.xls"

Regex:  /".+?", ".+?"/

String: "Milton", "Waddams", "Initech, Inc."

### Efficiency when using repetition

Efficient matching + less backtracking = speedy results

Define the quantity of repeated expressions
- /.+/ is faster than /.*/
- /.{5}/ and /.{3,7}/ are even faster

Narrow the scope of the repeated expression
- /.+/ can become /[A-Za-z]+/

Provide clearer starting and ending points
- /<.+>/ can become /<[^>]+>/
- use anchors and word boundaries
- scans "picked" but not "icked", ..."ed", or "d"


Regex:  /\w*s/

String: "We picked apples."

Regex:  /\w+s/

String: "We picked apples."

Regex:  /[A-Za-z]+s/

String: "We picked apples."

Regex:  /\s[A-Za-z]+s/

String: "We picked apples."

Regex:  /\s[a-z]+s/

String: "We picked apples."

Regex:  /\s[a-z]{5}s/

String: "We picked apples."


[Content](#content)



## Grouping and Alternation Expressions

### Grouping metacharacters

`(` start grouped expression

`)`  end grouped expression

Group:
- apply repetition operators to a group
- makes expressions easier to read
- captures group for use in matching and replacing
- cannot be used inside character set

/(abc)+/ matches "abc" and "abcabcabc"

/(in)?dependent/ matches "independent" and "dependent"

/run(s)?/ is the same as /runs?/

Regex:  /[A-Z][0-9]/ (splited by 2 symbols)

String: "A1B2C3D4E5F6G7H8I9J0"

Regex:  /([A-Z][0-9])/ (splited by 2 symbols)

String: "A1B2C3D4E5F6G7H8I9J0"

Regex:  /([A-Z][0-9])+/ (entire string)

String: "A1B2C3D4E5F6G7H8I9J0"

Regex:  /([A-Z][0-9]){3}/ (splited into 3 parts)

String: "A1B2C3D4E5F6G7H8I9J0"

Regex:  /(in)dependent/ (second)

String: "dependent or independent"

Regex:  /(in)?dependent/ (both)

String: "dependent or independent"

Regex:  /runs?/ (both)

String: "I run fast. He runs faster."

Regex:  /run(s)?/ (both)

String: "I run fast. He runs faster."


### Alteration metacharacter

`|` match previous or next expression

| is OR operator - either match expression on the left or match expression on the right. Ordered, leftmost expression gets precedence. Multiple choices can be daisy-chained

Regex:  /apple|orange/g (match all separeted words)

String: "apple orange appleorange apple|orange"

Regex:  /abc|def|ghi|jkl/g  (abcdefghijkl)

String: "abcdefghijklmnopqrstuvwxyz"


Grouping is always a good idea, and sometimes required.

Regex:  /applejuice|sauce/ (match applejuice or sauce) 

String: "applejuice applesauce"

Regex:  /apple(juice|sauce)/g (both)

String: "applejuice applesauce"


Find misspelled words.

Regex:  /w(ei|ie)rd/g (both)

String: "weird and wierd"


### Writing logical and efficient alternation

Regex:  (peanut|peanutbutter) (peanut)

String: "peanutbutter"

Regex:  peanut(butter)? (match peanutbutter)

String: "peanutbutter"

Regex:  (\w+|FY\d{4}_report.xls) (match)

String: "FY2003_report.xls"


Turn off global matching and notice which gets matched.

Regex:  /abc|def|ghi|jkl/ (abc)

String: "abcdefghijklmnopqrstuvwxyz"

Regex:  /xyz|abc|def|ghi|jkl/ (abc)

String: "abcdefghijklmnopqrstuvwxyz"


Which is more efficient?

Put simplest expression first

Regex:  /\w+_\d{2,4}|\d{4}_\d{2}_\w+|export\d{2}/

Regex:  /export\d{2}|\d{4}_\d{2}_\w+|\w+_\d{2,4}/



### Repeating and nesting alternations

First matched alternation does not effect the next matches

/(AA|BB|CC){6}/ matches "AABBAACCAABB"

Regex:  /(\d\d|[A-Z][A-Z]){3}/ (all)

String: "112233 AABBCC AA66ZZ 11AA44"


Nesting check carefully

/(\d{2}([A-Z]{2}|-\d\w\d\w)|\d{4}(-\d{2}-[A-Z]{2,8}|_x[A-F]))/

Regex:  /(apple (juice|sauce)|milk(shake)?|sweet (peas|corn|potatoes))/ (except yogurt)

Regex:  /(apple juice|apple sauce|milk|milk shake|sweet peas|sweet corn|sweet potatoes)/ (except yogurt)

Regex:  /[\w ]+/ (all)

String: 
milk
apple juice
sweet peas
yogurt
sweet corn
apple sauce
milkshake
sweet potatoes


[Content](#content)



## Anchored Expressions

### Start and end anchors

`^` start of string/line

`$` end of string/line

`\A` start of string, never end of line

`\Z` end of string, never end of line

/^apple/ or /\Aapple/

/apple$/ or /apple\Z/

/^apple$/ or /\Aapple\Z/

`^` and `$` are supported in all regex engines

`\A` and `\Z` are supported in Java, .NET, PHP, Python, Ruby

Regex:  /[A-Z]/g (capital letters)

String: "Mr. Smith went to Washington."

Regex:  /^[A-Z]/g (only first M)

String: "Mr. Smith went to Washington."

Regex:  /\./g (both dots)

String: "Mr. Smith went to Washington."

Regex:  /\.$/g (only last dot)

String: "Mr. Smith went to Washington."

Regex:  /^[A-Z][A-Za-z.\- ]+\.$/g (entire string)

String: "Mr. Smith went to Washington."


Regex:  /^\w+@\w+\.[a-z]{3}$/g

String: "nobody@nowhere.com"

Regex:  /^\w+@\w+\.[a-z]{3}$/g (first)

String: "nobody@nowhere.com, somebody@somewhere.com"


Find whitespace

Regex:  /^[ \t]+/

String: "    It was a dark and stormy night."

Regex:  /[ \t]+$/

String: "And they lived happily ever after.      "

### line breaks and multiline mode

#### Single-line mode 

`^` and `$` do not match at line breaks

`\A` and `\Z` do not match at line breaks

Regex:  /^[a-z ]+/ (milk)


Regex:  /[a-z ]+$/ (last sweet potatoes if delete line return)



#### Using Multiline mode

`^` and `$` will match at the start and end lines

`\A` and `\Z` do not match at line breaks

Java: Pattern.compile("^regex$", Pattern.MULTILINE)

JavaScript: /^regex$/m

.NET: Regex.Match("string", "^regex$", RegexOptions.Multiline)

Perl: m/^regex$/m

PHP: preg_match(/^regex$/m, "string")

Python: re.search("^regex$", "string", re.MULTILINE)

Ruby: string.match(/^regex$/m)


Regex:  /^[a-z ]+/m (all)


Regex:  /[a-z ]+$/m


String:
milk
apple juice
sweet peas
yogurt
sweet corn
apple sauce
milkshake
sweet potatoes

### Word boundaries

`\b` word boundary (start/end of word)

`\B` not a word boundary



Reference a position, not an actual character

Conditions for matching
- before the first word character in the string
- after the last word character in the string
- between a word character and non-word character

word characters: [A-Za-z0-9_] or \w

/\b\w+\b/ finds 4 matches in "This is a test."

/\b\w+\b/ matches all of "abc_123" but only part of "top-notch"

/\BThis/ does not match "This is a test."

/\B\w+\B/ finds 2 matches "This is a test." (hi and es)

Regex:  /\b\w+\b/g (all words exclude ')

Regex:  /\b[\w']+\b/g (all words include ')

Regex:  /\b[\w']+?\b/

String: 
Shall I compare thee to a summer's day?
Thou art more lovely and more temperate:
Rough winds do shake the darling buds of May,
And summer's lease hath all too short a date.



#### Faster matches using word boundaries

Regex:  /\w+s/g (apples)

String: "We picked apples."

Regex:  /\b\w+s\b/g (apples)

String: "We picked apples."

`Caution!!! ` A space is not a word boundary
word boundaries reference a position
- not an actual character
- zero-length

string: "apples and oranges"

no match: /apples\band\boranges/
match: /apples\b and\b oranges/


[Content](#content)


## Capturing Groups and Backreferences


### Backreferences

Grouped expressions are captured
Stores the matched portion in parentheses

/a(p{2}l)e/ matches "apple" and stores "ppl"

Stores the data matched, not the expression
Automatically, by default

Backreferences allow access to captured data
Refer to first backreference with \1

`\1 through \9` backreference for positions 1 to 9

USAGE:
- can be used in the same expression as the group
- can be accessed after the match is complete
- cannot be used inside character classes

Support:
- most regex engines support \1 through \9
- some regex engines support \10 through \99
- some regex engines use $1 through $9 instead

Regex:  /(apples) to \1/

String: "apples to apples"

Regex:  /(ab)(cd)(ef)\3\2\1/

String: "abcdefefcdab"

Regex:  /(ab)(cd)(ef)(gh)(ij)\3\2\1\4\5/

String: "abcdefghijefcdabghij"

Regex:  /<(i|em)>.+?</\1>/

String: "<i>Hello</i>" and  "<em>Hello</em>" (match)

String: "<i>Hello</em>" and  "<em>Hello</i>" (does not match)

Regex:  /<(i|em)>.+?</\1>/

String: "<i>italics</i> <em>emphasis</em> <i>bad</em> <em>bad</i>"

Regex:  /<(i|em|b|strong)>.+</\1>/

String: "<b>bold</b> <strong>strong</strong>"

Regex:  /\b([A-Z][a-z]+)\b\s\b\1son\b/

String: "Steve Smith, John Johnson, Eric Erikson, Evan Evanson"(John Johnson and Evan Evanson)

Regex:  /\b(\w+)\s+\1\b/

String: "Paris in the 
         the spring."


### Backreferences to optional expressions

Regex:  /A?B/

String: "AB B" (both matches)


#### Captures occur on zero-width matches

Regex:  /(A?)B/

String: "AB B" matches "AB" and captures "A", matches "B" and captures ""

#### Backreferences become zero-width too

Regex:  /(A?)B\1/

String: "ABA B" matches "ABA" and "B"

Regex:  /(A?)B\1C/

String: "ABAC BC" matches "ABAC" and "BC"


Captures do not always occur on optional groups
*** Except in JavaScript ***

Regex:  /(A)?B/

String: "AB B"

Regex:  /(A)?B\1/

String: "ABA B" match "ABA"


#### Element is optional, group/capture is not optional

Regex:  /(A?)B/    matches "B" and captures ""

#### Element is not optional, group/capture is optional

Regex:  /(A)?B/    matches "B" and does not capture anything



### Find and replace using backreferences

TextMate for Macintosh http://macromates.com

Notepad++ for Windows https://notepad-plus-plus.org

Open `us_presidents.csv`

In editor: Find-> select Regular expression

Write a regex to match target data

Find:  /^\d{1,2},[\w. ]+? [\w ]+?,\d{4}/


Add capturing groups around anything that varies from row to row

Find:  /^(\d{1,2}),([\w. ]+?) ([\w ]+?),(\d{4})/


Write the replacement expression.
Keep all captures and add back anything not captured

Replace:  $1,$3,$2,$4 (use replace)

tosum up:
- create a regex that matches target data
- test regex and revise as needed
  - use anchors and specificity to narrow scope
- add capturing groups
  - capture anything that varies row-to-row
- write the replacement groups
  - use all captures
  - add back anything not captured but still needed
  - may need to use $1 instead of \1



### Non-Capturing group expressions

`?:` specify a non-capturing group

`?` give this group a different meaning

`:` the meaning is non-capturing

Syntax:
- /(\w+)/ becomes /(?:\w+)/

Turns off capture and backreferences
- optimize for speed
- preserve space for more captures

Support
- most regex engines except Unix tools

#### Two capturing groups

Regex:  /(oranges) and (apples) to \1/
String: "oranges and apples to oranges"


#### One non-capturing group and one capturing group

Regex:  /(?:oranges) and (apples) to \1/
String: "oranges and apples to apples"


[Content](#content)


## Lookaround Assertions

Lookahead assertions - what ought to be ahead. If expr fails, the match fails. Can be used any valid regex. Zero-width does not include group in the match.

`?=` positive lookahead assertion

syntax: /(?-regex)/

Regex:  /(?=seashore)sea/

String: "seashore seaside" match only sea in seashore

Regex:  /sea(?=shore)/

String: "seashore seaside" match only sea in seashore


### Contrast lookahead with capturing and non-capturing

Regex:  /sea(?:shore)/

String: "seashore seaside" match seashore

Regex:  /(sea)shore/

String: "seashore seaside" match seashore


### All words followed by a comma

Regex:  /\b[A-Za-z']+?\b,/ matched word and coma

String: (see self-reliance.txt) copy text to browser

Regex:  /\b[A-Za-z']+?\b(?=,)/ matched word without coma

String: (see self-reliance.txt)


### Compare with non-capturing

Regex:  /\b[A-Za-z']+?\b(?:,)/

String: (see self-reliance.txt)


### Double-testing with lookahead assertions

Regex:  /\d{3}-\d{3}-\d{4}/

String: "
555-302-4321
555-781-6978
555-245-1312
"

Regex: /^[0-5\-]+$/ matches 555-302-4321 and 23140-5

!!!! Make sure multiline anchors are enabled.

Regex:  /(?=^[0-5\-]+$)\d{3}-\d{3}-\d{4}/m

String: "
555-302-4321
555-781-6978
555-245-1312
"
Regex:  /(?=^[0-5\-]+$)(?=.*4321)\d{3}-\d{3}-\d{4}/m

String: "
555-302-4321
555-781-6978
555-245-1312
"

#### All words containing a "gh" and followed by a comma.

Regex:  \b[A-Za-z']+?\b(?=,)

String: (see self-reliance.txt) copy text to browser

Regex:  \b(?=\w*gh)[A-Za-z']+?\b(?=,)

String: (see self-reliance.txt)


#### Password must be 8-15 characters

Regex:  /^.{8,15}$/

String: "swordfish"


#### Password must be 8-15 characters and contain 1 digit

Regex:  /^(?=.*\d).{8,15}$/

String: "sword42fish"


#### Password must be 8-15 characters and contain 1 digit and 1 capital letter

Regex:  /^(?=.*\d)(?=.*[A-Z]).{8,15}$/

String: "sword42Fish"

### Negative lookahead assertions

`?!` negative lookahead assertion

/(?!regex)/

/(?!seashore)sea/ match sea in seashore 

/online(?! training) does not match "online training"

/online(?!.* training) does not match "online video training"

Regex:  /\bblack\b(?! dog)/

String: "The black dog followed the black car into the black night." match second black

#### Contrasted with the positive lookahead assertion

Regex:  /\bblack\b(?= dog)/

String: "The black dog followed the black car into the black night." match fist black


Regex:  /(?=^[0-5\-]+$)(?=.*4321)\d{3}-\d{3}-\d{4}/m (first)

String: "
555-302-4321
555-781-6978
555-245-1312
"

Regex:  /(?=^[0-5\-]+$)(?!.*4321)\d{3}-\d{3}-\d{4}/m (last)

String: "
555-302-4321
555-781-6978
555-245-1312
"

#### All words NOT followed by a comma.

Regex:  /\b[A-Za-z']+?\b(?=,)/

String: see self-reliance.txt  copy text to browser

#### All words NOT followed by a comma.

Regex:  /\b[A-Za-z']+?\b(?!,)/

String: see self-reliance.txt

#### All words NOT followed by a comma or period

Regex:  /\b[A-Za-z']+?\b(?![,.])/

String: see self-reliance.txt


#### Last occurrence: an item that isn't followed by itself.

Regex:  /\bblack\b(?!.*\bblack\b)/

String: "The black dog followed the black car into the black night."

Regex:  /(\bblack\b)(?!.*\1)/

String: "The black dog followed the black car into the black night."

### Lookbehind assertions 

`?<=` positive lookbehind assertions 

`?<!` negative lookbehind assertions 

Lookbehind assertions - what ought to be behind. If expr fails, the match fails. Can be used any valid regex. Zero-width does not include group in the match.

syntax: 

/(?<=regex)/

/(?<!regex)/

supported: .NET, Java, Perl, PHP, Pytho, Ruby 1.9

not supported: JavaScript, Ruby 1.8, Unix

#### Will not work in JavaScript!

Regex:  /(?<=base)ball/

String: "I like baseball and football." matches ball in baseball

Regex:  /(?!=base)ball/

String: "I like baseball and football." matches ball in both

Regex:  /(jamin|ny)/

String: "Benny Benjamin Jenny Lenny" match ends of all words

Regex:  /(?<=Ben)(jamin|ny)/

String: "Benny Benjamin Jenny Lenny" match nothing JS (ny in Benny)

Regex:  /(?<=Ben|Jen)(jamin|ny)/

String: "Benny Benjamin Jenny Lenny" match nothing JS (ends of first 3 words)

Regex:  /(?<!Ben|Jen)(jamin|ny)/

String: "Benny Benjamin Jenny Lenny" match nothing JS (ny in Lenny)


### The power of positions

Allows testing of a regex apart from matching

- peek forwards or backwards /sea(?=shore)/

- match a string using multiple expressions /^(?=.*\d)(?=.*[A-Z]).{8,15}$/

- define rejection expressions /online(?! training)/

- find last occurence /(item)(?!.*\1)/

Zero-width means zero position movement /(?=seashore)sea/ matches sea in seashore

#### These will not work in JavaScript!

Regex:  /(?<![$\d])\d+\.\d\d/

String: "This costs 53.00 or $54.00." matches 53.00


#### Insertion by using all assertions

Regex:  /(?<![$\d])(?=\d+\.\d\d)/

String: "This costs 53.00 or $54.00."

Replace: "$" (use notepad++) 53


#### Adding commas to delimit a number

String: "An astronomical unit is 149597870.7 kilometers, approximately the average distance between the Sun and Earth."

Regex:  /(\d\d\d)+/

Regex:  /(?<=\d)(\d\d\d)+(?!\d)/

Regex:  /(?<=\d)(?=(\d\d\d)+(?!\d))/

Replace: ","


[Content](#content)




## Unicode and Multibyte Characters

Single byte
- uses 1 byte(8 bit) to represent a character
- allows for 256 characters
- A-Z, a-z, 0-9, punctuation, common symbols

Double byte
- uses 2 bytes(16 bit) to represent a character
- allows for 65536 characters

Many more characters than English alphabet

over 109000 characters

Unicode
- variable byte size
- maintains compatibility with one- and two-byte encoding
- mapping between a character and a number
- "U+" followed by a four-digit hexadecimal number

`é can be U+00E9 or ..`

### Unicode in regex

(Mac users can access special characters from "Edit > Special Characters")

`\u` unicode indicator 

supported: java, js, .NET, python, ruby

perl and PHP use `\x`

Regex:  /cafe/

String: "cafe café café" match first

Regex:  /café/

String: "cafe café café"

Regex:  /caf\u00E9/

String: "cafe café café"

Regex:  /caf\u0065\u0301/

String: "cafe café café"


### Unicode wildcard and properties


`\X` is only supported in Perl and PHP
Not supported in JavaScript

matches any single character

always matches line breaks(like /./s)

`\p{property}` property

matches characters that have a property

/\p{Mark}/ or /\p{M}/ matches any "mark"(accents)

/\p{Letter}/ or /\p{L}/ matches any letter

| property   | abbreviation |
| -------- | ------- |
| Letter  | L   |
| Mark | M    |
| Separator    | Z    |
| Symbol   | S  |
| Number  | N  |
| Punctuation | P  |
| Other   |  C  |


`\P{property}` not property (matches characters that do not have property)

supported: java, .NET, ruby, php, perl

not: js, python and unix tools

Regex:  /caf\X/

String: "cafe café café"


\p and \P are only supported in Java, .NET, Perl, PHP, Ruby
Not supported in JavaScript

Regex:  /caf\P{M}\p{M}/

String: "cafe café café"


[Content](#content)



## Useful Regular Expressions

### Expressions content

[Regular expression to match a year](#regular-expression-to-match-a-year)

[Use anchors, delimiters, and context](#use-anchors-delimiters-and-context)

[Match names](#match-names)

[Post codes](#post-codes)

[Match email](#match-email)

[Match url](#match-url)

[Decimal numbers](#decimal-numbers)

[IP](#ip)

[Date](#date)

[Time](#time)

[Tag](#tag)

[Password](#password)

[Credit card](#credit-card)

[Word near word](#word-near-word)

[Replace](#replace)

[Content](#content)

#### Regular expression to match a year

Regex:  /\d{4}/

String: "2005 0000 9999"

Regex:  /(19|20)\d\d/

String: "2005 0000 9999 1900 2099"

Regex:  /(19[5-9]\d|20[0-4]\d)/

String: "2005 0000 9999 1900 2099 1950 2049"

[Expressions content](#expressions-content)

#### Use anchors, delimiters, and context

Regex:  /\w+/

String: "%^@X&*!"

Regex:  /^\w+$/

String: "%^@X&*!"

[Expressions content](#expressions-content)

[Content](#content)

### Match names

Regex:  /\w+/

String: "
Kevin
Lynda
Charlie
Lucy
Linus
Sally
"

Regex:  /^\w+$/m

String: "$kevin"

Regex:  /^[A-Za-z]+$/m

String: "0kevin"

#### Does first letter have to be capitalized?

Regex:  /^[A-Z][A-Za-z]+$/m

String: "kevin"

Regex:  /^[A-Z][A-Za-z.'\-]+$/m

String: "J.R."

#### Match first and last name

Regex:  /^[A-Z][A-Za-z.'\- ]+$/m

String: "George Washington"

#### Capture first and last name

Regex:  /^([A-Z][A-Za-z.'\-]+) ([A-Z][A-Za-z.'\-]+)$/m

String: "George Washington"

#### Capture first, middle, and last name

Regex:  /^([A-Z][A-Za-z.'\-]+) (?:([A-Z][A-Za-z.'\-]+) )?([A-Z][A-Za-z.'\-]+)$/m

String: "John Quincy Adams"

#### Tough call

String: "Martin Van Buren"

[Expressions content](#expressions-content)

[Content](#content)


### Post codes

#### U.S. postal codes

Regex:  /\d{5}/

String: "
75087
10010-6543
123456789
"

Regex:  /^\d{5}$/m

Regex:  /^\d{5}(-\d{4})?$/m


#### Canada postal codes

Regex:  /^[A-Z]\d[A-Z] \d[A-Z]\d$/m

String: "A9A 9A9"


#### UK postal codes

Regex: /^[A-Z]{1,2}\d{1,2}[A-Z]? \d[A-Z][A-Z]$/m

String: "
A9 9AA
A99 9AA
AA9 9AA
AA99 9AA
A9A 9AA
AA9A 9AA
"

#### Allows an invalid format by accident

String: "AA99A 9AA"

Regex:  /^[A-Z]{1,2}\d{1,2}|[A-Z]{1,2}\d[A-Z] \d[A-Z][A-Z]$/m


#### From http://en.wikipedia.org/wiki/Postcodes_in_the_United_Kingdom

Regex: /(GIR 0AA|[A-PR-UWYZ]([0-9][0-9A-HJKPS-UW]?|[A-HK-Y][0-9][0-9ABEHMNPRV-Y]?) [0-9][ABD-HJLNP-UW-Z]{2})/


[Expressions content](#expressions-content)

[Content](#content)

### Match email

Regex:  /^\w+@\w+\.\w{3}$/

String: "someone@somewhere.com"

Regex:  /^[\w.%+\-]+@[\w.\-]+\.\w{2,3}$/

String: "someone@somewhere.co.uk"

Regex:  /^\w+@[\w.\-]+\.[A-Za-z]{2,3}$/

String: "someone@somewhere.co.uk"

#### Email and domain specifications allow other characters

Regex:  /^[\w.%+\-]+@[\w.\-]+\.[A-Za-z]{2,3}$/

Regex:  /^[\w.%+\-]+@[\w.\-]+\.[A-Za-z]{2,6}$/

String: "someone@somewhere.museum"

#### Top-level domain verfication
Regex:  /^[\w.%+\-]+@[\w.\-]+\.([A-Za-z]{2}|aero|asia|biz|cat|com|coop|edu|gov|info|int|jobs|mil|mobi|museum|name|net|org|pro|tel|travel|xxx)$/

String: "someone@somewhere.museum"

[Expressions content](#expressions-content)

[Content](#content)


### Match url


String: "
http://www.nowhere.com
http://nowhere.com
http://blog.nowhere.com
https://www.nowhere.com
http://www.nowhere.com/product_page.html
http://www.nowhere.com/images/image.gif
http://www.nowhere.com/product/
http://www.nowhere.com/product/3456
http://www.nowhere.com/product_page.php?product=28
http://www.nowhere.com?product=28&color=blue
http://www.nowhere.com#details
"

#### Protocol portion

Regex:  /^https?:\/\//

Regex:  /^(http|https):\/\//

#### Domain portion

/^(http|https):\/\/[\w.\-]+\.[A-Za-z]{2,6}/

/^(http|https):\/\/[\w\-_]+(\.[\w\-_]+)+/

#### Query string portion

Regex:  /^(http|https):\/\/[\w\-_]+(\.[\w\-_]+)+.*$/

Regex:  /^(http|https):\/\/[\w\-_]+(\.[\w\-_]+)+[/?#]?.*$/

Regex:  /^(http|https):\/\/[\w\-_]+(\.[\w\-_]+)+[\w\-.,@?^=%&:/~\\+#]*$/

#### Make groups non-capturing

Regex:  /^(?:http|https):\/\/[\w\-_]+(?:\.[\w\-_]+)+[\w\-.,@?^=%&:/~\\+#]*$/

[Expressions content](#expressions-content)

[Content](#content)


### Decimal numbers

String: "
5.1
314.27918
0.123
.345
23
"

Regex:  /^\d+\.\d+$/m

Regex:  /^\d?\.\d+$/m

Regex:  /^\d*\.?\d*$/m

#### If everything is optional, it matches an empty string!

Regex:  /^(\d*\.\d+|\d+)$/m


#### Currency

String: "
$50
$43.23
$0.39
$.60
"

Dollar

Regex:  /^\$(\d*\.\d{2}|\d+)$/m

#### British Pound

String: "£498.10"

Regex:  /^(\$|£)(\d*\.\d{2}|\d+)$/m

Regex:  /^(\$|\u00A3)(\d*\.\d{2}|\d+)$/m

#### Japanese Yen

String: "¥32.76"

Regex:  /^(\$|\u00A3|¥)(\d*\.\d{2}|\d+)$/m

Regex:  /^(\$|\u00A3|\u00A5|\uFFE5)(\d*\.\d{2}|\d+)$/m

[Expressions content](#expressions-content)

[Content](#content)

### IP 

String: "
255.255.255.255
0.0.0.0
67.52.159.38
067.052.159.038
"

Regex:  /\d+\.\d+.\d+\.\d+/m

String: "999.999.999.99999999"

Regex:  /\d{1,3}\.\d{1,3}.\d{1,3}\.\d{1,3}/m

String: "999.999.999.999"

Regex:  /[012]?[0-9]?[0-9]/m

String: "299.299.299.299"


#### Breaking down 255

#### 250-255

Regex:  /25[0-5]/

String: "200 255"

#### 200-249

Regex:  /2[0-4][0-9]/

String: "200 249"

#### 100-199

Regex:  /1[0-9][0-9]/

String: "100 199"

#### 000-099

Regex:  /0?[0-9]?[0-9]/

String: "0 000 99 099"

#### 000-099 (faster)

Regex:  /0?[0-9][0-9]?/

String: "0 000 99 099"

#### 000-199

Regex:  /[01]?[0-9][0-9]?/

String: "0 000 99 099 100 199"

#### 000-255

Regex:  /(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)/

String: "0 000 99 099 100 199 200 249 200 255 256 299"


#### IP Address

Regex: /^(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$/m

String: "
255.255.255.255
0.0.0.0
67.52.159.38
067.052.159.038
999.999.999.999
299.299.299.299
256.256.256.256
"

[Expressions content](#expressions-content)

[Content](#content)

### Date

String: "
2000-11-15
2000-6-9
2000-06-09
2000/6/9
"

Regex:  /^\d\d\d\d-\d\d-\d\d$/m

Regex:  /^\d{4}-\d{1,2}-\d{1,2}$/m

Regex:  /^\d{4}[-/]\d{1,2}[-/]\d{1,2}$/m


#### Month should be 1-12

String: "2000-14-55"

Regex:  /^\d{4}[-/](0?[1-9]|1[012])[-/]\d{1,2}$/m


#### Date should be 1-31

String: "2000-12-55"

Regex:  /^\d{4}[-/](0?[1-9]|1[012])[-/](0?[1-9]|[12][0-9]|3[01])$/m


#### Year between 1950-2050

String: "
1949-12-31
1950-12-31
2050-12-31
2051-12-31
"

Regex:  /^(19[5-9][0-9]|20[0-4][0-9]|2050)[-/](0?[1-9]|1[012])[-/](0?[1-9]|[12][0-9]|3[01])$/m


#### On your own

String: "January 31, 2012"

Regex:  ?

[Expressions content](#expressions-content)

[Content](#content)



### Time


String: "
2:34
2:34pm
2:34PM
02:34
14:34
14:34:56
14:34 EST
14:34 GMT -5
"

#### 12 hour time

Regex:  /^\d:\d\d$/m

Regex:  /^\d{1,2}:\d{2}$/m

String: "99:99"

Regex:  /^(0?[1-9]|1[0-2]):[0-5][0-9]$/m


#### Optional am/pm

Regex:  /^(0?[1-9]|1[0-2]):[0-5][0-9](am|pm|AM|PM)?$/m

Regex:  /^(0?[1-9]|1[0-2]):[0-5][0-9]([aApP][mM])?$/m


#### 24 hour time

String: "
0:02
23:45
24:45
"

Regex:  /^(0?[0-9]|1[0-9]|2[0-3]):[0-5][0-9]$/m

Regex:  /^([0-1]?[0-9]|[2][0-3]):[0-5][0-9]?$/m


#### Optional seconds

Regex:  /^([0-1]?[0-9]|[2][0-3]):[0-5][0-9](:[0-5][0-9])?$/m


#### Timezone

Regex:  /^([0-1]?[0-9]|[2][0-3]):[0-5][0-9](:[0-5][0-9])?( [A-Z]{3})?$/m

Regex:  /^([0-1]?[0-9]|2[0-3]):[0-5][0-9](:[0-5][0-9])?( ([A-Z]{3}|GMT [-+]([0-9]|1[0-2])))?$/m

[Expressions content](#expressions-content)

[Content](#content)


### Tag

String: "
<strong>Bold</strong>
<em>Emphazied</em>
<b>Bold</b>
<i>Italics</i>
<span id="foo" class="bar">Some text</span>
<hr />
"

Regex:  /^<strong>(.*?)</strong>$/m

Regex:  /^<(strong|em)>(.*?)</(strong|em)>$/m


#### Balancing tags

String: "<strong>Mistake</em>"

Regex:  /^<(strong|em)>(.*?)</\1>$/m


#### Flexibility

Regex:  /^<(strong|em|b|i)>(.*?)</\1>$/m

Regex:  /^<(.+?)>(.*?)</\1>$/m

Regex:  /^<([^>]+)>(.*?)</\1>$/m


#### Tag attributes

Regex:  /^<([A-Za-z][A-Za-z0-9]*)\b[^>]*>(.*?)</\1>$/m


#### Self-closing tags

Regex:  /^<(([A-Za-z][A-Za-z0-9]*)\b[^>]*>(.*?)</\1>|[A-Za-z][A-Za-z0-9]*\b[^/>]*/>)$/m

Regex:  /^<(?:([A-Za-z][A-Za-z0-9]*)\b[^>]*>(?:.*?)</\1>|[A-Za-z][A-Za-z0-9]*\b[^/>]*/>)$/m

[Expressions content](#expressions-content)

[Content](#content)


### Password

Password requirements
May contain any character except space
At least 8 characters long
No more than 15 characters long
Must include at least one uppercase letter
Must include at least one lowercase letter
Must include at least one numeric digit
Must include at least one symbol

String: "swordfish"

Regex:  /^.+$/m

#### May contain any character except space

Regex:  /^\S+$/m

####  At least 8 characters long
####  No more than 15 characters long

Regex:  /^\S{8,15}$/m

####  Must include at least one uppercase letter

Regex:  /^(?=.*[A-Z])\S{8,15}$/m

String: "swordFish"

####  Must include at least one lowercase letter

Regex:  /^(?=.*[A-Z])(?=.*[a-z])\S{8,15}$/m

####  Must include at least one numeric digit

Regex:  /^(?=.*\d)(?=.*[A-Z])(?=.*[a-z])\S{8,15}$/m

String: "sword42Fish"

####  Must include at least one symbol

Regex:  /^(?=.*\d)(?=.*[~!@#$%^&*()_\-+=|\\{}[\]:;<>?/])(?=.*[A-Z])(?=.*[a-z])\S{8,15}$/m

String: "sword#42Fish"

[Expressions content](#expressions-content)

[Content](#content)


### Credit card

String: "
American Express
370012345612345
3700-123456-12345

Visa
4000123412341234
4000-1234-1234-1234

Mastercard
5100123412341234
5100-1234-1234-1234

Discover
6011123412341234
6011-1234-1234-1234
"

Regex:  /^\d+$/m

Regex:  /^[\d\- ]+$/m

#### Correct length

Regex:  /^[\d\- ]{15,16}$/m

Regex:  /^[\d\- ]{15,19}$/m

#### Correctly delimited (without Amex)

Regex:  /^\d{4}[\- ]?\d{4}[\- ]?\d{4}[\- ]?\d{4}$/m

#### Require same delimter

String: "40001234-1234 1234"

Regex:  /^\d{4}([- ]?)\d{4}\1\d{4}\1\d{4}$/m

#### Validate by type
####   Visa prefix: 4
####   Mastercard prefix: 51-55
####   Discover prefix: 6011

Regex:  /^[456]\d{3}([\- ]?)\d{4}\1\d{4}\1\d{4}$/m

Regex:  /^(?:4\d{3}|5[1-5]\d{2}|6011)([\- ]?)\d{4}\1\d{4}\1\d{4}$/m


#### American Express

#### Length 15, prefix 34 or 37

Regex:  /^3[47]\d{13}$/m

#### Format is 4-6-5

Regex:  /^3[47]\d{2}([\- ]?)\d{6}\1\d{5}$/m


#### Put it all together

Regex:  /^(?:3[47]\d{2}([\- ]?)\d{6}\1\d{5}|(?:4\d{3}|5[1-5]\d{2}|6011)([\- ]?)\d{4}\2\d{4}\2\d{4})$/m


[Expressions content](#expressions-content)

[Content](#content)


### Word near word

String: use self-reliance.txt

#### Word1 near word2

Regex:  /[Aa].*[Mm]an/

Regex:  /[Aa](.+)[Mm]an/

Regex:  /[Aa](?:.+)[Mm]an/

Regex:  /[Aa](?:.+?)[Mm]an/

#### Use word boundaries

Regex:  /\b[Aa]\b(?:.+?)\b[Mm]an\b/

#### Don't cross punctuation

Regex:  /\b[Aa]\b(?:[^.,;]+?)\b[Mm]an\b/

#### Up to 20 characters between

Regex:  /\b[Aa]\b(?:[^.,;]{1,20}?)\b[Mm]an\b/

#### Up to 5 words between

Regex:  /\b[Aa]\b (?:\w+[\- :;.]){0,5}\b[Mm]an\b/

#### Lookahead assertions can control the match

Regex:  /\b[Aa]\b(?= (?:\w+[\- :;.]){0,5}\b[Mm]an\b)/

 Lookbehind assertions are not possible due to repetition and variable length


[Expressions content](#expressions-content)

[Content](#content)

### Replace


use  `midsummer_nights_dream.txt` in notepad++

#### Replace first

##### ( to [

Regex:    /^\(/

Regex:    /\n\n\(/

Replace:  "\n\n\n["

##### Did we miss any?

Regex:    /\n^(/

Replace:  "\n["

##### ) to ]

Regex:    /)$/

Replace:  "]"

#### Replace second


Regex:    /ACT ([A-Z]+?)\nSCENE ([A-Z]+?)\. (.+?)\n/

Replace:  "----------
Act: $1
Scene: $2
Location: $3
----------
"

#### Replace third

##### "THESEUS\n" to "THESEUS: "

Regex:    /[A-Z]+/

Regex:    /^[A-Z]+$/

Regex:    /^([A-Z]+)\n/

Replace:  "$1: "

##### Add four spaces of indentation to spoken lines

Regex:    /^[A-Z]+: /

Regex:    /^(?![A-Z]+: )/

Regex:    /^(?!([A-Z]+: |[\[\-]))/

Regex:    /^(?!([A-Z]+: |\n|[\[\-]))/

Regex:    /^(?!([A-Z]+: |\n|[\[\-]|Act: |Scene: |Location: ))/

Replace:  "    "


[Expressions content](#expressions-content)

[Content](#content)



