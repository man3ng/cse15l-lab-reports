# Lab Report #1
CSE 15L - Joe Politz - 10:50am - 1 | Manh Tri Nguyen | A17913483 | man026@ucsd.edu

### Using `cd`, `ls`, `cat` with no arguments.
- Using cd
  ```
  # Just my username on my home terminal
  
  trilosophe@Trilosophes-MPB-16 Library %

  trilosophe@Trilosophes-MPB-16 Library % cd

  trilosophe@Trilosophes-MPB-16 ~ % 
  ```
  I am in my library directory `Users/trilosophe/Library`. When using `cd` without an argument, I will be prompted to return to my home directory of the logged in user (with the `~`) which is
  `Users/trilosophe`
  
- Using ls
  ```
  # Just my username on my home terminal
  
  trilosophe@Trilosophes-MPB-16 ~ %

  trilosophe@Trilosophes-MPB-16 ~ % ls

  Applications	Documents	Library		Music		Public
  Desktop		Downloads	Movies		Pictures	UCSD
  trilosophe@Trilosophes-MPB-16 ~ %
  ```
  I am in my home directory `Users/trilosophe`. When using `ls` without an arugment, it will list every folders under the `../trilosophe` folder.

- Using cat
  ```
  # Just my username on my home terminal
  
  trilosophe@Trilosophes-MPB-16 ~ %

  trilosophe@Trilosophes-MPB-16 ~ % cat
  My name is Tri
  My name is Tri
  This is an input
  This is an input
  
  ```
  I am in my home directory `Users/trilosophe`. When using `cat` without an argument, it will like like a repeater to me. Everything I input, once I press entered, will be throw out exactly the same on the terminal screen.
  
### Using `cd`, `ls`, `cat` a path to with a directory as an argument.
- Using cd
  ```
  # Just my username on my home terminal

  trilosophe@Trilosophes-MPB-16 ~ %

  trilosophe@Trilosophes-MPB-16 ~ % cd Library/
  
  trilosophe@Trilosophes-MPB-16 Library %
  ```
  I am in my home directory `Users/trilosophe`. When using `cd` with a directory as an argument, I will redirect to that directory which is `Users/trilosophe/Library` which is shown with `trilosophe@Trilosophes-MPB-16 Library %` prompt on the terminal
- Using ls
  ```
  # Just my username on my home terminal

  trilosophe@Trilosophes-MPB-16 ~ %

  trilosophe@Trilosophes-MPB-16 ~ % ls Downloads/
  
  CSE
  DMV Address Change
  Docu
  lib
  pro_manhtri-nguyen_DLAMP-app-essay_12-29-2023(fa1).pdf

  trilosophe@Trilosophes-MPB-16 ~ %
  ```
  I am in my home directory `Users/trilosophe`. When using `ls` with a directory as an argument, the terminal will list all the folders and files within the `Users/trilosophe/Downloads/` directory. But, I am in still at the home directory based on the last command line because I haven't moved anywhere.
- Using cat
  ```
  # Just my username on my home terminal

  trilosophe@Trilosophes-MPB-16 ~ %

  trilosophe@Trilosophes-MPB-16 ~ % cat Downloads 
  cat: Downloads: Is a directory
  
  trilosophe@Trilosophes-MPB-16 ~ % 
  ```
  I am in my home directory `Users/trilosophe`. When using `cat` with a directory as an argument, the terminal will print "cat: Downloads: Is a directory" because there is nothing to concatenate and you can't concatenate directory using the specific commands nor you can view the contents of the directory (it's not a file).
  
### Using `cd`, `ls`, `cat` with a path to a file as an argument.
- Using cd
  ```
  ```
- Using ls
  ```
  ```
- Using cat
  ```
  ```
