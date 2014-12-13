#SED TEXT MODIFIER

Welcome to cs100! :smiley: :trollface: :fearful:

We will be learning about the `sed` bash command and the power it holds!

## <a name="Top"></a>Top

###1. [What is *sed*?](#What is *sed*?)

###2. [How Does it Work?](#How Does it Work?)

###3. [What Does it Look Like?](#What Does it Look Like?)

###4. [What Can We Do With it?](#What Can We Do With it?)

###5. [Why Should We Ever Use *sed*?](#Why Should We Ever Use *sed*?)

### <a name="What is *sed*?"></a>What is *sed*?

`sed` (standing for a {**s**}tream {**ed**}itor) is a quick and efficient way of changing the text inside of a file without having to go in and change things yourself.

#### [Top](#Top)

### <a name="How Does it Work?"></a>How Does it Work?
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

#### [Top](#Top)

### <a name="What Does it Look Like?"></a>What Does it Look Like?
The format of the `sed` command is as follows:
```
sed options ... [ script ] [ inputfile ... ]
```

* *options* refers to a passed in flag (i.e. **-n** or **-i**) 

* *script* refers to a pattern that will be used to filter the infile text

* *inputfile* refers to the filename of the file you want to modify

In practice, `sed` is not completely strict in how it can be called.

For example, say you had a file containing a list of subscriber email addresses and you accidently got the domain names wrong. One way you could quickly and painlessly resolve this 
dilemma would be to pass your old email list into the `sed` command: 
```
sed 's/aol.com/gmail.com/' oldlist > newlist
```

or
```
sed s/aol.com/gmail.com/ oldlist > newlist
```

which replaces the first occurence of "aol.com" on each line of the input source with "gmail.com".

**NOTE:** `sed` can be written with or without single quotations. Although, it is better practice to always include them. It makes seeing which instructions belong to `sed`
and which instructions belong to another command easier.

Alternatively, you can accomplish the same goal by piping the contents of the old email list to `sed`: 
```
cat oldlist | sed 's/aol.com/gmail.com/' > newlist
```

If `sed` is called without a source of input:
```
sed 's/aol.com/gmail.com/'
```

`sed` will become "hungup" and will wait for input from stdin (manually entered input from the user), which is not very useful on its own.

#### [Top](#Top)

### <a name="What Can We Do With it?"></a>What Can We Do With it?
Despite what the average programmer might suggest, `sed` can be used for more than just simple text transformations. With regular expressions, `sed` can execute much more
complicated transformations that have virtually no restricitons. You can build an entire program using only `sed` (i.e. a script that capitalizes all the vowels in a text file).
You can also make `sed` behave like other commands (i.e. `grep`, `head`, and `tail`). 

For the purposes of cs100, we will confine the scope of our usage of `sed` to the following 2 categories:

####1. [Substitution](#Substitution)
####2. [Emulation](#Emulation)

We will begin with the most widely used and most popular use of `sed`, **subsitution**.

#####1. <a name="Substitution"></a>Substitution
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

Let&#39;s say a writer for the entertainment website Variety finished writing an article about the recent Sony Pictures hack. The writer gives their article to an editor and goes on their way.
Upon reading over the writer&#39;s article the editor notices that instead of accusing North Korea of the reported hacks, they incorrectly gave South Korea the credit. The average editor would have
to go in by hand and correct this issue amongst others, but this editor is special. This editor took a minor in computer science courses in college and remembers that there is a 
quick and painless way for them to correct this pervasive error. The writer accesses the html code for the article webpage and copies it to a file in his computer called *draft1*.
The editor opens a `sed` script file he wrote to delete repeated words in the articles he or she&#39;s responsible for and adds a new command to the file:

```
#sed script file *deletes repeated words and for this specific case will transform "SOuth Korea" to "North Korea"
s/[a-zA-Z]* //2
s/SOUTH KOREA/NORTH KOREA/g
```

To apply their sed script to the article, the editor uses the `-f` flag and the name of their sed script in place of a pattern or regular expression:
```
sed -f sedscript draft1 > draft2
```

and now "draft2" holds the edited Sony hack article.


#####2. <a name="Emulation"></a>Emulation

#### [Top](#Top)

### <a name="Why Should We Ever Use *sed*?"></a>Why Should We Ever Use *sed*?
A good programmer is defined by how the spend time, how much they value time, and how efficiently they use their time. Good programmers don&#39;t waste time on tedious coding that
a program or a command can accomplish in a fraction of the time he or she would need to do it by hand. `sed` and commands like `sed` exist to encourage a "good programmer" mentality.

So when you find yourself in a position where you&#39;ve forgotten to put a set of () around a recurring conditional statenment in a file or you want to change
the name of a project in your project README, you&#39;ll have a choice to make: be a bad programmer and spend valuable time making the corrections or be a good 
programmer and have `sed` do it for you.

#### [Top](#Top)

