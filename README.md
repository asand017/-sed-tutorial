#BASH TEXT MODIFIERS

##1. sed
##2. awk
##3. ed/red
##4. tr
##5. sort
##6. expand/unexpand
##7. replace

###1. sed
*sed* (standing for a {**s**}tream {**ed**}itor) is a quick and efficient way of changing the text inside of a file without having to go in and change things yourself (time you can better use working on the next assignment :wink:).

The usual format of the sed command is as follows:

<blockquote>
sed *OPTIONS*... [*SCRIPT*] [*INPUTFILE*...]
</blockquote>

* *OPTIONS* refers to a passed in flag (i.e. **-n** or **-i**)
* *SCRIPT* refers to a pattern that will be used to filter the infile text
* *INPUTFILE* refers to the filename of the file you want to modify.


