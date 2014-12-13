#SED TEXT MODIFIER

Welcome to cs100! :smiley: :trollface: :fearful:

###1. [link](#What is *sed*?)

###2. How Does it Work?

###3. What Does it Look Like?

###4. What Can We Do With it?

###5. Why Should We Ever Use it?

We will be learning about the `sed` bash command and the power it holds!

### <a name="What is *sed*?"></a>

`sed` (standing for a {**s**}tream {**ed**}itor) is a quick and efficient way of changing the text inside of a file without having to go in and change things yourself.

###How Does it Work?
`sed` works by maintaining two data buffers: the active **pattern**
space and the auxiliary **hold** space. Both of these begin empty.

`sed` operates by going line by line of an input file and placing it into 
the **pattern** space, after removing any leading newline characters. 
Once the text is in the pattern space, the desired commands are executed.
A command will only execute if the text in the pattern space qualifies for
the command. When the end of the infile text is reached, the pattern space
is output to the output stream, replacing the previously removed newline.
Another cycle begins for the next line of text in the file.

The **pattern** space is deleted between any two cycles; however, the 
**hold** space maintains its data throughout the process.

###What Does it Look Like?
The format of the `sed` command is as follows:
```
sed options ... [ script ] [ inputfile ... ]
```

* *options* refers to a passed in flag (i.e. **-n** or **-i**)

* *script* refers to a pattern that will be used to filter the infile text

* *inputfile* refers to the filename of the file you want to modify

In practice, `sed` is not completely strict in how it can be called.

For example: 
```
sed 's/aol.com/gmail.com/' testfile
```

does the same thing as 
```
sed s/aol.com/gmail.com/ testfile
```

which does the same thing as
```
cat testfile | sed 's/aol.com/gmail.com/'
```

which does the same thing as 
```
cat testfile | sed s/aol.com/gmail.com/
```

which replaces the first occurence of "aol.com" on each line of the input source with "gmail.com".

**NOTE:** `sed` requires some sort of input to pass over. This input can come from a pipe or 
it can be passed in as shown in the `sed` declaration. 

Alternativly, you can call sed without input
```
sed 's/aol.com/gmail.com/'
```

which will cause `sed` to wait for input from stdin and modify the input that matches the
desired pattern.

###What Can We Do With it?
The `sed` command is hilariously underused by most programmers for purposes outside of string 
substituion. With a little imagination, `sed` can have many more uses. For instance, `sed` can 
be used to emulate other commands such as *grep* and *head*. If someone wanted to write a 
a program that automatically edits a file, `sed` would be their best friend. Unfortuneatly for most
programmers, the simplicity of *sed* is overshadowed by its lengthy documentation.

####1. Substitution
####2. Emulate Other Commands

The most widely used and most popular use of `sed` is **subsitution**.

#####Substitution
The bread and butter of `sed`, the **s** command (s for substitution) 

A simple example of `sed` substitution in action: 

```
echo aol.com | sed 's/aol.com/gmail.com/'
```

There are four parts to the substitution command:

1. **s** &#8594; Substitute

2. **/.../.../** &#8594; Delimiter

3. **aol.com** &#8594; Regular Expression Pattern/Search Pattern

4. **gmail.com** &#8594; Replacement String

**1.** The command character (in this case **s** for substitution) must go on the left side of the first
delimiter.

**2.** The character after **s** is called a delimiter. The delimiters are needed to parse the
command, to seperate the substitution command from the search pattern and seperate the replacement string from
the search pattern. In the case of the above example, the delimiter is a slash, but the delimiter can 
be any character you want as long as there are three of them:

```
echo aol.com | sed 's_aol.com_gmail.com_'    
```

is equivalent to

```
echo aol.com | sed 's^aol.com^gmail.com^'
```

is equivalent to

```
echo aol.com | sed 'sxaol.comxgmail.comx'
```

and so forth.

Each of these instances will have the same output as the original example.

A missing delimiter while result in a "Unterminated 's' command" error.

**3.** The string you want to search for (i.e. "aol.com" the search pattern) is on the left side of the delimiter sequence. 

**4.** The string you want to replace the search pattern with (i.e. "gmail.com") goes on the right side.

Now let&#39;s look at a few real world instance where substitution would be useful.

You are working on a project that you completed a version of in 2012. Upon completing your coding you remember that your README file describing what your project does has the wrong 
version date listed in it. A bad programmer would waste their time manually changing each incorrect year number in their README, but you aren&#39;t a bad programmer. You know that
you can complete this task in a matter of seconds as opposed to ten minutes you could be using doing something more productive. All you&#39;ll type is a one line into your terminal:

```
sed 's/2012/2014/g' README.md > newREADME.md; cat newREADME.md > README.md; rm newREADME.md
```

**NOTE:** It is important to keep in mind that `sed` will not replace the text in the input file on its own. `sed` will print the modified text to stdout. So inorder to capture the 
changes, you must use output redirection to copy the modified input file into a new file and then put copy the contents of the new file back into the old input file. Lastly, you 
would delete the file you created to do the file transformation (it is always considered good prectice to delete files you don&#39;t need).  



###Why Should We Ever Use *sed*?
