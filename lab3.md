# Lab Report #2
CSE 15L - Joe Politz - 10:00am - 11:50am | Manh Tri Nguyen | A17913483 | man026@ucsd.edu
### Bugs from Week 4 Lab
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
   - Non-error
     <img width="994" alt="image" src="https://github.com/man3ng/cse15l-lab-reports/assets/141669725/db0fe5fa-da49-4f09-a2bd-c2a077e1a301">
