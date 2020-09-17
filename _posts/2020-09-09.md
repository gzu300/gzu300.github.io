---
title: 'Three Musketeers' in bash
date: 2020-09-09
---
## `sed`
### Synopsis
`sed [command line flags] command [file]`  
`command` has different components: `[address1[,address2]]function[arguments]`  
addresses mean the line range or pattern of the input file. For example `sed 1,100 s/abc/ABC/ example.txt`. `1,100` are the 2 addresses.  
functions may receive 0, 1 or 2 addresses. represented by 0addr, 1addr or 2addr in the below text.  
pattern space: the current matched line is buffered into pattern space except for some special commands.  
hold space: the pattern to be matched
#### common one-line functions
1. `[1addr[,2addr]] s/regex/pattern/flags`  
flags:  
N: is the number, meaning the N th occurance  
g: make change to all non-overlapping matched pattern  
p: print to output when replacement made.  
w: write to a file if replacement made.  
2. `[1addr]a\`  
`text`  
append the text below the matched line.
3. `[1addr[,2addr]]c\`  
`text`  
replace the current line with `text`. **if addresse is a range, then replace the range with one single line of text**. 
4. `[1addr]i\`
`text`
insert the text above the matched line.
5. `y/source pattern/transformed pattern/`  
transform character sets. If wanto to transform set of regex, need to use multiple `s` commands.
#### command line flags
`-e` when considering multiple arguments for commands, use it.
#### advanced one-line functions on pattern and hold spaces
`g` replace hold space with pattern space. `G` append pattern space to hold space.  
`h` replace pattern space to hold space. `H` append hold space to pattern space.
`d` and `D` deletes the current pattern space.
`e` exchange hold and pattern space.
#### advanced multiple-line function
`N` `P` `D` commands includes the next line till by including newline character into buffer. So it operates on multiple lines. refer to manual when need this function.  
usually called before other commands in a functoin list `{}`.
### summary
#### when need to use regex to match pattern, used `sed`.
#### `sed` is a **stream** editer for **TRANSFORMING** and **FILTERING** input text ONE LINE AT A TIME.
#### the synopsis of `sed` is always `command-line flags`+`[address] function|{functions} [arguments]`+`< input file` + `> output file`
#### the most common and useful command in sed is the s command. make well used of it.

## `awk`

Different shells use different versions of awk. **Linux** uses `gawk`. **Mac** uses `nawk`. But nowawadys, shell scripting languages are more of a convienent and light weight tools for data processing. So only commands in `awk` is sufficient and fast.

### synopsis
`awk '[BEGIN {exp1[ ; exp2]}] { } END {exp1 [; exp2]}' [file]`  
`if () {} [else {}]`  
`for () {}`  
`while () {}`  
`printf(format[,expression_list])`

### built-in variables
`FS`, `OFS` field seperator  
`RS`, `ORS` carriage seperator
`NF`, `NR`  number of field, line
`FILENAME`  
### expressions
regular expressions: word [~|!~] /regex/
boolean operators: `&&`, `||`, `~`  
conditional expressions:  >, <, ...  
arithmetic expressions:  
assignment expressions: +=, -=, ++, **array[string|number] = expression** ...  
### functions
convienent functions for numbers and strings
numerical functions  
string functions  
self-defined functions
### flow control
`break`  
`continue`  
`next` skip the current line. run the command againe on the next line.   
`exit [1|2]`
### I/O
`>`, `>>` put **Inside** the script, to write to file.
### summary
#### when operating structure data, use `awk`.
#### operate more complex data. more suitable for structured data.
#### generally more sophisticated than `sed`, making the use scenario of `sed` more limited to simple substitution.

## grep

### flags
`-v` inverse selection  
`-o` output only matched world  
`-c` count the number of lines selected  


