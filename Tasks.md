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
cat declaration.txt | tr [a-z] [A-Z]
```

Count the # of lines that contain the phrase “WE”:

```
cat declaration.txt | grep [wW]e | wc -l
```

grep (Global regular Expression Print) is probably the MOST powerful command in linux. It let’s you find patterns in files and streams. Above we take the output from displaying the file with the cat command and grep or search for the word “WE” using either capital or lowercase “w”.

Then we pipe that stream into wordcount to get the number of lines.

** Question 2: # of lines containing WE: _____________ **

Sort the lines (ignoring case –i) in the file (this doesn’t really make sense in this case):

```
cat declaration.txt | sort –i
```

Do the following:

```
mkdir sandbox
cd sandbox
cp ../declaration.txt .
```

Makes a new directory called sandbox then change into it. Then copy (cp) the \*.txt file into the new directory (the . at the end means current directory).

```
head -10 declaration.txt > part1.txt
tail -10 declaration.txt > part2.txt
```

Head looks at the –Nth number of lines at the beginning of a file, Tail the last –Nth elements (in this case 10 first and 10 last). The > redirects output to a new file, here part1.txt and part2.txt. Now let’s append some data to a file:

```
head -11 declaration.txt | tail -1 >> part1.txt
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
  echo "Usage: test.sh <filename> "
  echo "You did not supply a filename."
  exit 1
fi

fn=$1
numWords=`wc -w $fn | xargs | cut -d ' ' -f 1`

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

Escape (ESC) takes the file out of insert mode. Colon enters a command and wq means “Write Quit”, ie, save the file and exit.

Now, try to run the script. In linux you put a period (“./”) in front of the filename to run:

```
./test.sh declaration.txt
```

** Question 4: What message did you receive? **

You should have received a permission denied error. The reason here is that linux thinks this file is a read/write text file and NOT an executable.

```
ls –l test.sh
```

lists the file with the –l or LONG option:

```
-rw- r-- r-- 1 vagrant staff 233 Jul 8 15:14 test.sh
```

Read about file permissions here:

https://www.linux.com/learn/understanding-linux-file-permissions

So, let’s tell it that the file is executable:

```
chmod u+x test.sh
```

The chmod (Change mode) command says: change mode of User’s permissions (u) and add executable (+x) to file test.sh. Now when we do ls –l we get:

```
-rwxr-- r-- 1 vagrant staff 233 Jul 8 15:14 test.sh
```

Notice now that the user’s (vagrant) permission for this file now has an “X” for allow execution. Now try to execute:

```
./test.sh declaration.txt
```

** Question 5: What’s the answer? **

Let’s briefly go over the code in the shell script:

```
1 - #!/bin/bash
2 - if [[ $# -eq 0 ]]
3 - then
4 -   echo "Usage: test.sh <filename>"
5 -   echo "You did not supply a filename."
6 - exit 1
7 - fi
8 - fn=$1
9 - numWords=`wc -w $fn | xargs | cut -d ' ' -f 1`
10 - echo "Number of words in $fn is: $numWords"
11 - exit 0
```

Line 1 tells the OS that this is a bash shell script. (type echo $SHELL to see the shell you are using on any linux system)

Line 2 tests the # of arguments from the command line $# to see if it is equal to (-eq) 0. Meaning that the user did not enter a filename after the program name.

If the test is true then echo back to the user information on how to run the program (lines 4 and 5) then exit with a non zero exit code (line 6).

Line 7 ends the if/then statement. Notice that with bash shell it uses a backwards if (fi) to end the statement.

Line 8 assigns a variable *fn* to the 1st parameter ($1) passed to the program on the command line (ie, the filename)

Line 9 assigns the variable numWords a command output of wc. Notice that backticks (\`) are used to extrapolate a command. Here the command is pretty complex. Do a wordcount on the given file (wc –w) and pipe ( | ) to xargs which removes any leading/trailing blanks then pipe ( | ) to the cut command which delimits the output by space (-d ‘ ‘) and then returns only the first field (-f 1).

Line 10 prints out the number of words in the given file.

Finally, line 11 exits the program.

** EXERCISE 1: Write a shell script to output the first line of a given file as uppercase. **

1. Make a copy of the test.sh file:
  ```
  cp test.sh upperCaseMe.sh 
  ```
2. Use TextMate or another editor on Mac to edit the file
3. Using the head -1 and translate (tr [a-z] [A-Z]) commands together should help you figure it out. HINT: replace the code in between the backticks.
4. Since we copied the file there is no need to change permissions since they came with the original file.
5. Run the file against the declaration.txt file and save it to a file (./upperCaseMe.sh declaration.txt > line1.txt)
