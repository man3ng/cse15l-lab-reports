# Lab Report #3
CSE 15L - Joe Politz - 10:00am - 11:50am | Manh Tri Nguyen | A17913483 | man026@ucsd.edu
### Part One: Bugs from Week 4 Lab
1. Failure inducing-input for the buggy program
     ```java
     @Test
     public void appendTest() {
          for(int i = 10; i >= 0; i--) {
               emptyList.append(i);
          }
          assertEquals(0, this.emptyList.last());
          assertEquals(emptyList.length(), 11);
     }
     ```
     - For this particular append method for the LinkedList, the aim of the JUnit test is to add multiple inputs sequentially to the list and check how many elements there are in the list after all the element it is added. This aimed to test not only the `append()` method, which is our main focus, but also the `length()` method. The total should return an integer of 11 for the length, and the last element should be 0.

2. Input that doesn't induce failure
     ```java
     @Test
     public void appendTest() {
          emptyList.append(1);
          assertEquals(emptyList.root.value, 1);
     }
     ```
     - For this particular test, we are initializing an empty list. We are appending to the list with the element 1. According to the method, when the root is null, the method will replace the root's value as the inputted value.

3. The symptoms of the failure input and non-failure input
   - Error

     <img width="821" alt="image" src="https://github.com/man3ng/cse15l-lab-reports/assets/141669725/cb6838e6-ef0b-48ae-b554-797d47ce1126">

     - The reason that we are running out of heap space is that we are running in an infinite while loop if we leave the original error code intact. The code continuously check if the node next value or not, but it also creating a next node with a value of the argument and the next pointer to null. `n.next = new Node(value, null);`, with this line of code, we will never reach the end because we are one step behind the node with the value of null.
   - Non-error
     <img width="994" alt="image" src="https://github.com/man3ng/cse15l-lab-reports/assets/141669725/db0fe5fa-da49-4f09-a2bd-c2a077e1a301">

     - The reason that this doesn't induce an error is due to this conditional as the method is called:
       ```java
       if(this.root == null) {
            this.root = new Node(value, null);
            return;
        }
       ```
       As you can see, since the list is empty. The root will be replaced with the element, setting the next element equal to null, and we will exit the method.
4. The before-and-after code blocks to fix the bug
   - Before:
     ```java
     public void append(int value) {
        if(this.root == null) {
            this.root = new Node(value, null);
            return;
        }
        // If it's just one element, add if after that one
        Node n = this.root;
        if(n.next == null) {
            n.next = new Node(value, null);
            return;
        }
        // Otherwise, loop until the end and add at the end with a null
        while(n.next != null) {
            n = n.next;
            n.next = new Node(value, null);
        }
     }
     ```
   - After:
     ```java
     public void append(int value) {
        if(this.root == null) {
            this.root = new Node(value, null);
            return;
        }
        // If it's just one element, add if after that one
        Node n = this.root;
        if(n.next == null) {
            n.next = new Node(value, null);
            return;
        }
        // Otherwise, loop until the end and add at the end with a null
        while(n.next != null) {
            n = n.next;
        }
        next = new Node(value, null);
     }
     ```
     As you can see between the before and after image, let's focus on this particular operation `next = new Node(value, null);`. It is setting the next non null node to be the the value, which should be the last node of the Linkedlist. Also, it will create a new tail node with the value of null. However, in the original code, it is set inside, which keep generating the next non-null node, and the while loop never managed to catch the node that is not null which caused the "heap space" error. The quick fix was to put `next = new Node(value, null);` outside and after the while loop.
### Part Two: Researching Command Lines Options - `GREP`
1. First variation: `grep -r "pattern" directory/`
  - The function is recursively searching the inputted directories and search everything in there that has the pattern
    1. Input: `trilosophe@Trilosophes-MBP-16 docsearch % grep -r "tri" technical/`
       //
       Output:
       `technical//biomed/1476-069X-2-9.txt:        in this study it was found that chemical distribution
       technical//biomed/1476-069X-2-9.txt:        Authors' contributions
       technical//biomed/1478-1336-1-3.txt:        intrinsic histone acetyltransferase activity suggests that
       technical//biomed/1478-1336-1-3.txt:          105 per well) in 5% charcoal stripped serum (Hyclone,
       technical//biomed/1478-1336-1-3.txt:          phenol red-free DMEM containing 5% charcoal stripped
       technical//biomed/1478-1336-1-3.txt:        Authors' Contributions
       technical//biomed/1471-2164-2-4.txt:          restriction endonuclease Alu I and assayed in two
       technical//biomed/1471-2164-2-4.txt:          determined by restriction fragment length polymorphism or
       technical//biomed/1471-2164-2-4.txt:          samples were repeated in triplicate the genotyping
       technical//biomed/1471-2164-2-4.txt:        triplicate, the genotyping accuracy jumped to over 99%. The
       technical//biomed/1471-2164-2-4.txt:        and industrial laboratories.
       technical//biomed/1471-2164-2-4.txt:          CAU). The DNA samples were digested with the restriction`

       I recursively searched within the `technical/` directory find any files and sub-directories with the pattern of **"Tri"**. There were hundred of lines that have the matched pattern. I didn't include it here due to space. Biggest downside, if you are looking through all of this, there are too many files to look at and you can't get much out of it.
    3. Input: `grep -r "Tri" technical/ | wc -l`
       <br>
       Output: `900`
       With `| wc -l`, from the output before, we are counting the entire line of the file from the `grep -r` that contains **"Tri"**. In total, we have 900 lines. This is slightly more useful because now you have a precise information out of all the raw data from before.
            
