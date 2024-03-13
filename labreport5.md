<h1>Part 1</h1>

<h3>Diego Inostroza:</h3>
  
Hi! I was running my grading script, and for some reason, I have a test that's always failing. I'm running `bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-corrected`, which should work according to the lab.
  
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
  
And this is what is inside of my grade.sh file
```
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission
echo 'Finished cloning'

# Check existence of ListExamples.java

if ! [[ -f student-submission/ListExamples.java ]]
then
    echo "Missing Necessary Files"
    exit
fi
echo "continue"

cp student-submission/ListExamples.java TestListExamples.java grading-area
cp -r lib grading-area

cd grading-area

javac -cp $CPATH *.java
if [ $? -ne 0 ]
then
    echo "Compilation Error"
    echo "0%"
    exit
fi

java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > Grade.txt

lastline=$(cat Grade.txt | tail -n 2 | head -n 1)
tests=$(echo $lastline | awk -F'[, ]' '{print $3}')
failures=$(echo $lastline | awk -F'[, ]' '{print $6}')
successes=$((tests - failures))

echo "Your score is $successes / $tests"
```
  
And here is my code for TestListExamples.java  
```
import static org.junit.Assert.*;
import org.junit.*;
import java.util.Arrays;
import java.util.List;

class IsMoon implements StringChecker {
  public boolean checkString(String s) {
    return s.equalsIgnoreCase("moon");
  }
}

public class TestListExamples {
  @Test(timeout = 500)
  public void testMergeRightEnd() {
    List<String> left = Arrays.asList("a", "b", "c");
    List<String> right = Arrays.asList("a", "d");
    List<String> merged = ListExamples.merge(left, right);
    List<String> expected = Arrays.asList("a", "a", "b", "c", "d");
    assertEquals(expected, merged);
  }
  @Test(timeout = 500)
  public void testMergeLeftEnd() {
    List<String> left = Arrays.asList("c", "d", "e");
    List<String> right = Arrays.asList("a", "d");
    List<String> merged = ListExamples.merge(left, right);
    List<String> expected = Arrays.asList("a", "e", "d", "d", "e");
    assertEquals(expected, merged);
  }
}

```
  
  
<h3>TA:</h3>
  
Alright, since JUnit outputs the reason for tests failing, instead of just saying whether the test passed or failed, I want you to run the case in which it's supposed to succeed, then let me know what you see in that file. JUnit's output will likely point you into a far more easily understood direction, as it can be a lot of work to look at the code and debug it directly. Since you are probably doing this in ieng6, you should cd into your grading area and use the `cat` command to see what's in the JUnit output.
  
  
<h3>Diego Inostroza:</h3>
  
This is what my JUnit output is.
  
![Image](https://i.imgur.com/0Jfknb4.png)
  
  
<h3>TA:</h3>
  
Okay, so if you look at the documentation of the merge method, it is supposed to output the items in order, however, in the expected, it seems that you mistook a "e" for a "c". While the student's output was what your expected should have been. When creating your second test, it seems that you made a typo, and created a bug within the program, as you made a test which can't be passed when the student's test functions correctly. Solving this should be an easy fix, as it is just a typo, and you should replace the first "e" in the expected with a "c".
  
  
  
<h1>Part 2</h1>

One thing that I have learned in my lab experience in the second half of this quarter is the ability to use vim in a more efficient way. Although we did learn about vim in class, it's hard to remember all of the different commands just by looking at a screen and taking notes. However, in the labs, by using vim on my own, while timing myself, I became far more familiar with how to actually navigate a file in vim. Although some may find it boring, I find vim to be an incredibly interesting editor, as the ability to edit text from within a terminal means that it's entirely possible to code without an IDE. Even though its far less practical than using an IDE many times, the ability to have it seems useful in many actual cases, like when working remotely on a server. The documentation online showed many vim commands which weren't shown in class. Commands like 10G allow users to skip directly to specific lines (in this case, it skips to line 10). Online resources also showed commands which were interesting, like ciw, which replaces an entire word. Although many of these seem impractical or inherently useless in some cases, their existence is interesting to see, as it shows how navigation and text editing could be sped up, even if it is only slightly quicker than it would be to change the text by fully navigating through insert mode and changing the text.
