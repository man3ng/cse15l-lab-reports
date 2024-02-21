# Lab Report #4
CSE 15L - Joe Politz - 10:00am - 11:50am | Manh Tri Nguyen | A17913483 | man026@ucsd.edu
## Step-by-step guide from Week 7 Lab: Vim Step 4-9

### Part One: Step 4 From Week 7 Lab
- From your desktop, open terminal / command prompt. I am on a Mac so I will use the Mac jargon. First, press `CMD + Space`, search for `Terminal` then press enter. To log in to my ieng6 account, on the terminal prompt, I will type `ssh man026@ieng6-201.ucsd.edu`. The reason I am using @ieng6-201 is because there are some devices that I have issues with so -201 is the best option. Since I already have a private SSH key store, the terminal will output below:
```
trilosophe@Trilosophes-MBP-16 ~ % ssh man026@ieng6-201.ucsd.edu
Last login: Wed Feb 21 11:27:43 2024 from 100.81.37.15
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2024-01-12_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/ieng6/cs120wi24/cs120wi24dx/.snapshot/hourly.2024-01-29_1201: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2024-02-04_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2024-02-05_0010: Stale file handle
Hello man026, you are currently logged into ieng6-201.ucsd.edu

You are using 0% CPU on this system

Cluster Status 
Hostname     Time    #Users  Load  Averages  
ieng6-201   11:25:01   24  0.82,  0.57,  0.54
ieng6-202   11:25:01   12  0.63,  0.24,  0.27
ieng6-203   11:25:01   10  0.03,  0.26,  0.26

 

To begin work for one of your courses [ cs15lwi24 ], type its name 
at the command prompt.  (For example, "cs15lwi24", without the quotes).

To see all available software packages, type "prep -l" at the command prompt,
or "prep -h" for more options.
[man026@ieng6-201]:~:144$
```
- I have successfully log on to the virtual lab machine.
**Key Pressed:** `ssh <Spacebar> man026@ieng6-201.ucsd.edu <Enter>`

### Part Two: Step 5 From Week 7 Lab
- After logging on to the lab machine, if I haven't done it already then I should create an SSH key in order to `git clone` with SSH. However, I already completed that step so I am ready to clone the forked repository from lab 7. In the terminal, I will run `git clone git@github.com:man3ng/lab7-assignment.git` to clone with SSH. It will output as below after you finish cloning.
```
[man026@ieng6-201]:~:151$ git clone git@github.com:man3ng/lab7-assignment.git
Cloning into 'lab7-assignment'...
Warning: Permanently added the RSA host key for IP address '140.82.112.3' to the list of known hosts.
remote: Enumerating objects: 58, done.
remote: Total 58 (delta 0), reused 0 (delta 0), pack-reused 58
Receiving objects: 100% (58/58), 376.39 KiB | 1.42 MiB/s, done.
Resolving deltas: 100% (21/21), done.
[man026@ieng6-201]:~:152$
```
**Key Pressed:** `git <Spacebar> clone <Spacebar> git@github.com:man3ng/lab7-assignment.git <Enter>`

### Part Three: Step 6 From Week 7 Lab
- After successfully cloning the repository `lab7-assignment` to my lab machine, I can now begin the testing process. First, on the terminal, I press `ls` to get the general idea of all the subfolders. Then I press `cd lab7-assignment` to get into the directory (`/home/linux/ieng6/oce/8o/man026/lab7-assignment`). Then, I press `bash test.sh` to run the test demonstrating that no edit to the files have been made and there will be an error outputted when running `ListExamplesTests.java` from `test.sh`.
```
[man026@ieng6-201]:~:153$ ls
lab7  lab7-assignment  new_file.txt  perl5  skill-demo1  wavelet
[man026@ieng6-201]:~:154$ cd lab7-assignment/
[man026@ieng6-201]:lab7-assignment:155$ ls
ListExamples.java  ListExamplesTests.java  lib  test.sh
[man026@ieng6-201]:lab7-assignment:156$ bash test.sh
JUnit version 4.13.2
..E
Time: 0.518
There was 1 failure:
1) testMerge2(ListExamplesTests)
org.junit.runners.model.TestTimedOutException: test timed out after 500 milliseconds
	at ListExamples.merge(ListExamples.java:44)
	at ListExamplesTests.testMerge2(ListExamplesTests.java:19)

FAILURES!!!
Tests run: 2,  Failures: 1

[man026@ieng6-201]:lab7-assignment:157$
```
**Key Pressed:** `ls <Enter>`, `cd lab7-assignment <Enter>`, `ls <Enter>`, `bash <Spacebar> test.sh <Enter>` 

### Part Four: Step 7 From Week 7 Lab
- I realized that the `ListExamples.java` file is failing the test so I will open the **VIM** text editor to go find the error and edit it. Since I am already at the correct directory (`/home/linux/ieng6/oce/8o/man026/lab7-assignment`) I don't have to change the directory or list all the sub-items under my current working directory. After getting into the **VIM** editor, I have to get to press `j` 43 times to get to the line (44) that needed to be edited. Then I press `e` to get to the first word before the last character, `dw` to delete the last character, `i` to insert with `2` as the input and `<Spacebar>` to maintain original formatting in sequence to change the variable `index1` to `index2`. Then, I pressed `<ESC>` with `:wq!` to exit and save. Now, we are back at the terminal on a new line ready for the next command.
```
[man026@ieng6-201]:lab7-assignment:160$ vim ListExamples.java
```
Before code snippet:
```
while(index2 < list2.size()) {
	result.add(list2.get(index2));
	// change index1 below to index2 to fix test
	index1 += 1;
}
```
After code snippet:
```
while(index2 < list2.size()) {
	result.add(list2.get(index2));
	// change index1 below to index2 to fix test
	index2 += 1;
}
```
**Key Pressed:** 
1. `vim <Spacebar> List<Tab>Examples.java <Enter>`, I have to manually type `.java`
2. Inside the vim editor: `j * 43` + `e` + `dw` + `i` + `2` + `<Spacebar>` + `<ESC>` + `<:wq!>`

### Part Five: Step 8 From Week 7 Lab
- At my working directory, `/home/linux/ieng6/oce/8o/man026/lab7-assignment`, I just have to rerun the `test.sh` file again to ensure that the edit is saved and the file will pass the test.
```
[man026@ieng6-201]:lab7-assignment:163$ bash test.sh 
JUnit version 4.13.2
..
Time: 0.015

OK (2 tests)

[man026@ieng6-201]:lab7-assignment:164$
```
**Key Pressed:** `bash <Spacebar> test.sh <Enter>`

### Part Six: Step 9 From Week 7 Lab
- 
