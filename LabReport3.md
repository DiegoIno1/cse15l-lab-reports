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
<h4>The Reason Why This Fix Works</h4>

The bug initially added all of the correct elements to the list, however, the issue was the fact that it added each element to the beginning of the ArrayList. This caused the entire returned list to be returned backwards. For this reason, simply changing the `add` method to append the given string allows for the bug to be fixed. 

<h1>Part 2</h1>

<h2>Alternate Command-line options of Grep</h2>

<h3>-c</h3>

`-c` allows grep to output the count of matching lines.

```
diego@LAPTOP-I86GVFH5 MINGW64 ~/.vscode/CSE15L REPO/docsearch-1 (main)
$ grep -c "at" technical/911report/chapter-1.txt
284
```

Here, `-c` is being used to view the contents of a specific file, "chapter-1.txt". It's counting how many lines contain "at", and returning the count of lines that contain it. This could potentially be used in a situation where one may want to see how often a specific word is being used within a piece. If used alongside writing, `-c` could indicate repetitive word choice if it is used to scan a document.

```
diego@LAPTOP-I86GVFH5 MINGW64 ~/.vscode/CSE15L REPO/docsearch-1 (main)
$ grep -c "alcohol" technical/government/Alcohol_Problems/*.txt
technical/government/Alcohol_Problems/DraftRecom-PDF.txt:53
technical/government/Alcohol_Problems/Session2-PDF.txt:97
technical/government/Alcohol_Problems/Session3-PDF.txt:168
technical/government/Alcohol_Problems/Session4-PDF.txt:164
```

In this situation, `-c` is being used on every file in a directory. With this, it is returning the amount of lines that contain "alcohol" in each of the sessionns. If used on a directory with different chapters of a book, it could allow us to view trends. For example, grabbing the amount of lines that contain a certain character's name could allow us to draw trends on that character's rates of appearance.
  
Source: https://www.geeksforgeeks.org/grep-command-in-unixlinux/

<h3>-n</h3>

`-n` allows grep to precede each line by a line number.

```
diego@LAPTOP-I86GVFH5 MINGW64 ~/.vscode/CSE15L REPO/docsearch-1 (main)
$ grep -n "46 minutes" technical/911report/chapter-1.txt
166:    By all accounts, the first 46 minutes of Flight 93's cross-country trip proceeded routinely. Radio communications from the plane were normal. Heading, speed, and altitude ran according to plan. At 9:24, Ballinger's warning to United 93 was received in the cockpit. Within two minutes, at 9:26, the pilot, Jason Dahl, responded with a note of puzzlement: "Ed, confirm latest mssg plz-Jason."
172:    The terrorists who hijacked three other commercial flights on 9/11 operated in five-man teams. They initiated their cockpit takeover within 30 minutes of takeoff. On Flight 93, however, the takeover took place 46 minutes after takeoff and there were only four hijackers. The operative likely intended to round out the team for this flight, Mohamed al Kahtani, had been refused entry by a suspicious immigration inspector at Florida's Orlando International Airport in August.
```

In this situation, `-n` is being used with grep in order to see where "46 minutes" occurs within the "chapter-1.txt" file. It's returning each line that contains the text while also returning its corresponding line number. This could be used in order to search for specific things within a long file. Rather than manually searching, `gren -n` could be used to find specific lines that could contain a commonly made typo or desired word.

```
$ grep -n "media" technical/government/media/*.txt
technical/government/media/Abuse_penalties.txt:93:and immediate delivery and service of PFA orders.
technical/government/media/Abuse_penalties.txt:116:violence deserve immediate, consistent, respectful treatment and
technical/government/media/AP_LawSchoolDebts.txt:25:attend law school, where median tuition is nearly $23,000 a year,
technical/government/media/AP_LawSchoolDebts.txt:46:The median starting salary last year at private law firms, was
technical/government/media/Avoids_Budget_Cut.txt:104:protection from abuse order.'" Benitez said. "So I immediately
technical/government/media/Barnes_new_job.txt:29:took Barnes' decision to put the national media spotlight on our
technical/government/media/BergenCountyRecord.txt:86:Rep. William Pascrell Jr., D-Paterson, who has sought to mediate
technical/government/media/Disaster_center.txt:64:"Once flood victims' immediate needs are met, they may encounter
technical/government/media/Domestic_violence_aid.txt:49:immediate legal assistance services for the protection of the
technical/government/media/Farm_workers.txt:12:field in Olathe, said they felt sick immediately: They gasped for
technical/government/media/Farm_workers.txt:46:immediately. He said crew supervisors did not report what workers
technical/government/media/Farm_workers.txt:170:insects on agricultural crops can cause immediate sickness in
technical/government/media/Greedy_Generous.txt:11:Immediately following the site greedyassociates.com appeared the
technical/government/media/IOLTA_INTEREST_RATE.txt:18:immediate access to the funds, or for small amounts whose interest
technical/government/media/IOLTA_INTEREST_RATE.txt:106:they must select those most in immediate need. The rest of their
technical/government/media/Law_Schools.txt:71:their financial reach. Even at the smallest of firms, the median
technical/government/media/Law_Schools.txt:113:median student debt past $84,000, it is understandable why some
technical/government/media/Law-school_grads.txt:37:In 2001, median private law school tuition was about $23,000 a
technical/government/media/Local_Attorneys.txt:127:started coming back by fax almost immediately."
technical/government/media/Making_a_case.txt:110:mediator, judge-conducted settlement conferences, arbitration,
technical/government/media/Making_a_case.txt:111:private mediators or other methods.
technical/government/media/Marylands_Legal_Aid.txt:21:mediaCoall critical components to make justice available to all in
technical/government/media/Oregon_Poor.txt:17:put under . . . pressure to purchase the car immediately. Eva can't
technical/government/media/Oregon_Poor.txt:21:"Eva immediately had problems with the car. She tried to return
technical/government/media/predatory_loans.txt:118:percent. Their mortgage payments immediately jumped $1,200 a month,
technical/government/media/The_State_of_Pro_Bono.txt:154:immigrants' detention were not immediately clear and sometimes had
```

