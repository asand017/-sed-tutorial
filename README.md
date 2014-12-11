#SED TEXT MODIFIER

Welcome to cs100! :smiley: :trollface: :fearful:

We will be learning about *sed* and the power it holds!

####What is *sed*?

*sed* (standing for a {**s**}tream {**ed**}itor) is a quick and efficient way of changing the text inside of a file without having to go in and change things yourself (time you can better use working on the next 100  assignment :wink:).

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

####So What Does it Look Like?
The format of the *sed* command is as follows:
<blockquote>
sed *OPTIONS* ... [ *SCRIPT* ] [ *INPUTFILE* ... ]
</blockquote>

* *OPTIONS* refers to a passed in flag (i.e. **-n** or **-i**)

* *SCRIPT* refers to a pattern that will be used to filter the infile text

* *INPUTFILE* refers to the filename of the file you want to modify

Practically, *sed* is somewhat flexible in how it can be called.

For example: 
<blockquote>
sed 's/cat/dog/' testfile
</blockquote> 

does the same thing as 
<blockquote>
sed s/cat/dog/ testfile
</blockquote>

which does the same thing as
<blockquote>
cat testfile | sed 's/cat/dog/'
</blockquote>

which does the same thing as 
<blockquote>
cat testfile | sed s/cat/dog/
</blockquote>

**NOTE:** *sed* requires some sort of input to function. This input can come from a pipe or 
it can be passed in as shown in the *sed* declaration. 

####When To Use it
The *sed* command is hilariously underused by most programmers for purposes outside of string 
substituion. With a little imagination, *sed* can have many more uses. For instance, *sed* can 
be used to emulate other commands such as *grep* and *head*. If someone wanted to write a 
a program that automatically edits a file, *sed* would be their best friend. Unfortuneatly for most
programmers, the simplicity of *sed* is overshadowed by its lengthy documentation.

The most widely used and most popular use of *sed* is **subsitution**.

#####Substitution
The bread and butter of *sed*, the **s** command (s for substitution) 

A simple example of *sed* substitution in action: 

<blockquote>
echo dog | sed 's/dog/cat/'
</blockquote>
