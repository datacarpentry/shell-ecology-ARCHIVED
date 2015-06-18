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


Refer to the Software Carpentry material in 01-filedir.md, online at [http://software-carpentry.org/v5/novice/shell/01-filedir.html](Software Carpentry) for detailed descriptions of commands. 

The working directory is your working 'folder'. It groups together the files that you can see, and it is also the place where simple command will read or create files.

What is my current working directory (print working directory):

	$ pwd

Discuss the path and how that relates to the directory structure you see in the file browser on your computer. 

List contents of the working directory:

	$ ls				# shows all files

Introduce the concept of a command having one or more flags / parameters:

	$ ls -F
	$ ls -l -h
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

	$ cd ..         		# change the working directory 'one level up'
	$ cd            		# change to your home directory
	
Create and remove directories:

<pre>
	$ mkdir <em>directory</em>
	$ rmdir <em>directory</em>
</pre>


Make a directory for this course. Now, let us put some files in that directory. 

Introduce how to Copy, move, delete files:
	
	$ cp
	$ mv
	$ rm
	
Warn folks about rm - there is no Trash with bash. 



Copy, rename, move, delete:
	
<pre>	
	$ cp <em>origin</em> <em>destination</em>
	$ mv <em>origin</em> <em>destination</em>  # used for both renaming and moving
	$ rm <em>file</em>
	$ rm -r <em>directory</em>		# deletes complete directory tree
</pre>	

If  *destination* is not a directory, `mv` renames, and `cp` copies.
If *destination* is a directory, `mv` moves file *origin* into that directory, and `cp` makes a copy of file *origin* into that directory.

Warn folks about rm - there is no Trash with bash. 

*Hint: tab completion makes you more efficient and less error-prone*

Exercise: move the three .csv data files into a directory called 'data' in the directory for the course. Change to this directory.  

Create and edit a file:
	
	$ touch readme.txt
	$ nano readme.txt
	
Put some information about these files in a README.txt file and save. 

###Working with file contents

Seeing the contents of a file:

<pre>
	$ cat <em>file</em>
	$ less <em>file</em>  		# use 'q' to leave the viewer
</pre>	

For instance:

	$ cat species.csv
	$ cat plots.csv
	$ cat surveys.csv
	$ cat plots.csv species.csv

'cat' can get multiple arguments. This will append the contents of all the files after one another. This works well for the small files but not so well for the large file. How can we look at only the top of the file?

	$ less
	$ head
	$ tail

How big is this file?
	
<pre>
	$ ls -lh <em>file(s)</em>
	$ wc     <em>file(s)</em>		# count of lines, words and characters
</pre>

Using wildcards:

	$ ls *.csv
	$ wc -l *.csv

Redirecting output to a file using the '>' operator, e.g.:

	$ wc -l *.csv > number_lines.csv

Sorting the contents of a file:
	
<pre>
	$ sort <em>file</em>
</pre>

Pipe commands together using the `|` operator, e.g.:

	$ wc -l *.csv | sort
	
Getting subset of rows:

<pre>
	$ head  <em>file</em>        		# first 10 lines of a file
	$ tail  <em>file</em>        		# last 10 lines of a file
</pre>	


Exercise: get rows 100 through 200 using head, tail and pipe

Getting a subset of columns (in this case, the year, which is the 4th column of a file called surveys.csv):
	
	$ cut -f 4 -d , surveys.csv
	
Talk about how to get help on commands from man pages; show where to find this information in the web browser (because git bash does not have man). 

	$ cut -f 4 -d , surveys.csv | sort 
	$ cut -f 4 -d , surveys.csv | sort -r 

How many different genders are there?

	$ cut -f 7 -d , surveys.csv | uniq

Did that work? Why not and how could we fix it? (cut | sort | uniq)

## Searching

### In files:

Finding specific text in files using grep:

	$ grep 2000 surveys.csv
	$ grep -w 2000 surveys.csv

Exercise: get all rows with species="DM" and put these in a new file. How many are there?

Bonus: How would we put a header row on this new file?

	$ head -n 1 > header.csv
	$ cat header.csv file.csv > newfile.csv

### Finding files

	$ find ~ -name "*.csv" -print
	
This will start in '~' (your home directory) and traverses the whole directory tree searching for a file with this particular name. Look at man page for find and see how many different ways we can search. 


### Advanced demo

As a final demo, show something more complicated. Where are the python scripts where I used the csv library?

	$ grep -w 'import csv' $(find ~/Documents -name "*.py" -print)

If you have time, unpack this:
You are storing this output: 
	$ find ./ -name "*.py"
in a variable.  Try storing what is in the $() as a named variable:

	$ PYFILES=$(find ./ -name "*.py")

print it to the screen:
	$ echo $PYFILE
	
Now use this in the grep command:

	$ grep -w 'import csv' $PYFILE

This is the same as:

	$ grep -w 'import csv' $(find ./ -name "*.py")

## What did I do? 

To walk through the history of commands you issued, use the arrow-up key. Alternatively, type
	
	$ history
	$ history > my_swc_history.txt
