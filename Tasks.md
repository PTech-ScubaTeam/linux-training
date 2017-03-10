### Linux Tasks

We'll use vagrant here to play with linux.  Issue the following command in the directory where your Vagrantfile is located:

```
vagrant up
```

after a minute when Vagrant is done downloading the appropriate box you can issue:

```
vagrant ssh
```

You are now in the shell of our virtual machine.  To prove it:
```
uname -a
```

You should see:  *Linux vagrant-ubuntu-trusty-64 3.13.0-110-generic \#157-Ubuntu SMP Mon Feb 20 11:54:05 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux*


Now lets change to our mounted host directory mapped to /vagrant:

```
cd /vagrant
ls *.txt
```

This changes directories to your home OS's mapped folder. The *ls* command will list all of the files with a \*.txt extension in the current directory. You should see the Declaration of Independence text file you downloaded earlier.

```
ls –l *.txt
```

This will list the LONG format (-l switch) of the directory which lists owners and permissions of files/directories.

Now try some linux commands against the file:

```
wc declaration-of- independence.txt
```

TIP: type in part of a filename like “dec” and then hit the TAB key. Shell should automatically complete to declaration-of- independence.txt *wc* stands for Word Count. By itself it lists the lines, words and characters in a file.

** Question 1: For this file, type the # ______ lines, # _____ words, #________ characters **

Now, let’s echo the file to caps using pipes and translations:

```
cat declaration-of-independence.txt | tr [a-z] [A-Z]
```

Count the # of lines that contain the phrase “WE”:

```
cat declaration-of-independence.txt | grep [wW]e | wc -l
```

grep (Global regular Expression Print) is probably the MOST powerful command in linux. It let’s you find patterns in files and streams. Above we take the output from displaying the file with the cat command and grep or search for the word “WE” using either capital or lowercase “w”.

Then we pipe that stream into wordcount to get the number of lines.

** Question 2: # of lines containing WE: _____________ **

Sort the lines (ignoring case –i) in the file (this doesn’t really make sense in this case):

```
cat declaration-of-independence.txt | sort –i
```

Do the following:

```
mkdir sandbox
cd sandbox
cp ../declaration-of-independence.txt .
```

Makes a new directory called sandbox then change into it. Then copy (cp) the \*.txt file into the new directory (the . at the end means current directory).

```
head -10 declaration-of-independence.txt > part1.txt
tail -10 declaration-of-independence.txt > part2.txt
```

Head looks at the –Nth number of lines at the beginning of a file, Tail the last –Nth elements (in this case 10 first and 10 last). The > redirects output to a new file, here part1.txt and part2.txt. Now let’s append some data to a file:

```
head -11 declaration-of-independence.txt | tail -1 >> part1.txt
```

The >> operator will append contents to a file.

** Question 3: What do you now expect to see in the part1.txt file? **

Rename our files using the move command (mv):

```
mv part1.txt part-one.txt
mv part2.txt part-two.txt
```

ls to confirm they have been renamed. Try a few grep expressions now:

```
ls | grep *.txt
ls | grep part*
```

### SHELL SCRIPTING

Let’s create a (bash shell) script to print out the # of words in a file.  Copy this code to your clipboard:

```
#!/bin/bash

if [[ $# -eq 0 ]]
then
  echo "Usage: test.sh < filename > "
  echo "You did not supply a filename."
  exit 1
fi

fn=$1
numWords=`wc -w $fn | xargs | cut -d &#39; &#39; -f 1`

echo "Number of words in $fn is: $numWords"

exit 0
```

Then at the $ prompt:

```
touch test.sh
vi test.sh
```

*touch* creates an empty file and vi is the simple editor that comes with linux (or VIM in the case of Mac).

Next, put the file into insert mode by hitting the lowercase “I” on your
keyboard. And paste in the code from your clipboard. Then to save, hit the following keystrokes:

```
ESC
:wq
ENTER
```
