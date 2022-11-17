# ConSumSlice

This repository hosts ConSumSlice, a regression analysis approach based on program slicing. 
Given a test failure and two versions of a program and a test passing on one and failing on the other version of the program, 
ConSumSlice automatically generates a summarized version of the slices produced by dual slicing technique. 

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

ConSumSlice relies on TRegression (ERASE) (https://github.com/llmhyy/tregression) project to align the two traces. It also relies on Slicer4J (https://github.com/resess/Slicer4J) to compute control and data-flow dependencies. 
To prevent any inconsistencies between the tool versions that we used and newer versions, 
we included the source code of Slicer4J, ERASE, and its underlying Microbat (https://github.com/llmhyy/microbat) project.

Start with cloning the repository:
````yaml
git clone https://github.com/anonymousresearcher2020/ConSumSlice.git
````
In this repo we provide:
1. microbat: including all microbat subprojects
2. tregression
3. Slicer4J
4. ConSumSlice

Note that ConSumSlice, Microbat, and TRegression projects are Eclipse plugin project. 

1. You need to import the following projects through "Existing Projects into Workspace":

- microbat/mirobat
- mirobat/microbat_instrumentator
- mirobat/microbat_junit_test
- mirobat/mutation
- mirobat/sav.commons
- mirobat/experiment.utils
- tregression/tregression
- ConSumSlice

![](/img/structure.png)

2. Please unzip the junit_lib ("ConSumSlice/lib/junit_lib.zip") under the dropins directory of your eclipse root folder. It contains all the runtime Java libraries required for running microbat and tregression:
````yaml
$path-to-eclipse_root_folder\dropins\junit_lib.
````
For example,
````yaml
/path-to/Eclipse.app/Contents/Eclipse/dropins
````

---
---
## Running the Tool with Main() method in Run
Now, you can run ConSumSlice through the main method in the run class (run as "Java Application"):

![](/img/run.png)

The main method takes as input following arguments: 
- the path to the base folder, including two versions (See below for our subject and Defects4J). 
- The benchmark name to run: ConSumSlice, Math, Closure, ....
- The bug_id
- The failing test

---

### Running on Our Subjects
As running the client and library projects needs merging two projects in one and create a merged jar to run Slicer4J, we provide the merged and ready to run folders in a Google Drive folder (https://drive.google.com/file/d/1XZ_lJG7cgMJvOSvlURCJgSG3Hu-cFvWM/view?usp=share_link):
The structure of ConSumSlice should be as follows:

|__ ConSumSlice<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|__ 1 (bug_id: jettison-xstream)<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|__ 2   <br /> 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|__ ...<br />

Here is an example of running bug_id 6 of ConSumSlice subjects:

![](/img/arg.png)

Where, the base folder storing the ConSumSlice subjects is "/Documents/Projects/defects4j/bug_repos/". 
"ConSumSlice" is the name of the benchmark to run. 
Bug_id is 6 and the failing test is "com.intuit.wasabi.export.rest.impl.DefaultRestEndPointTest::testGetRestEndPointURI"

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


---