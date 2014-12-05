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
*sed* works by maintaining two data buffers: the active **pattern** and 
the auxiliary **hold** space. 
