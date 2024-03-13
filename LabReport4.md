<h1>Step 4</h1>

![Image](https://i.imgur.com/sZ2tmuE.png)

Keys Pressed: `<up><enter>`
  
The command `ssh dinostroza@ieng6-202.ucsd.edu` was one command up in the search history outside of the server, so one up arrow press was needed to run it.

<h1>Step 5</h1>

![Image](https://i.imgur.com/VdujsL5.png)

Keys Pressed: `git clone <ctrl + v>`
  
Here, I just normally typed git clone, and pasted in the ssh. Since I had "git@github.com:DiegoIno1/lab7.git" already on my clipboard from my last attempt, I simply pasted it in order to clone it in without needing to press the up arrow many times.

<h1>Step 6</h1>

![Image](https://i.imgur.com/LX3ZSyE.png)

Keys Pressed: `cd l<tab><enter>bash t<tab>`
  
Here, I used the cd command to change directory to the newly created `lab7` directory, using `<tab>` after `l` since `lab7` is the only directory starting with "l" within my current directory. Then, I ran the `bash` command with the argument `test.bash` by before `t` and `<tab>` in order to autofill the `test.bash` file.

<h1>Step 7</h1>


![Image](https://i.imgur.com/0eUktxj.png)

Keys Pressed for the command: `vim L<tab>.j<tab><enter>`
  
In order to access file using vim, I ran the `vim` command `vim ListExamples.java`. Although I typed the `vim` command normally, I used `L` and `<tab>` to fill ListExamples, then `.j` and `<tab>` in order to specify that I wanted `ListExamples.java` instead of `ListExamplesTests.java`.
  
![Image](https://i.imgur.com/ELPllPe.png)  
    
Keys pressed to fix the error: `G 6k 11l r2 <escape> :wq`
  
Since the error occured near the end of the file, I used `G` to move to the bottom of the page. After that I used `6k` to move the cursor up 6 lines in order to get to the line I wanted. Then I pressed `11l` to move 11 characters to the left, with my cursor hovering over the 1 which needed to be fixed. Finally I used `r2` to replace the 1 with a 2. Finally, I used `:wq` to save and quit the file.

<h1>Step 8</h1>

![Image](https://i.imgur.com/kXs0xy9.png)

Keys Pressed: `<up><up><enter>`
  
Since the same test is being ran as before, I pressed the up arrow twice to rerun the bash command.

<h1>Step 9</h1>

![Image](https://i.imgur.com/uSbIKSv.png)

Keys Pressed: 
  
`git add L<tab>.j<tab><enter> 
git commit -m fix<enter>
git push`
  
Here, I simply used `git add` followed by the same technique used in step 7 in order to fill in `ListExamples.java`. Then, I typed in `git commit -m fix` to commit without needing vim in order to add a commit message. Finally, I used git push in order to finish pushing the updated file to github.
