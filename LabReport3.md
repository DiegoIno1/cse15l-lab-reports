<h1>Part 1</h1>

<h3>Failure-Inducing Input in ListExamples</h3>

```
@Test
    public void TestFilter(){
        List<String> input1 = Arrays.asList("Apple", "Banana", "Candy", "Aioli", "Lettuce");
        List<String> expectedOut = Arrays.asList("Apple", "Aioli");
        StringChecker checker = new TestingStringTester();
        List<String> finalList = ListExamples.filter(input1, checker); 
        assertEquals(expectedOut, finalList);
    }
```
    
   
<h3>Non-Failure Input in ListExamples</h3>

```
@Test
    public void SuccessTestFilter(){
        List<String> input1 = Arrays.asList("Banana","Egg");
        List<String> expectedOut = Arrays.asList();
        StringChecker checker = new TestingStringTester();
        List<String> finalList = ListExamples.filter(input1, checker); 
        assertEquals(expectedOut, finalList);
    }
```

<h3>Symptoms</h3>

[!Image]"https://i.imgur.com/6A0u4Kj.png"
