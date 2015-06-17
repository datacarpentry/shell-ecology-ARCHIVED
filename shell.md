#Introduction to the shell

Based on the very detailed material at [http://software-carpentry.org/v5/novice/shell/index.html](http://software-carpentry.org/v5/novice/shell/index.html).

Assume that students have a set of three data files (plots.csv, surveys.csv and species.csv) from the  et al publication, either from a github repo or from some other mechanism. 

##Objectives

* Understand the advantages of text files over other file types
* Introduce the concept of command-line interface
* Explain how to navigate your computer's directory structures and understand paths
* Bash commands: using flags, finding documentation
* Move, copy and delete files
* Using tab completion for efficiency
* Use of wildcards for pattern matching

## Text files
Let's start by opening Word (other other word processing software such as Libre Office or Open Office). Type some text:

	$ This is not a text file

Save in native format (that might be text.doc, text.docx, text.odt, depending on your word processor). Then, also Save As a text document (text.txt)

Now, open these two files in our text editor - Notepadd++ on Windows or Text Wrangler on Mac. Discuss the simplicity of the text document and the complexity of the non-text document. All of the tools we will use over the next few days can operate on text files. Using text makes it easier to read, manipulate, analyze and share your data. In 20 years, we will still be able to read text files. No such guarantee about Office docs or other proprietary format. 

##Using the shell

The shell is an example of a command-line interface (CLI). See the material in 00-intro.md, online at [http://software-carpentry.org/v5/novice/shell/00-intro.html](Software Carpentry) for details on introducing the shell.  

### Finding help
<pre>	
	$ type <em>command</em>		# what does command refer to
	$ man <em>command</em>		# manual page for command
</pre>

### Listing, navigating, creating and moving things

The working directory is your working 'folder'. It groups together the files that you can see, and it is also the place where simple command will read or create files.

Printing working directory:

	$ pwd

List contents of the working directory:

	$ ls				# show all files

Introduce the concept of a command having one or more flags / parameters:

	$ ls -F
	$ ls -lh

The -F flag is useful when you do not have colours set on your shell to help distinguish files from directories. This will be true for most participants, while most instructors probably have colours. 

Note that spaces are important. ls-F and ls - F do not work. 

	$ ls -l				# show details
	$ ls *.txt     			# just files matching pattern *.txt
	
Change directories:
<pre>	
	$ cd  <em>directory</em>		# change to that directory
</pre>

If *directory* start with a '/'; it is an *absolute* path, meaning the location is specified starting at the top of the entire file system (*note: in Linux and Mac OS X there are no drive letters like in Windows!*). If *directory* does not start with a '/' the location is relative to the current directory. The special directory name `..` means 'one level up'. 

	$ cd ..         		# change 'one level up'
	$ cd            		# change to your home directory
	
Create and remove directories:

<pre>
	$ mkdir <em>directory</em>
	$ rmdir <em>directory</em>
</pre>

Copy, rename, move, delete:
	
<pre>	
	$ cp <em>origin</em> <em>destination</em>
	$ mv <em>origin</em> <em>destination</em>  # used for both renaming and moving
	$ rm <em>file</em>
	$ rm -r <em>directory</em>		# deletes complete directory tree
</pre>	
If  *destination* is not a directory, `mv` renames, and `cp` copies.
If *destination* is a directory, `mv` moves file *origin* into that directory, and `cp` makes a copy of file *origin* into that directory.

*Hint: tab completion makes you more efficient and less error-prone*

###Working with file contents

Seeing the contents of a file:

<pre>
	$ cat <em>file</em>
	$ less <em>file</em>  		# use 'q' to leave the viewer
</pre>	

Create and/or edit a file:
	
	$ nano <em>file</em>

How big is this file?
	
<pre>
	$ ls -lh <em>file(s)</em>
	$ wc     <em>file(s)</em>		# count of lines, words and characters
</pre>

Sorting the contents of a file:
	
<pre>
	$ sort <em>file</em>
</pre>

Redirecting output to a file: use the '>' operator, e.g.:

	$ wc -l *.csv > number_lines.csv
	
Pipe commands together using the `|` operator, e.g.:

	$ wc -l *.csv | sort
	
Getting subset of rows:

<pre>
	$ head  <em>file</em>        		# first 10 lines of a file
	$ tail  <em>file</em>        		# last 10 lines of a file
</pre>	

Getting a subset of columns (in this case, 3rd column of a file called inputfile.csv):
	
	$ cut -f 3 -d , inputfile.csv
	
## Finding things

In files and in directories:
<pre>
	$ grep <em>regexp</em> <em>file(s)</em>		# search pattern in files
	$ find. -name 'pattern'		# search file matching pattern in current dir and below
</pre>		

## What did I do? 

Use the arrow-up key, or:
	
	$ history