Here, `-n` is being used on every file in the "media" directory. This allows us to view every file alongside the specific line numbers in which the word "media" exists. Similarly to the first example, this could allow us to more easily look for certain words or phrases within a large section of text, allowing for far easier searching within directories.
  
Source: https://www.geeksforgeeks.org/grep-command-in-unixlinux/

<h3>-h</h3>

`-h` allows grep to output matching files without preceding them by their file names.

```
diego@LAPTOP-I86GVFH5 MINGW64 ~/.vscode/CSE15L REPO/docsearch-1 (main)
$ grep -h "Bin Laden" technical/911report/chapter-13.4.txt
                Terrorism, Sudan Struck a Blow by Fleecing Bin Laden," Wall Street Journal, Dec. 3,
                Bin Laden: How Bill Clinton's Failures Unleashed Global Terror (Regnery, 2003),
                memo,"U.S. Engagement with the Taliban on Usama Bin Laden," undated (attached to NSC
```

In this instance, `grep -h` is being used in order to return all of the instances of "Bin Laden" in the text file. Since this is on one singular file, there is no discernable difference between `grep -h` and `grep`. In order for it to be used properly, it needs to be called onto multiple files, since the file name isn't returned when a singular file is called..

```
grep -h "phone" technical/plos/*.txt
        fighting teams enter wind flow data online or by telephone to a central base where gridded
        Even more remarkable, put a sensitive microphone in the ear canal and you will usually
        science as spontaneous otoacoustic emission, the sound registered by the microphone is a
        physicist David Kemp first put a microphone to an ear and discovered the telltale sounds of
        ringing in the ear (tinnitus), and daringly suggested that if a microphone were put next to
        the ear, a corresponding sound might be picked up. He experimented, placing a microphone in
        to the job—in 1948 microphones weren't sensitive enough—and the experiment, sadly,
        scientist at a major drug company—participated by phone.
        Lenzer's phone call to PLoS, enquiring whether we might step in, came just ten days
        participated via speakerphone. The whistleblowers came from an extraordinary variety of
```

In this scenario, `grep -h` is being called to parse through all of the txt files within the plos directory, searching for instances of "phone". However, it doesnt include the file paths. Because of this, if it is placed into a txt file using `>`, or used as the input for another command, the data can be parsed in order to gather more information on lines where specific words or phrases appear. Normally, this wouldn't work as well, as the file paths could be identified as text when being parsed.
  
Source: https://www.geeksforgeeks.org/grep-command-in-unixlinux/

<h3>-v</h3>

`-v` returns all lines that do not contain the given text.

```
$ grep -v " " technical/government/Alcohol_Problems/Session2-PDF.txt





tests
drinks).
subgroups.
questionnaires.7
administer.24,25
version.26-28
explore.38
questionnaires
protocol.
behaviors.
References
1979;47:205-6.
1992;53:197-202.
1991;52:33-6.
1998;46:328-35.
1974;131:1121-3.
1972;129:342-8.
1971;127:1653-8.
1975;36:117-26.
1991;15:155-7.
1989;160:863-70.
2000;160:1977-89.
1995;19:628-34.
1996;11:426-30.
1994;15:303-10.
1987;35:864-9.
1999;36:33-9.
```

Here, `grep -v` is used in order to return all lines that do not contain any spaces. This allows for us to find any single word lines. This could be useful in a coding scenario, as I personally like to use print statements throughout my code in order to track what is currently running, and `grep -v` could allow me to put everything into a new file while only excluding my test statement lines.

```
diego@LAPTOP-I86GVFH5 MINGW64 ~/.vscode/CSE15L REPO/docsearch-1 (main)
$ grep -v " " technical/government/Alcohol_Problems/*.txt
technical/government/Alcohol_Problems/DraftRecom-PDF.txt:
technical/government/Alcohol_Problems/DraftRecom-PDF.txt:
technical/government/Alcohol_Problems/DraftRecom-PDF.txt:
technical/government/Alcohol_Problems/DraftRecom-PDF.txt:
technical/government/Alcohol_Problems/DraftRecom-PDF.txt:
technical/government/Alcohol_Problems/DraftRecom-PDF.txt:discussion.
technical/government/Alcohol_Problems/DraftRecom-PDF.txt:patients.
technical/government/Alcohol_Problems/DraftRecom-PDF.txt:recommendations.
technical/government/Alcohol_Problems/DraftRecom-PDF.txt:them.
technical/government/Alcohol_Problems/DraftRecom-PDF.txt:consequences.
technical/government/Alcohol_Problems/DraftRecom-PDF.txt:drinking.
technical/government/Alcohol_Problems/DraftRecom-PDF.txt:clinical
technical/government/Alcohol_Problems/DraftRecom-PDF.txt:interventions.
... note 240 lines omitted ...
```
  
In this scenario, `grep -v` is being used to return every file within the Alcohol_Problems directory that excludes spaces. Although it may be a lot to process in a case where there are hundreds of matching lines, in a smaller directory, it could potentially be used in order for a similar case to the previous use of `grep -v`, where words are grabbed in a way that allows for you to take away unneeded lines of information and concatenate at the same time.
  
Source: https://www.geeksforgeeks.org/grep-command-in-unixlinux/
