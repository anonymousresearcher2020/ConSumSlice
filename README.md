# ConSumSlice

This repository hosts ConSumSlice, a regression analysis approach based on program slicing. 
Given a test failure and two versions of a program and a test passing on one and failing on the other version of the program, 
ConSumSlice automatically generates a summarized version of the slices produced by the dual slicing technique. 

## Table of Contents
1. [Requirements](#Requirements)
2. [Building the Tool](#Building-the-Tool)
3. [Running the Tool](#Running-the-Tool)

---
---

## Requirements

* Running platform: MacOS

* Java Runtime Environment version: 8

* Eclipse version: 4.16

---
---

## Building the Tool

ConSumSlice relies on the TRegression (ERASE) (https://github.com/llmhyy/tregression) project to align the two traces. It also relies on Slicer4J (https://github.com/resess/Slicer4J) to compute control and data-flow dependencies. 
To prevent any inconsistencies between the tool versions that we used and newer versions, 
we included the repositories of Slicer4J, ERASE, and its underlying Microbat (https://github.com/llmhyy/microbat) project.

1. Start with cloning the repository:
````yaml
git clone https://github.com/anonymousresearcher2020/ConSumSlice.git
````
In this repo, we provide:
- microbat: including all microbat subprojects
- tregression
- Slicer4J
- ConSumSlice

Note that ConSumSlice, Microbat, and TRegression projects are Eclipse plugin project. 

2. You need to import the following projects through "Existing Projects into Workspace":

<img align="right" src="img/structure.png" alt="drawing" width="350"/>

- ConSumSlice
- mirobat/experiment.utils
- microbat/mirobat
- mirobat/microbat_instrumentator
- mirobat/microbat_junit_test
- mirobat/mutation
- mirobat/sav.commons
- tregression/tregression


3. Please unzip the junit_lib (https://github.com/anonymousresearcher2020/ConSumSlice/blob/main/ConSumSlice/lib/junit_lib.zip) under the dropins directory of your eclipse root folder. It contains all the runtime Java libraries required for running microbat and tregression:
````yaml
$path-to-eclipse_root_folder/dropins/junit_lib
````
For example,
````yaml
/Applications/Eclipse.app/Contents/Eclipse/dropins
````

---
---
## Running the Tool
### General guideline: Running with Main() method in Run
Now, you can run ConSumSlice through the main method in the run class (run as "Java Application"):

![](/img/run.png)

The main method takes as input following four arguments: 
- the path to the base folder, including two versions (See below for our subjects and Defects4J). 
- The benchmark name to run: ConSumSlice, Math, Closure, ....
- The bug_id
- The failing test

Here is an example of the structure of the bug repositories:

![](/img/fileStructure.png)

---

### Running on Our Subjects
As running the client and library projects needs merging two projects in one and creating a merged jar to run Slicer4J, we provide the merged and ready to run folders in a Google Drive folder (https://drive.google.com/file/d/1XZ_lJG7cgMJvOSvlURCJgSG3Hu-cFvWM/view?usp=share_link).

The structure of the folder is as follows:

|__ ConSumSlice<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|__ 1 <br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|__ 2 <br /> 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|__ ...<br />

Here is an example of running bug_id 6 of ConSumSlice subjects:

![](/img/args.png)

Where, the base folder storing the ConSumSlice subjects is "/Documents/Projects/defects4j/bug_repos/". 
"ConSumSlice" is the name of the benchmark to run. 
Bug_id is 6 and the failing test is "com.intuit.wasabi.export.rest.impl.DefaultRestEndPointTest::testGetRestEndPointURI".

The failing test (test_class::test_method) is stored in the "failing_tests" file in the buggy version of each subject. 

---

### Running on Defects4J
Follow the instructions in https://github.com/llmhyy/tregression to create the Defects4J Benchmarks: 
The structure of Defects4J is as follows:

|__ Math<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|__ 1 (bug_id)<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|__ 2 (bug_id)<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|__ ...<br />
|__ Closure<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|__ 1 (bug_id)<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|__ 2 (bug_id)<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|__ ...<br />

You can run each bugs similar to running our subjects. 

---
