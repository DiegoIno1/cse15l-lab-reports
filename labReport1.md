cd Example\
Current Working Directory: /home 
(The working directory did change because of the cd command)
```
{
[user@sahara ~]$ cd
[user@sahara ~]$ cd lecture1/
[user@sahara ~/lecture1]$ cd Hello.java
bash: cd: Hello.java: Not a directory
}
```
![Image](https://i.imgur.com/d7HyF1s.png)\
For Example 1, nothing changed. This isn't exactly an error, as we are trying to change the directory, but nothing is input. Because of this, the absolute path remains the same as the workign directory.\
For Example 2, the working directory changed from /home to /home/lecture1/. This was not an error, as it did exactly what the command is intended to do.\
For Example 3, the working directory did not change. This example caused an error, as the specific file (Hello.java) is not a directory, so it can't become the working directory.\
\
ls Example\
Current Working Directory: /home
```
{
[user@sahara ~]$ ls
lecture1
[user@sahara ~]$ ls lecture1
Hello.class  Hello.java  messages  README
[user@sahara ~]$ ls lecture1/Hello.java
lecture1/Hello.java
}
```
![Image](https://i.imgur.com/9appgwb.png)\
For example 1, it printed out the list of items under the given directory. Since my working directory was /home, it output the lecture1 file. Thus, this is not an error.\
For example 2, it printed out the list of items under lecture1. Since lecture1 is a directory, the command can print out whatever is inside of it, making it not an error.\
For example 3, ?
\
cat Example\
Current Working Directory: /home
```
{                         
[user@sahara ~/lecture1]$ cat
This prints things out
This prints things out
^C 
[user@sahara ~/lecture1]$ cat messages/
cat: messages/: Is a directory
[user@sahara ~/lecture1]$ cat messages/en-ca.txt
Hello world!
}
```
![Image](https://i.imgur.com/mfLbFY3.png)\
For example 1, the cat command took whatever I was writing and would output that. This is not an error, as it is printing out all of the text it is given, since it wasn't given a specific file to read from.
For example 2, the cat command resulted in an error. Since the command reads text from files, a directory creates an error, as directories contain files, not text.
For example 3, the cat command worked as it normally does. It read the text from the en-ca.txt file, making this not an error.
