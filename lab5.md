# Lab Report #5
CSE 15L - Joe Politz - 10:00am - 11:50am | Manh Tri Nguyen | A17913483 | man026@ucsd.edu

### Reference Material:
1. Grading Code
```bash
original_dir=`pwd`

for submission_dir in submissions/*
do
  echo $submission_dir
  cd $submission_dir

  javac Sorter.java 2> compile-feedback.txt

  # Replace this with a condition that does the appropriate check
  if [ $? -ne 0 ];
  then
    echo "$submission_dir: Compile error" > result.txt    
    cd $original_dir
    continue
  else
    echo "Compile successful for $submission_dir"
  fi

  passed=0
  failed=0
  for test_file in $original_dir/test-data/*.txt
  do
    result=`java Sorter < $test_file`
    expect=`cat $test_file.expect`
    if [[ $expect == $result ]]
    then
      passed=$(( $passed+1 ))
    else
      failed=$(( $failed+1 ))
    fi
  done
  echo "$submission_dir: Test results: $passed passed, $failed failed" > result.txt
  echo "$submission_dir: Test results: $passed passed, $failed failed" > result1.txt

  cd $original_dir
done

all_results=`find submissions -name "result.txt"`
cat $all_results | grep "Compile error"  > compile-errors.txt

# Here, add code to put all of the results for files that successfully ran into
# run-results.txt
cat $all_results | grep "Test results" > run-results.txt
```
2. Student's current Sorter.java file:
```java
import java.util.ArrayList;
import java.util.Scanner;
import java.util.Collections;

class Sorter {
  public static void main(String[] args) {
    ArrayList<Integer> a = new ArrayList<>();
    Scanner in = new Scanner(System.in);
    
    System.out.println("Enter a list of integers separated by spaces:");
    String s = in.nextLine().trim();

    for(String num: s.split(" ")) {
      a.add(Integer.parseInt(num));
    }
    for(int i = 0; i < a.size(); i += 1) {
      System.out.print(a.get(i));
      if(i < a.size() - 1) { System.out.print(" "); }
    }
    System.out.println();
  }
}
```

3. Student's result.txt file:
`submissions/student2: Test results: 1 passed, 1 failed`

### Original Post:
Summary: The student is having an issue with his file, Sorter.java. The current lab is to be able to find the and fix error of the file. The TA, me, will guide the student to the answer after running the student's file with a bash file in the background. In this problem, assume the student doesn't have access to the internal testing file that the TA have. They only have some inputs to test on and the test is rudimentary to encourage the students to write custom tester. The instructor test file will tell the students that they had fail the test but not specifically which one.

![image](https://github.com/man3ng/cse15l-lab-reports/assets/141669725/601d7589-8464-4c49-917d-64f89e42c188)

### Troubleshooting:
1. Directory Structure:
   - Here, I have a few other students file to compare to and work with because there are more than one students who have completed the assignment or still having issue with the assignment.
```
PS C:\Users\tring\Downloads\cse15l-lab-5> pwd

Path
----
C:\Users\tring\Downloads\cse15l-lab-5

PS C:\Users\tring\Downloads\cse15l-lab-5> tree /f
C:.
└───skill_demo3_data
    │   .gitignore
    │   grade.sh
    │
    ├───submissions
    │   ├───student1
    │   │       Sorter.java
    │   │
    │   ├───student2
    │   │       Sorter.class
    │   │       Sorter.java
    │   │
    │   ├───student3
    │   │       Sorter.java
    │   │
    │   ├───student4
    │   │   └───pa3-code
    │   │           Sorter.java
    │   │
    │   ├───student5
    │   │       Sorter.java
    │   │
    │   └───student6
    │           Sorter.java
    │
    └───test-data
            input1.txt
            input1.txt.expect
            input2.txt
            input2.txt.expect
```
