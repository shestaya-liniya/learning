# COMMON COMMANDS

`ls` : print files

    ls -R : recursively print files
    ls -a : show all (hidden too) files

`cd` : change directory

    cd - : move to the last opened directory

`grep`, `rg` : find by symbol

    rg -A1 : show 1 line above match
    rg -B1 : show 1 line before match
    rg -C1 : show 1 line above and before match (C for context)
    rg -i : case insensitive
    rg -o : print only the part that matched

`less` : file/output pager

    less file.txt
    alias | les :  execute command alias and pipe its output as the input of less

    N for going to the next search match, Shift-N for going to prev match

`man` : command manual

    man ls

`type` : print the type of a command
    
    type ls
    type -a ls : print all types of a command

    For example the command 'echo' is a shell built-in and also an external programm, so 'type -a' helps finding approriate documentation.
    For echo the documentation can be queried by 'man echo' and 'help echo' in bash or in a zsh builtins manual by 'man zshbuiltins'

`file` : determine file type

    file test.txt

`tr` : translate characters, replace symbol 'a' by symbol 'b'

    `echo $PATH | tr : '\n'` replace symbol ':' by a symbol '\n'

# SHELL OPERATORS

`>` : overwrite file by the output

    echo "hello" > file 

`>>` : append the file by output

    echo "hello" > file 

`|` : pipe the data (output) to the program

    cat file.txt | grep apple :  print the content of file.txt, send it as an input of the grep command where it should find the word "apple"



# SCRIPTING 

To mark the file as bash executable it is required to add a header with a specific syntax  `!#path_to_executor`

    !#/usr/bin/env bash


### INPUT

`read` : read a line from stdin

    read -p "Enter your name: " name : print prompt and assign input to the variable "name"


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


# FUNCTIONS

    greet() {
        local name=$1

        echo "Hello, $name"
    }

Variables in a function is assigned as a global variable, to avoid this the `local` keyword is needed