2. Second variation: `grep -A <afterlineNum> "filename"`
  - To follow up with the last command, we are displaying the content of a particular file that we want onto the terminal after a certain line numbers.
    1. Input: `trilosophe@Trilosophes-MBP-16 Media % grep -A 5 "law" Legal_Aid_attorney.txt`
       Output:
     `Depictions of lawyers in American pop culture are
     notoriously unkind.
     Whether castigating them on the silver screen, between the lines
     of pulpy, true-crime narratives, or in the jokes told around the
     proverbial water cooler, attorneys have been on the receiving end
     of many a hackneyed punch line.
     --
     when she entered law school at Georgetown University that she
     wanted to use her training to help others.
     "A reason I went to law school was to do social justice work,"
     Schwartz said recently. "I get paid to make the community a better
     place for vulnerable people -- and I like that." Schwartz grew up
     in Charlotte, N.C. She earned a bachelor's degree in English
     literature from Davidson College before heading to Georgetown for
     her law degree, where she finished in 1993.
     "When I was in school I really liked Virginia Woolf," Schwartz
     said of her nascent literary tastes. "Right now what I read is
     nonfiction.
     "I've been reading a lot about Buddhism," she added. "I just
     sort of call it my peace studies program -- any author that I think
     --
     tribal and housing law. Legal Aid is a nonprofit national
     organization aimed at providing low-cost or free legal aid to those
     who need it.
     A South Dakota blizzard six years ago prompted her to call the
     Roseburg office, which, coincidentally, was in the process of
     trying to find her to fill the vacancy left by Rubenstein's
     trilosophe@Trilosophes-MBP-16 Media % `
     
     For this example, I am in `/Users/trilosophe/Downloads/CSE/15/LabWeek5/docsearch/technical/government/Media`. I want to display the content containing the word **"law"** in this particular file after line number **5**. It is particular useful if you are working with organized data and are searching for some particular lines of the text.
    
     2. Input: `trilosophe@Trilosophes-MBP-16 government % grep -r -A 5 "law" Media/ | wc -l`
        Output: `4445`
        I am in `/Users/trilosophe/Downloads/CSE/15/LabWeek5/docsearch/technical/government` and combining the technique from the previous example to recursively search through the `Media/` directory to find all the files with the pattern **"law"** after line number 5 and count the number of lines that are outputing.
