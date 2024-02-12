# Lab Report #2
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
- First variation
- Second variation
- Third variation
- Fourth variation

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
