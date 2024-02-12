# Lab Report #2
CSE 15L - Joe Politz - 10:00am - 11:50am | Manh Tri Nguyen | A17913483 | man026@ucsd.edu
### Bugs from Week 4 Lab
1. Failure inducing-input for the buggy program
     ```java
     @Testpublic void appendTest() {
       for(int i = 10; i >= 0; i--) {
         emptyList.append(i);
      }
      assertEquals(0, this.emptyList.last());
    assertEquals(emptyList.length(), 11);
    }
     ```
