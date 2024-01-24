# Lab Report #1
CSE 15L - Joe Politz - 10:00am - 11:50am | Manh Tri Nguyen | A17913483 | man026@ucsd.edu

### Using `cd`, `ls`, `cat` with no arguments.
- Using cd
  ```
  # Just my username on my home terminal
  
  trilosophe@Trilosophes-MPB-16 Favorites %

  trilosophe@Trilosophes-MPB-16 Favories % cd

  trilosophe@Trilosophes-MPB-16 ~ % 
  ```
  I am in my library directory `/Users/trilosophe/Library/Favorites` (can check with `pwd`). When using `cd` without an argument, I will be prompted to return to my home directory of the logged in user (with the `~`) which is `/Users/trilosophe`. There is no error.
  
- Using ls
  ```
  # Just my username on my home terminal
  
  trilosophe@Trilosophes-MPB-16 ~ %

  trilosophe@Trilosophes-MPB-16 ~ % ls

  Applications	Documents	Library		Music		Public
  Desktop		Downloads	Movies		Pictures	UCSD
  trilosophe@Trilosophes-MPB-16 ~ %
  ```
  I am in my home directory `/Users/trilosophe`. When using `ls` without an arugment, it will list every folders under the `../trilosophe` folder. There is no error.

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
  I am in my home directory `/Users/trilosophe`. When using `cat` without an argument, it will like like a repeater to me. Everything I input, once I press entered, will be throw out exactly the same on the terminal screen since there is no files to read. There is no error thrown, but I am stuck in that screen so I have to force quit to get out of it. You can stop with `CMD + D`.
  
### Using `cd`, `ls`, `cat` a path to with a directory as an argument.
- Using cd
  ```
  # Just my username on my home terminal

  trilosophe@Trilosophes-MPB-16 ~ %

  trilosophe@Trilosophes-MPB-16 ~ % cd Library/
  
  trilosophe@Trilosophes-MPB-16 Library %
  ```
  I am in my home directory `/Users/trilosophe`. When using `cd` with a directory as an argument, I will be redirected to that directory which is `/Users/trilosophe/Library` which is shown with `trilosophe@Trilosophes-MPB-16 Library %` prompt on the terminal. No error is thrown here because the action of changing directory is completed.
  
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
  I am in my home directory `/Users/trilosophe`. When using `ls` with a directory as an argument, the terminal will list all the folders and files within the `/Users/trilosophe/Downloads/` directory. But, I am in still at the home directory based on the last command line because I haven't moved anywhere. No error is thrown because the action is complete by listing all the sub-folders/directories under the inputted argument.
  
- Using cat
  ```
  # Just my username on my home terminal

  trilosophe@Trilosophes-MPB-16 ~ %

  trilosophe@Trilosophes-MPB-16 ~ % cat Downloads 
  cat: Downloads: Is a directory
  
  trilosophe@Trilosophes-MPB-16 ~ % 
  ```
  I am in my home directory `/Users/trilosophe`. When using `cat` with a directory as an argument, the terminal will print an error: "cat: Downloads: Is a directory"; there is nothing to concatenate and you can't concatenate directory using the specific commands nor you can view the contents of the directory (it's not a file).
  
### Using `cd`, `ls`, `cat` with a path to a file as an argument.
- Using cd
  ```
  # Just my username on my home terminal
  trilosophe@Trilosophes-MPB-16 ~ %
  
  trilosophe@Trilosophes-MPB-16 ~ % cd Downloads/lab1-test.rtf
  cd: not a directory: Downloads/lab1-test.rtf

  trilosophe@Trilosophes-MPB-16 ~ %
  ```
  I am in my home directory `/Users/trilosophe`. When using `cd` with a path to a file as an argument, the terminal throws an error: "cd: not a directory: Downloads/lab1-test.rtf". It is because the file is end with an extension `.rtf` for text formatting and it is not a directory for the computer to redirect you to.
  
- Using ls
  ```
  # Just my username on my home terminal
  trilosophe@Trilosophes-MPB-16 ~ %
  
  trilosophe@Trilosophes-MPB-16 ~ % ls Downloads/lab1-test.rtf
  Downloads/lab1-test.rtf

  trilosophe@Trilosophes-MPB-16 ~ %
  ```
  I am in my home directory `/Users/trilosophe`. When using `ls` with a path to a file as an argument, the command prints out the path that you initally inputted from the prompt. No error was thrown because the action is completed when all the sub-folders are shown.
  
- Using cat
  ```
  # Just my username on my home terminal
  trilosophe@Trilosophes-MPB-16 ~ %
  
  trilosophe@Trilosophes-MPB-16 ~ % cat Downloads/lab1-test.rtf
  {\rtf1\ansi\ansicpg1252\cocoartf2759
  \cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;}
  {\colortbl;\red255\green255\blue255;}
  {\*\expandedcolortbl;;}
  \margl1440\margr1440\vieww11520\viewh8400\viewkind0
  \pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
  
  \f0\fs24 \cf0 Hello, this is my personal computer}% 

  trilosophe@Trilosophes-MPB-16 ~ %
  ```

  I am in my home directory `/Users/trilosophe`. When using `cat` with a path to a file as an argument, it will give me the information of the file. For example, with the Rich Text Formating (rtf) format, it shows all the formatting and finally my text line "this is my personal computer" at the end. For a normal `.txt` file, it will output the text in the file. No error is thrown.
