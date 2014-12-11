#SED TEXT MODIFIERS

Welcome to cs100! :smiley: :trollface: :fearful:

We will be learning about *sed* and the power it holds!

###sed
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

####So what does it look like?

The format of the *sed* command is as follows:
<blockquote>
sed *OPTIONS* ... [ *SCRIPT* ] [ *INPUTFILE* ... ]
</blockquote>

* *OPTIONS* refers to a passed in flag (i.e. **-n** or **-i**)

* *SCRIPT* refers to a pattern that will be used to filter the infile text

* *INPUTFILE* refers to the filename of the file you want to modify

The typical appearence of a *sed* command

####When to use *sed*
The *sed* command is hilariously underused by most programmers at its full potential. 

However, this does not mean any one programmer should refrain from using the simpler aspects 
of *sed*.

The most popular use of the *sed* command is for **subsitution**.

#####substitution
While *sed* has more commands than substitution, the average programmer will only ever use the substitution command: *s*.

A simple example of *sed* substitution in action: 

<blockquote>
echo dog | sed 's/dog/cat/'
</blockquote>
**NOTE:** Unlike in previous declaration of *sed*, *sed* can have input piped to it instead of an input file.




