# COMMON COMMANDS

`ls` : print files

    ls -R # recursively print files
    ls -a # show all (hidden too) files

`cd` : change directory

    cd - # move to the last opened directory

`grep`, `rg` : find by symbol

    rg -A1 # show 1 line above match
    rg -B1 # show 1 line before match
    rg -C1 # show 1 line above and before match (C for context)
    rg -i # case insensitive
    rg -o # print only the part that matched

`less` : file/output pager

    less file.txt
    alias | less #  execute command alias and pipe its output as the input of less

Shortcuts: N for going to the next search match, Shift-N for going to prev match

`man` : command manual

    man ls

`type` : print the type of a command
    
    type ls
    type -a ls # print all types of a command

For example the command `echo` is a shell built-in and also an external programm, so `type -a` helps finding approriate documentation.
For echo the documentation can be queried by `man echo` and `help echo` in bash

`file` : determine file type

    file test.txt

`tr` : translate characters, replace symbol 'a' by symbol 'b'

    `echo $PATH | tr : '\n' # replace symbol ':' by a symbol '\n'

`test` : condition evaluation utility

`sleep` : suspend execution

# SHELL OPERATORS

`>` : write to the file, overwrite by the output

    echo "hello" > file 

`>>` : append the file by output

    echo "hello" >> file 

`<` : read from a file

    echo < greeting.txt

`|` : pipe the data (output) to the program

    cat file.txt | grep apple # print the content of file.txt, send it as an input of the grep command where it should find the word "apple"



# SCRIPTING 

To mark the file as bash executable it is required to add a header with a specific syntax  `!#path_to_executor`

    !#/usr/bin/env bash


## INPUT

`read` : read a line from stdin

    read -p -r "Enter your name: " name # print prompt and assign input to the variable "name", -r is for raw, do not parse special characters as backslaches

## COMMANDS

`exit` : alternative of `return` but outside of a function

## OPERATORS

`[]` or `[[]]` : test lexical expression 

    if [[ $name == "john" ]] ...

`(())` : test mathematical expression
    
    if (( $age > 18 )) ...


## VARIABLES

    name=john
    echo $name 

The syntax of setting a variable by `var_name=$(command)` will set the output of the command as the variable value 

    path_copy=$(echo "$PATH")
    echo $path_copy # print the value of $PATH

The script can be run with arguments

    ./script foo bar baz

Then it can be readed by $[N] variable, $0 is a script name, $1 is a fisrt argument, $2 is a second argument etc.

    # ./script file

    echo $1 $2 $3 # foo bar baz

Variable `$?` has the value which is the exit code of the previous command

    echo hello
    echo $? 

    # output
    hello
    0

Variable `$@` is a list of passed arguments

Variable `$#` is a number of passed arguments


## LOOP

    for thing in foo bar baz; do
        echo "thing is $thing"
    done
    
    # output
    thing is foo
    thing is bar
    thing is baz

Loop through all passed arguments to a script

    for thing in "$@"; do
        echo "$thing"
    done

Generate mathematical progression

    max=5
    for ((i = 0; i < max; i++)); do
        echo "$i"
    done
    

## FUNCTIONS

    greet() {
        local name=$1

        echo "Hello, $name"
    }

Variables in a function are assigned as global variables, to avoid this the `local` keyword is used


## CONDITIONS

Expression between `[]` is the same as the command `test`, `[[]]` - is a bash enhanced version  that brings a bit more feature

    a=2
    b=2

    if [[ $a == $b ]]; then       # could be `if test $a == $b; then
        echo "a is equal to b"
    fi

    while [[ $a == $b ]]; do     
        echo "a is equal to b"
    done
    
Boolean is `true` or `false`

    true
    echo $? # 0

    false
    echo $? # 1


### CASE STATEMENT

    case "$name" in
        john)
            echo "hi john"
            ;;
        dave)
            echo "hi dave"
            ;;
        *)
            echo "hello anyway"
    esac
    
    # compact 
    case "$name" in
        john) echo "hi john";;
        dave) echo "hi dave";;
        *) echo "hello anyway"
    esac
    
Case statement operators:
`;;` : break
`;&` : always fallthrough, when the condition is true, all next branches will be automatically true

    case "$true_value" in
        true)
            echo "the value is true" ;&
        false)
            echo "the value is false" ;&

    # output
    the value is true
    the value is false

`;;&` : if true, continue but do not set next branches automatically true


    case "$true_value" in
        true)
            echo "the value is true" ;;&
        false)
            echo "the value is false" ;;&
        true)
            echo "the value is true" ;;&

    # output
    the value is true
    the value is true

## DATA STRUCTURES

### ARRAY

    array=(foo bar baz)
    echo "${array[0]}" # foo
    echo "${array[-1]}" # baz

    idx = 2
    echo "${array[idx]}"

Iterating through items

    for item in "${array[@]}"; do
        echo "$item"
    done

Manually declaring an array

    declare -a array=(foo bar baz)
    
Copying

    array_1 = (foo bar baz)
    array_2 = ( "${array_1[@]}" )

Pushing

    array = (foo bar baz)
    array+=(guy john)


