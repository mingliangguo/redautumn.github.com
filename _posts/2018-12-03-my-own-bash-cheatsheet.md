---
title: "My own bash cheatsheet"
layout: single
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
date: 2018-12-03 16:47:03 EST
---

## Check the real command of an alias

```bash
type aliased-command
```

## Check if a command exists or not

```bash
command -v kubectl >/dev/null 2>&1
```

[Here](https://unix.stackexchange.com/questions/163352/what-does-dev-null-21-mean-in-this-article-of-crontab-basics) is a very helpful explanation about the usage of redirecting to `/dev/null` and what `2>&1` means:

- `/dev/null` is a black hole where any data sent, will be discarded
- `2` is the file descriptor for Standard Error
- `&` is the symbol for file descriptor (without it, the following `1` would be considered a filename)
- `1` is the file descriptor for Standard Out

Therefore `>/dev/null 2>&1` is redirect the output of your program to `/dev/null`. Include both the Standard Error and Standard Out.

To find the return code of the last executed comamnd is `$?`, so you can check if the value of `$?` equals to `0` to verify if the previous command succeeds or not.

More detail information can be found at The Linux Documentation Project's [I/O Redirection](http://www.tldp.org/LDP/abs/html/io-redirection.html) page.

# Define variables in bash

```bash
array[0]=valA                # how to define an array
array[1]=valB
array[2]=valC
array=([2]=valC [0]=valA [1]=valB)  # another way
array=(valA valB valC)              # and another

${array[i]}                  # displays array's value for this index. If no index is supplied, array element 0 is assumed
${#array[i]}                 # to find out the length of any element in the array
${#array[@]}                 # to find out how many values there are in the array

declare -a                   # the variables are treaded as arrays
declare -f                   # uses function names only
declare -F                   # displays function names without definitions
declare -i                   # the variables are treaded as integers
declare -r                   # makes the variables read-only
declare -x                   # marks the variables for export via the environment

${varname:-word}             # if varname exists and isn't null, return its value; otherwise return word
${varname:=word}             # if varname exists and isn't null, return its value; otherwise set it word and then return its value
${varname:?message}          # if varname exists and isn't null, return its value; otherwise print varname, followed by message and abort the current command or script
${varname:+word}             # if varname exists and isn't null, return word; otherwise return null
${varname:offset:length}     # performs substring expansion. It returns the substring of $varname starting at offset and up to length characters

${variable#pattern}          # if the pattern matches the beginning of the variable's value, delete the shortest part that matches and return the rest
${variable##pattern}         # if the pattern matches the beginning of the variable's value, delete the longest part that matches and return the rest
${variable%pattern}          # if the pattern matches the end of the variable's value, delete the shortest part that matches and return the rest
${variable%%pattern}         # if the pattern matches the end of the variable's value, delete the longest part that matches and return the rest
${variable/pattern/string}   # the longest match to pattern in variable is replaced by string. Only the first match is replaced
${variable//pattern/string}  # the longest match to pattern in variable is replaced by string. All matches are replaced

${#varname}                  # returns the length of the value of the variable as a character string

*(patternlist)               # matches zero or more occurrences of the given patterns
+(patternlist)               # matches one or more occurrences of the given patterns
?(patternlist)               # matches zero or one occurrence of the given patterns
@(patternlist)               # matches exactly one of the given patterns
!(patternlist)               # matches anything except one of the given patterns

$(UNIX command)              # command substitution: runs the command and returns standard output

```

> credit belongs to [awesome cheatsheets](https://github.com/LeCoupa/awesome-cheatsheets/blob/master/languages/bash.sh)


## Loop through arrays

```bash
declare -a fruits=("apple" "orange" "banana")

for fruit in "${fruits[@]}";
do
    echo "$fruit"
done
```

## Basic if condition check

### check if the line only contains 1 single character (e.g. line ending)

```bash
    if [ ${#line} -eq 1 ]; then
        continue
    else
        echo ${line}
    fi
```

### Use regex to check if a string starts with "#"

```bash
if [[ "$var" =~ ^#.*  ]]; then
    echo "yes"
fi
```

### Read a file and print lines not start with “#”

```bash
#!/bin/bash
input="/path/to/txt/file"
while IFS= read -r var
do
  #
  # if value of $var starts with #, ignore it
  #
  [[ $var =~ ^#.* ]] && continue
  echo "$var"
done < "$input"
```

### Find which process listens to a port

On Linux(ubuntu/fedora)

```bash
# sudo apt install net-tools
netstat -ltnp |grep $PORT
```

On Mac (or other linux system)

```bash
# sudo apt-get install lsof
# sudo yum install losf
lsof  -t -i :6379
```

### Kill all process which match with a certain name

e.g. kill all redis-server process

```bash
for pid in `pgrep -f redis-server`;do kill $pid; done
```

### Enable sudo without password

Edit `/etc/sudoers` file and add a line as below for the user you want to allow nopassword sudo.



```bash
sudo cp /etc/sudoers ~/sudoers.bak
sudo visudo
# Add the following line to the sudoers file
user_name ALL=(ALL) NOPASSWD:ALL
```

# References

- [Bash check if string starts with character such as #](https://www.cyberciti.biz/faq/bash-check-if-string-starts-with-character-such-as/)
- [Sudo without password](https://linuxhandbook.com/sudo-without-password/)

