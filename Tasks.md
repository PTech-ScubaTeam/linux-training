### Linux Tasks

Try the following on your Mac (Open Terminal). Remember linux is CASE SENSITIVE so you need to be exact.

```
cd ~/Documents
ls *.txt
```

First changes directories to your home directory’s Documents folder. The *ls* command will list all of the files with a \*.txt extension in the current directory. You should see the Declaration of Independence text file you downloaded earlier.

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
cat declaration-of- independence.txt | tr [a-z] [A-Z]
```

Count the # of lines that contain the phrase “WE”:

```
cat declaration-of- independence.txt | grep [wW]e | wc -l
```

grep (Global regular Expression Print) is probably the MOST powerful command in linux. It let’s you find patterns in files and streams. Above we take the output from displaying the file with the cat command and grep or search for the word “WE” using either capital or lowercase “w”.

Then we pipe that stream into wordcount to get the number of lines.

** Question 2: # of lines containing WE: _____________ **

Sort the lines (ignoring case –i) in the file (this doesn’t really make sense in this case):

```
cat declaration-of- independence.txt | sort –i
```

Do the following:

```
mkdir sandbox
cd sandbox
cp ../declaration-of- independence.txt .
```

Makes a new directory called sandbox then change into it. Then copy (cp) the \*.txt file into the new directory (the . at the end means current directory).

```
head -10 declaration-of- independence.txt > part1.txt
tail -10 declaration-of- independence.txt > part2.txt
```

Head looks at the –Nth number of lines at the beginning of a file, Tail the last –Nth elements (in this case 10 first and 10 last). The > redirects output to a new file, here part1.txt and part2.txt. Now let’s append some data to a file:

```
head -11 declaration-of- independence.txt | tail -1 >> part1.txt
```

The >> operator will append contents to a file.

** Question 3: What do you now expect to see in the part1.txt file? **