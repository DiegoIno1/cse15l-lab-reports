<h1>Part 1</h1>

<h3>Diego Inostroza:</h3>
  
Hi! I was running my grading script, and for some reason, I have a test that's always failing.
![Image](https://i.imgur.com/WtYV6fh.png)
I've tried tweaking some of my code, but I can't get it to work. I think it might be an issue with how my tests could be set up, but I'm not entirely sure. I think it could be possible that in my test file, there could be a typo or something that is stopping my test from properly running. Although I can see the symptom of the bug (as any scores can't go higher than 1/2), I'm not sure where to go from here.
  
  
<h3>TA:</h3>
  
Hey Diego, have you tried looking at the variables stored? Since you've only really provided us with the image of your input and output, rather than the code itself, the most we can do to help you is a few general debugging solutions. What are you doing with your JUnit output?
  
  
<h3>Diego Inostroza:</h3>
  
My JUnit output is being redirected to a .txt file named `Grade.txt`. within my grading area. I'm using the line `java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > Grade.txt` to do this within my bash file. Just incase you need it, this is the relevant file structures, so that you can have a better idea. I'm running grade.sh, which uses `cp` to get into `grading-area`, where `TestListExamples` is being ran with JUnit and redirected into Grade.txt.
```
TestListExamples.java
grade.sh

./grading-area:
   Grade.txt
   TestListExamples.class
   TestListExamples.java
   /lib:
      hamcrest-core-1.3.jar
      junit-4.13.2.jar
```
  
  
<h3>TA:</h3>
  
Alright that line looks like it should work, assuming that $CPATH is correct. Since JUnit outputs the reason for tests failing, instead of just saying whether the test passed or failed, I want you to run the case in which it's supposed to succeed, then let me know what you see in that file.
  
  
<h3>Diego Inostroza:</h3>
  
This is what my JUnit output is.
  
![Image](https://i.imgur.com/0Jfknb4.png)
  
  
<h3>TA:</h3>
  
Okay, so if you look at the documentation of the merge method, it is supposed to output the items in order, however, in the expected, it seems that you mistook a "e" for a "c". While the student's output was what your expected should have been. When creating your second test, it seems that you made a typo, and created a bug within the program, as you made a test which can't be passed when the student's test functions correctly.    
