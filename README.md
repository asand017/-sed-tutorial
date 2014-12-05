#BASH TEXT MODIFIERS

Welcome to cs100! :smiley: :trollface: :fearful:

We will be learning about text-modifying bash commands!

##1. sed
##2. awk
##3. ed/red
##4. tr
##5. sort
##6. expand/unexpand
##7. replace

###1. sed
*sed* (standing for a {**s**}tream {**ed**}itor) is a quick and efficient way of changing the text inside of a file without having to go in and change things yourself (time you can better use working on the next 100  assignment :wink:).

The usual format of the sed command is as follows:

<blockquote>
sed *OPTIONS* ... [ *SCRIPT* ] [ *INPUTFILE* ...]
</blockquote>

* *OPTIONS* refers to a passed in flag (i.e. **-n** or **-i**)
* *SCRIPT* refers to a pattern that will be used to filter the infile text
* *INPUTFILE* refers to the filename of the file you want to modify

**NOTE:** unless options **-e** or **-f** are selected (options that
specify a predetermined script to be used), *sed* will expect a 
script to be the first non-option parameter. 


<blockquote>
sed -e G test > result 
</blockquote> 
Because option/tag **-e** is passed in, we do not need to declare 
another script. (This particular line double-spaces each line of the 
"test" file and copies the result into the "result" file. The "test" file
is unchanged).


Alternatively
<blockquote>
sed 's/test/example/' test > result
</blockquote>
Because no flag was option/tag is passed in, we must specify our own
script to filter the passed in file. (This line replaces each occurence of 
the string *test* in the "test" file with the string *example* and copies
the result into the "result" file. The "test" file remains unchanged.)

####What is Going on Inside?
*sed* works by maintaining two data buffers: the active **pattern**
space and the auxiliary **hold** space. Both of these begin empty.

*sed* operates by going line by line of the input file and placing it into 
the **pattern** space, after removing any leading newline characters. 
Once the text is in the pattern space, the desired commands are executed.
A command will only execute if the text in the pattern space qualifies for
the command. When the end of the infile text is reached, the pattern space
is output to the output stream, replacing the previously removed newline.
Another cycle begins for the next line of text in the file.

The **pattern** space is deleted between any two cycles; however, the 
**hold** space maintains its data throughout the process.

####Available Options for *sed*
OPTIONS | DESCRIPTION
--------|------------
-n, --quiet, --silent | suppress automatic printing of pattern space
-e script, --expression=script | add the script to the commands to be executed
-f script-file, --file=script-file | add the contents of script-file to the commands to be executed
-i[SUFFIX], --in-place[=SUFFIX] | edit files in place (make backup if extension supplied)
-c, --copy | use copy instead of rename when shuffling files in -i mode (avoids change of input file ownership)
-l N, --line-length=N | specify the desired line-wrap length for the 'l' command
--posix | disable all GNU expressions
-r, --regexp-extended | use extended regular expressions in the script
-s, --separate | consider files as separate rather than as a single continous long stream
-u, --unbuffered | long minimal amounts of data from the input files and flush the output buffers more often
--help | display this help and exit
--version | output version information and exit

