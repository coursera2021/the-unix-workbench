# Working with Unix

## Self-Help

Each of the commands that we've discussed so far are thoroughly documented, and
you can view their documentation using the `man` command, where the first
argument to `man` is the command you're curious about. Let's take a look at the
documentation for `ls`:


```bash
man ls
```

```
LS(1)                     BSD General Commands Manual                    LS(1)

NAME
     ls -- list directory contents

SYNOPSIS
     ls [-ABCFGHLOPRSTUW@abcdefghiklmnopqrstuwx1] [file ...]

DESCRIPTION
     For each operand that names a file of a type other than directory, ls
     displays its name as well as any requested, associated information.  For
:
```

The controls for navigating `man` pages are the same as they are for `less`.
I often use `man` pages for quickly seraching for an option that I've forgotten.
Let's say that I forgot how to get `ls` to print a long list. After typing
`man ls` to open the page, type `/` in order to start a search. Then type the
word or phrase that you're searching for, in this case type in `long list` and
then press `Enter`. The page jumps to this entry:

```
     -l      (The lowercase letter ``ell''.)  List in long format.  (See below.)
             If the output is to a terminal, a total sum for all the file sizes is
             output on a line before the long listing.
```

Press the `n` key in order to search for the next occurrence of the word, and if
you want to go the previous occurrence type `Shift` + `n`. This method of
searching also works with `less`. When you're finished looking at a `man` page
type `q` to get back to the prompt.

The `man` command works wonderfully when you know which command you want to look
up, but what if you've forgotten the name of the command you're looking for? You
can use `apropos` to search all of the available commands and their
descriptions. For example let's pretend that I forgot the name of my favorite
command line text editor. You could type `apropos editor` into the command line
which will print a list of results:


```bash
apropos editor
```

```
## ed(1), red(1)            - text editor
## nano(1)                  - Nano's ANOther editor, an enhanced free Pico clone
## sed(1)                   - stream editor
## vim(1)                   - Vi IMproved, a programmers text editor
```

The second result is `nano` which was just on the tip of my tongue! Both `man`
and `apropos` are useful when a search is only a few keystrokes away, but if 
you're looking for detailed examples and explanations you're better off using 
a search engine if you have access to a web browser.

### Summary

- Use `man` to look up the documentation for a command.
- If you can't think of the name of a command use `apropos` to search for a word
associated with that command.
- If you have access to a web browser, using a search engine might be better
than `man` or `apropos`.

### Exercises

1. Use `man` to look up the flag for human-readable output from `ls`.
2. Get help with `man` by typing `man man` into the console.
3. Wouldn't it be nice if there was a calendar command? Use `apropos` to look
for such a command, then use `man` to read about how that command works.

## Get Wild

Let's go into my `Photos` folder in my home directory and take a look around:


```bash
pwd
```

```
/Users/sean
```


```bash
ls
```

```
Code
Documents
Photos
Desktop
Music
todo-2017-01-24.txt
```


```bash
cd Photos
ls
```

```
2016-06-20-datasci01.png
2016-06-20-datasci02.png
2016-06-20-datasci03.png
2016-06-21-lab01.jpg
2016-06-21-lab02.jpg
2017-01-02-hiking01.jpg
2017-01-02-hiking02.jpg
2017-02-10-hiking01.jpg
2017-02-10-hiking02.jpg
```