3. Third variation: `grep -v "pattern" <filename>`
  - We are displaying the part that do not match that pattern. It is particularly useful if you are looking for something that's wrong.
    1. Input: `trilosophe@Trilosophes-MBP-16 plos grep -v "Tri" pmed.0020024.txt %`
       Output:
       `Many different things combine to cause epidemics of disease. Among these factors are the
        characteristics of the infecting organism, the resistance of the host, and, as is
        increasingly realized, climatic conditions.
        El Niño, the best known climatic disturbance, is caused by a warming of the Pacific
        Ocean, which then affects the climate globally. Previous work has suggested that this
        recurring phenomenon can have a profound effect on the incidence of many diseases,
        including dengue, malaria, and diarrheal diseases.
        In a paper in this month's 
        PLoS Medicine , Sultan and colleagues from a climate research institute
        and an infectious diseases center in France looked at the relation between climate and
        meningitis outbreaks in Mali in West Africa, a region that every year between February and
        May sees devastating epidemics of meningococcal meningitis affecting up to 200,000 people.
        The most important recurring climatic event in this region is a dry wind, known as the
        Harmattan, that blows throughout the winter, causing a drop in humidity and the production
        of vast quantities of dust.
        What the authors found was that over the years 1994–2002, the week of the onset of the
        yearly meningitis epidemic came at around the same time as the peak of one measure of the
        wind—the sixth week of the year. As Pascual and Dobson say in their Perspective article on
        this study, “Sultan and colleagues' study is exceptional in that it illustrates a clear
        relationship between an external environmental variable and the initiation of disease
        outbreaks.”
        How do climatic changes influence disease? In some cases, such as the role of flooding
        in spreading a waterborne disease, the causes are perhaps obvious, but why should a dry
        wind affect disease incidence? Previous works have suggested that the climate can work in a
        number of ways, by influencing the life cycle of both disease vectors and the
        disease-causing organism, and, as here perhaps, by affecting the resistance of the host.
        Sultan and colleagues speculate that the drying effects of the wind on the mucous membranes
        could increase the chances of the organism getting established in the human host. Whatever
        the causes, one very useful feature of climate is that, once the patterns are understood,
        they can often be predicted.
        A way of predicting these meningitis epidemics could be enormously useful. Sultan and
        colleagues looked at only a few years, but if these findings are confirmed over a longer
        time period, they could make preparing for an epidemic much more efficient.`

       Here, we are in `/Users/trilosophe/Downloads/CSE/15/LabWeek5/docsearch/technical/plos` and we are exploring one of the file in this directory to display all the lines that do not match **"Tri"** from this particular file.
    3. Input: `trilosophe@Trilosophes-MBP-16 technical % grep -r -n -v "Tri" plos/ | wc -l`
       Output: `38054`
       While I could display all the lines, it would not be able to fit all of them in this particular document. However, if you are trying to remove a particular file with the "pattern" out of the directory, now you have all the files needed for your automated tool to start removing. Extremely useful!
4. Fourth variation: `grep -c "pattern" <file_name>`
   Whenever you want to know how many lines match the pattern, use this command.
   1. Input: `trilosophe@Trilosophes-MBP-16 911report % grep -c "help" chapter-13.5.txt`
      Output: `13`
      Here we are counting how many lines in `/Users/trilosophe/Downloads/CSE/15/LabWeek5/docsearch/technical/911report` file named `chapter-13.5.txt` that contains the pattern **"help**. The output said there are 13 occurences.
   2. Input: `trilosophe@Trilosophes-MBP-16 technical % grep -r -c "help" 911report/`
      Output: `911report//chapter-13.4.txt:13
               911report//chapter-13.5.txt:13
               911report//chapter-13.1.txt:10
               911report//chapter-13.2.txt:0
               911report//chapter-13.3.txt:3
               911report//chapter-3.txt:12
               911report//chapter-2.txt:12
               911report//chapter-1.txt:6
               911report//chapter-5.txt:18
               911report//chapter-6.txt:16
               911report//chapter-7.txt:28
               911report//chapter-9.txt:12
               911report//chapter-8.txt:5
               911report//preface.txt:3
               911report//chapter-12.txt:22
               911report//chapter-10.txt:5
               911report//chapter-11.txt:2`

      Here we are counting how many lines through the recursive method in the directory `911report/` with the pattern **"help"**. The output is listing for all the files in there and how many times did the pattern occur.

- Citation:
  - ChatGPT:
    - Prompt: "give me all the useful variations of using grep"
    - Output:
      Sure, here are some useful variations of using `grep`:

     1. **Basic pattern matching**: Search for a pattern in a file.
        ```bash
        grep "pattern" file.txt
        ```
     
     2. **Case-insensitive search**: Ignore case distinctions in both the pattern and the input files.
        ```bash
        grep -i "pattern" file.txt
        ```
     
     3. **Display line numbers**: Display line numbers along with the matching lines.
        ```bash
        grep -n "pattern" file.txt
        ```
     
     4. **Display only matching part**: Display only the part of each line that matches the pattern.
        ```bash
        grep -o "pattern" file.txt
        ```
     
     5. **Invert match**: Display lines that do not contain the pattern.
        ```bash
        grep -v "pattern" file.txt
        ```
     
     6. **Recursive search**: Search for a pattern recursively in all files under a directory.
        ```bash
        grep -r "pattern" directory/
        ```
     
     7. **Count matches**: Display only the count of matching lines.
        ```bash
        grep -c "pattern" file.txt
        ```
     
     8. **Using regular expressions**: Use regular expressions for pattern matching.
        ```bash
        grep -E "regex pattern" file.txt
        ```
     
     9. **Search for whole words only**: Match whole words only, not substrings.
        ```bash
        grep -w "word" file.txt
        ```
     
     10. **Display lines before/after match**: Display lines before or after the matching line.
         ```bash
         grep -B 3 "pattern" file.txt  # Display 3 lines before the match
         grep -A 3 "pattern" file.txt  # Display 3 lines after the match
         ```
     
     These are some of the commonly used variations of `grep` commands, but there are many more options available. You can always refer to the `grep` manual (`man grep`) for more details and options.
