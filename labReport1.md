cd Example\
Current Working Directory: /home\ 
(The working directory did change because of the cd command)\
```
{
[user@sahara ~]$ cd
[user@sahara ~]$ cd lecture1/
[user@sahara ~/lecture1]$ cd Hello.java
bash: cd: Hello.java: Not a directory
}
```
![Image](https://i.imgur.com/d7HyF1s.png)\
\
ls Example\
Current Working Directory: /home\ 
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
\
cat Example\
Current Working Directory: /home\
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