I've just been dumping pictures and figures into this folder without organizing
them at all! Thankfully (in the words of Dr. Jenny Bryan) [I have an unwavering 
commitment to the ISO 8601 date
standard](https://twitter.com/JennyBryan/status/816143967695687684) so at least
I know when these photos were taken. Instead of using `mv` to move around each
individual photo I can select groups of photos using the `*` wildcard. A 
**wildcard** is a character that represents other characters, much like how
joker in a deck of cards can represent other cards in the deck. Wildcards are
a subset of metacharacters, a topic which we will discuss in detail later on in
this chpater. The `*` ("star") wildcard represents *zero or more of any
character*, and it can be used to match names of files and folders in the command
line. For example if I wanted list all of the files in my Photos directory which
have a name that starts with "2017" I could do the following:


```bash
ls 2017*
```

```
2017-01-02-hiking01.jpg
2017-01-02-hiking02.jpg
2017-02-10-hiking01.jpg
2017-02-10-hiking02.jpg
```

Only the files starting with "2017" are listed! The command `ls 2017*` literally
means: list the files that start with "2017" followed by zero or more of any
character. As you can imagine using wildcards
is a powerful tool for working with groups of files that are similarly named.

Let's walk through a few other examples of using the star wildcard. We could
only list the photos starting with "2016":


```bash
ls 2016*
```

```
2016-06-20-datasci01.png
2016-06-20-datasci02.png
2016-06-20-datasci03.png
2016-06-21-lab01.jpg
2016-06-21-lab02.jpg
```

We could list only the files with names ending in `.jpg`:


```bash
ls *.jpg
```

```
2016-06-21-lab01.jpg
2016-06-21-lab02.jpg
2017-01-02-hiking01.jpg
2017-01-02-hiking02.jpg
2017-02-10-hiking01.jpg
2017-02-10-hiking02.jpg
```

In the case above the file name can start with a sequence of zero or more of 
any character, but the file name must end in `.jpg`.
Or we could also list only the first photos from each set of photos:


```bash
ls *01.*
```

```
2016-06-20-datasci01.png
2016-06-21-lab01.jpg
2017-01-02-hiking01.jpg
2017-02-10-hiking01.jpg
```

All of the files above have names that are composed a sequence of characters,
followed by the adjacent characters `01.`, followed by another sequence of
characters.
Notice that if I had entered `ls *01*` into the console every file would have
been listed since `01` is a part of all of the file names in my Photos
directory.

Let's organize these photos by year. First let's create one directory for
each year of photos:


```bash
mkdir 2016
mkdir 2017
```

Now we can move the photos using wildcards:


```bash
mv 2017-* 2017/
ls
```

```
2016
2016-06-20-datasci01.png
2016-06-20-datasci02.png
2016-06-20-datasci03.png
2016-06-21-lab01.jpg
2016-06-21-lab02.jpg
2017
```

Notice that I've moved all files that start with "2017-" into the 2017 folder!
Now let's do the same thing for files with names starting with "2016-":


```bash
mv 2016-* 2016/
ls
```

```
2016
2017
```

Finally my photos are somewhat organizaed! Let's list the file in each directory
just to make sure all was moved as planned:


```bash
ls 2016/
```

```
2016-06-20-datasci01.png
2016-06-20-datasci02.png
2016-06-20-datasci03.png
2016-06-21-lab01.jpg
2016-06-21-lab02.jpg
```


```bash
ls 2017/
```

```
2017-01-02-hiking01.jpg
2017-01-02-hiking02.jpg
2017-02-10-hiking01.jpg
2017-02-10-hiking02.jpg
```

Looks good! There are a few more wildcards beyond the star wildcard which we'll
discuss in the next section where searching file names gets a little more
advanced.

### Summary

- Wildcards can represent many kinds and numbers of characters.
- The star wildcard (`*`) represents zero or more of any character.
- You can use wildcards on the command line in order to work with multiple files
and folders.

### Exercises

1. Before I organized the photos by year, what command would have listed all of
the photos of type `.png`?
2. Before I organized the photos by year, what command would have deleted all of
my hiking photos?
3. What series of commands would you use in order to put my figures for a data
science course and the pictures I took in the lab into their own folders?

## Search

The ability to search through files and folders can greatly improve your
productivity using Unix. First we'll cover searching through text files.
I recently downloaded a list of the names of the states in the US. Let's take a
look at this file:


```bash
cd ~/Documents
ls
```

```
a-tale-of-two-cities.txt
canada.txt
states.txt
```


```bash
wc states.txt
```

```
50      60     472 states.txt
```

Makes sense that there are 50 lines, but it's interesting that there are 60
total words. Let's a take a peak at the beginning fo the file:


```bash
head states.txt
```

```
Alabama
Alaska
Arizona
Arkansas
California
Colorado
Connecticut
Delaware
Florida
Georgia
```

This file looks basically how you would expect it to look! You may recall from
chapter 3 that the kind of shell that we're using is the bash shell. Bash
treats different kinds of data differently, and we'll dive deeper into data
types in chapter 5. For now all you need to know is that text data are
called **strings**. A string could be a word, a sentence, a book, or a file or 
folder name. One of the most effective ways to search through strings is to use
**regular expressions**. Regular expressions are strings that define patterns
in other strings. You can use regular expressions to search for a sub-string
contained within a larger string, or to replace one part of a string with
another string.

One of the most popular tools for searching through text files is `grep`.

-n line number
-x exact
-i ignore case
-v invert match






## Make

## Control

- chmod

## Configure

- .bash_profile, .bash_history, alias, PATH and other env vars

## Differentiate

- diff, md5, sha1

## Connect

- pipes, input redirection