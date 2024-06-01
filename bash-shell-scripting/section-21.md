# Linux Administration: The Complete Linux Bootcamp For 2024
### Date: 6/1/2024

## Section 21: Bash Shell Scripting
  - The `#!` is used to define the interpreter for the script and it can point to the binary of any scripting language(not just bash).
    - `#!/usr/bin/env bash` - Bash
    - `#! /usr/bin/python3` - Python
  - There are two main ways of running scripts in the terminal:
    1. `./my-bash-script.sh` - Runs the script in a new shell process & if anything is returned it will be displayed in the terminal
    2. `source my-bash-script.sh` - Runs the script in the current shell & if anything is returned it will be stored in the shell variable `SCRIPT_OUTPUT`
       - `. my-bash-script.sh` - is the same as `source my-bash-script.sh`
  
  ### Variables In Bash
    - Variables are used to store information in the shell
    - `$` is used to reference a variable
    - `$1` is used to reference the first argument passed to the script
    - To see all functions & variables use `env` or `set`
      - The `set` command often prints too much output, so it's reccomended to pipe it's output to less `set | less` or `set | grep VAR_NAME` to filter and see specific variables
    - To unset a variable use `unset VAR_NAME`
    - OS env variables that are predefined are often all capitalized such as `$PATH` or `$SHELL`
    
    #### Env Variables
    - Defined for the current shell and are inherited by any child shells or processes spawned by the shell.
    - They are used to pass information to the processes that are spawned from the current shell.
    - To see all env variables use `env` or `printenv`.
    
    #### Shell Variables
      - They are contained exclusively within the shell in which they were set or defined.
      - Can be displayed with the `set` command or `env` command.
    
    #### Connfig Files:
      - User confirgurati file: `~/.bashrc` or `/.zshrc`.
      - System wide configuration file: `/etc/bash.bashrc` or `/etc/zsh/zshrc`
    
    #### The `PATH` Variable
      - The `PATH` variable is used to specify the search path for commands.
      - The `PATH` variable is set in the `~/.bashrc` or `~/.zshrc`
      - To see all PATHs use `echo $PATH`
      - To add a new PATH use `export PATH=PATH_TO_ADD:$PATH`
      - To remove a PATH use `export PATH=PATH_TO_REMOVE:$PATH`
      - Any shell scripts that are located in any of the directories that are listed in the `PATH` variable will be able to run by the name of the script without needing to specify the path such as `./script.sh` could become `script.sh` and executed without needing to specify the path.
    
    #### Postional Parameters
      - See the [PDF](./bash-shell-scripting/resources/positional-args.pdf) for more details.
    
    #### If, Elif, and Else Statements
      - To see all possible conditionals to use in an if/elif/else statement use `man test`.
      - Using `[[]]` in conditional statements allows for single quote string variables, however it's consideered good practice to include double quotes in the string.
        - `[[ -d "$1" ]]` -> Tests if `$1` is a directory
    
    #### Testing Integers
      - In scripts conditional statements can be used to test integers with a set of operators such as `==`, `!=`, `>=`, `>`, `<=`, `<` and their string equivalents like `-eq`, `ne`, `ge`, `gt`, `le`, `lt`.
    
    #### Command Substitution
      - To run a shell command and store it's output into variable for later use use `$(VAR_NAME)`.
    
    #### String Comparison in Conditionals
      - See the Bash script [bash_comparing_strings.sh](./bash-shell-scripting/resources/bash_comparing_strings.sh) for more details.
    
    
    #### Conditional Code Syntax:
      # if [ some_condition_is_true ]
      # then
      #   //execute this code
      # elif [ some_other_condition_is_true ]
      # then
      #   //execute_this_code
      # else
      #   //execute_this_code
      # fi
      ## Examples:
      ```sh
        i=1
        if [[ $i -lt 10 ]]
        then
          echo "i is less than 10."
        fi
        #################
        i=100
        if [[ $i -lt 10 ]]
        then
          echo "i is less than 10."
        else
          echo "i is greater than or equal to 10."
        fi
        ################
        i=10
        if [[ $i -lt 10 ]]
        then
          echo "i is less than 10."
        elif [[ $i -eq 10 ]]
        then
          echo "i is 10"
        else
          echo "i is greater than or equal to 10."
        fi
      ```
      ### TESTING CONDITIONS => man test ###
      ### For numbers (integers) ###
      # -eq   equal to
      # -ne   not equal to
      # -lt   less than
      # -le   less than or equal to
      # -gt   greater than
      # -ge   greater than or equal to
      
      # For files:
      # -s    file exists and is not empty
      # -f    file exists and is not a directory
      # -d    directory exists
      # -x    file is executable by the user
      # -w    file is writable by the user
      # -r    file is readable by the user
      
      # For Strings
      # =     the equality operator for strings if using single square brackets [ ]
      # ==    the equality operator for strings if using double square brackets [[ ]]
      # !=    the inequality operator for strings
      # -n $str   str is nonzero length
      # -z $str   str is zero length
      
      # &&  => the logical and operator
      # ||  => the logical or operator
    
    
    #### Local Variables In Functions
      - The `local` keyword is used to create local variables in a function.
      - It's a good practice to use `local` keyword when declaring variables in a function.
      - Functions have access to the global variables.
    
    ##### Menus in Bash. The Select Statement
      - See the script [bash_select_menus.sh](./bash-shell-scripting/resources/bash_select_menus.sh) for more details.
      - Commonly used in CLI applications.
    
    #### Bash Arrays
      - Bash arrays are used to store multiple values in a single variable.
      - To print the array use `echo ${array[@]}` or `echo ${array[*]}`.
      - To print the indices of the array use `echo ${!array[@]}` or `echo ${!array[*]}`.
      - To print the length of the array use `echo ${#array[@]}` or `echo ${#array[*]}`.
      - You can reference by index or by name `echo ${array[0]}` or `echo ${array[name]}`.
      - Negative indices can be used to reference from the end of the array `echo ${array[-1]}`.
      - To remove an element from the array use `unset array[index]`.
      - To remove all elements from the array use `unset array`.
      - To clear the array use `array=()`.
      - To copy an array use `array2=(${array1[@]})`.
      - To append an element to the array use `array+=("element")`.
      - To slice an array use `array2=(${array1[@]:index:length})`.
      - Associative arrays are indexed with string keys and used to store key/value pairs in a single variable.
      - To set an associative array use `declare -A array`.
      
      
      ##### The `readarray` Command:
        - The `readarray` command is used to read the contents `STDIN` or files and store them into an indexed array.
        - `readyarray account < <(cat ./users.txt)`
          - The `< < ( ... )` syntax is used to redirect the output of a command to the `readarray` command.
      
      ##### Iterating Over Arrays:
        - Iterate over an array using a for loop:
          - `for element in "${array[@]}"`
        - Iterate over an array using a while loop:
          - `while read -r element; do`