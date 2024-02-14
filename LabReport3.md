<h1>Part 1</h1>

<h3>Failure-Inducing Input in ListExamples</h3>

```
class TestingStringTester implements StringChecker{
    @Override
    public boolean checkString(String s){
        return (s.substring(0,1).equals("A"));
    }
}

public class ListTests {
    @Test
    public void TestFilter(){
        List<String> input1 = Arrays.asList("Apple", "Banana", "Candy", "Aioli", "Lettuce");
        List<String> expectedOut = Arrays.asList("Apple", "Aioli");
        StringChecker checker = new TestingStringTester();
        List<String> finalList = ListExamples.filter(input1, checker); 
        assertEquals(expectedOut, finalList);
    }
}
```
    
   
<h3>Non-Failure Input in ListExamples</h3>

```
class TestingStringTester implements StringChecker{
    @Override
    public boolean checkString(String s){
        return (s.substring(0,1).equals("A"));
    }
}

public class ListTests {
    @Test
    public void SuccessTestFilter(){
        List<String> input1 = Arrays.asList("Banana","Egg");
        List<String> expectedOut = Arrays.asList();
        StringChecker checker = new TestingStringTester();
        List<String> finalList = ListExamples.filter(input1, checker); 
        assertEquals(expectedOut, finalList);
    }
}
```

<h3>Symptoms</h3>

![Image](https://i.imgur.com/wZRiN7R.png)

<h3>Before the Bugfix</h3>

```
static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(0, s);
      }
    }
    return result;
  }
```

<h3>After the Bugfix</h3>

```
static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(s);
      }
    }
    return result;
  }
```
<h5>The Reason Why This Fix Works</h5>
The bug initially added all of the correct elements to the list, however, the issue was the fact that it added each element to the beginning of the ArrayList. This caused the entire returned list to be returned backwards. For this reason, simply changing the `add` method to append the given string allows for the bug to be fixed. 

