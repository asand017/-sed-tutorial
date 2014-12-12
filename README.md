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
```
sed options ... [ script ] [ inputfile ... ]
```

* *options* refers to a passed in flag (i.e. **-n** or **-i**)

* *script* refers to a pattern that will be used to filter the infile text

* *inputfile* refers to the filename of the file you want to modify

Practically, *sed* is somewhat flexible in how it can be called.

For example: 
```
sed 's/cat/dog/' testfile
```

does the same thing as 
<blockquote>
sed s/cat/dog/ testfile
</blockquote>

which does the same thing as
```
cat testfile | sed 's/cat/dog/'
```

which does the same thing as 
```
cat testfile | sed s/cat/dog/
```

which replaces the first occurence of "cat" on each line of the input source with "dog".

**NOTE:** *sed* requires some sort of input to function. This input can come from a pipe or 
it can be passed in as shown in the *sed* declaration. 

Alternativly, you can call sed without input
```
sed 's/cat/dog/'
```

which will cause *sed* to wait for input from stdin and modify the input that matches the
desired pattern.




####What Can We Do With it?
The *sed* command is hilariously underused by most programmers for purposes outside of string 
substituion. With a little imagination, *sed* can have many more uses. For instance, *sed* can 
be used to emulate other commands such as *grep* and *head*. If someone wanted to write a 
a program that automatically edits a file, *sed* would be their best friend. Unfortuneatly for most
programmers, the simplicity of *sed* is overshadowed by its lengthy documentation.

The most widely used and most popular use of *sed* is **subsitution**.

#####Substitution
The bread and butter of *sed*, the **s** command (s for substitution) 

A simple example of *sed* substitution in action: 

```
echo dog | sed 's/dog/cat/'
```

There are four parts to the substitution command:

1. "s" &#8594; Substitute

2. "/.../.../" &#8594; Delimiter

3. "dog" &#8594; Regular Expression Pattern/Search Pattern

4. "cat" &#8594; Replacement String

**1.** The command character (in this case **s** for substitution) must go on the left side of the first
delimiter.

**2.** The character after **s** is called a delimiter. The delimiters are needed to parse the
command, to seperate the substitution command from the search pattern and seperate the replacement string from
previous part. In the case of the above example, the delimiter is a slash, but the delimiter can 
be any character you want as long as there are three of them:

```
echo dog | sed 's_dog_cat_'    
```

is equivalent to

```
echo dog | sed 's^dog^cat:'
```

is equivalent to

```
echo dog | sed 'sxdogxcatx'
```

and so forth.

Each of these instances will have the same output as the original example.

A missing delimiter while result in a "Unterminated 's' command" error.

**3.** The string you want to search for (i.e. "dog" the search pattern) is on the left side of the delimiter sequence. 

**4.** The string you want to replace the search pattern with (i.e. "cat") goes on the right side.

Now let&#39;s look at a real world example of substitution. 
