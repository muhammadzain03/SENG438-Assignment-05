**SENG 438 - Software Testing, Reliability, and Quality**

> **Assignment #5**
> **Software Reliability Assessment**
  Instructor: 
>   -   Dr. Kangsoo Kim (kangsoo.kim@ucalgary.ca)

> Department of Electrical and Computer Engineering
> University of Calgary

Due Date: Check D2L for the submission deadline.

> **Summary:**
> - Install a reliability assessment (reliability growth and reliability demonstration chart) tool.
> - Run the tool and feed the provided data into it.
> - Display and discuss the results.

# 1 INTRODUCTION

This lab includes analysis of integration test data using reliability assessment tools. There are two ways to assess failure data:

1. Reliability growth testing
2. Reliability assessment using Reliability Demonstration Chart (RDC)

Both will be practiced in this lab.

# 2 PART 1: RELIABILITY GROWTH TESTING

## 2.1 OBJECTIVES

The purpose of this assignment is to give students hands-on experience on assessing the reliability of a hypothetical system given its failure data collected during integration testing. To do this, students will need to install a reliability growth assessment tool, such as C-SFRAT, and create plots of the failure rate and reliability of the SUT.

After completing this part, students will:

- gain an understanding of what reliability growth testing is and why it is useful.
- be able to measure the failure rate, MTTF, and reliability of the SUT through analyzing the test data.
- become familiar with the features and usage of a reliability growth testing tool.

## 2.2 TESTING TOOLS

The testing tool to be used in this part is 
- C-SFRAT (an open source software developed in Python). 

## 2.3 SYSTEM UNDER TEST

The system to be tested for this part is a hypothetical system and its failure data is attached ([failure-data-set2.zip](./failure-data-set2.zip)). There will be a few test data files and students should select one of them.

**Note:**
- For this assignment, take a deeper look into the suitable sample input for the tools that you are supposed to use, since you need to **convert your selected input data** into a compatible input file based on the used tool.

---

### 🔧 Example: Data Preparation for C-SFRAT (To Include in Report)

#### Data Preparation

The provided datasets are in the form of raw failure logs containing information such as failure time, severity, and descriptions. However, C-SFRAT requires interval-based input data. Therefore, preprocessing is required before performing the analysis.

The required input format for C-SFRAT is:

- **T**: time interval index  
- **FC**: number of failures in the interval  
- **E**: execution effort (hours)  
- **F**: failure identification effort (person-hours)  
- **C**: computer-based effort (hours)  

---

#### Conversion Method (Step-by-Step)

We demonstrate the conversion using `Failure Report 1.docx`.


### Step 1: Extract Failure Times

From the report, extract only the **Time (min)** values:

```
8, 8, 8, 8,
40, 40, 40,
48,
56,
80, 80, 80, 80, 80, 80, 80,
112,
120,
136, 136,
176,
192, 192,
208,
240, 240,
248,
272, 272,
288,
296,
320,
336,
352,
368,
392,
416,
440,
448,
528,
640,
712
````



### Step 2: Define Time Intervals (1 hour = 60 min)

We divide time into **1-hour intervals**:

| Interval (T) | Time Range (min) |
|-------------|------------------|
| 1 | 0–60 |
| 2 | 60–120 |
| 3 | 120–180 |
| 4 | 180–240 |
| 5 | 240–300 |
| 6 | 300–360 |
| 7 | 360–420 |
| 8 | 420–480 |
| 9 | 480–540 |
| 10 | 540–600 |
| 11 | 600–660 |
| 12 | 660–720 |


### Step 3: Assign Each Failure to an Interval

We now group each failure time into its corresponding interval:

- **0–60** → 8, 8, 8, 8, 40, 40, 40, 48, 56 → **9 failures**
- **60–120** → 80, 80, 80, 80, 80, 80, 80, 112 → **8 failures**
- **120–180** → 120, 136, 136, 176 → **4 failures**
- **180–240** → 192, 192, 208, 240, 240 → **5 failures**
- **240–300** → 248, 272, 272, 288, 296 → **5 failures**
- **300–360** → 320, 336, 352 → **3 failures**
- **360–420** → 368, 392, 416 → **3 failures**
- **420–480** → 440, 448 → **2 failures**
- **480–540** → 528 → **1 failure**
- **540–600** → (none) → **0 failures**
- **600–660** → 640 → **1 failure**
- **660–720** → 712 → **1 failure**



### Step 4: Compute FC (Failure Count)

| T | FC |
|---|----|
| 1 | 9 |
| 2 | 8 |
| 3 | 4 |
| 4 | 5 |
| 5 | 5 |
| 6 | 3 |
| 7 | 3 |
| 8 | 2 |
| 9 | 1 |
| 10 | 0 |
| 11 | 1 |
| 12 | 1 |


### Step 5: Assign Effort Variables

Since effort data is not provided:

- **E = 1** (1 hour per interval)  
- **F = 1**  
- **C = 1**  


### Final Processed Dataset

```csv
T,FC,E,F,C
1,9,1,1,1
2,8,1,1,1
3,4,1,1,1
4,5,1,1,1
5,5,1,1,1
6,3,1,1,1
7,3,1,1,1
8,2,1,1,1
9,1,1,1,1
10,0,1,1,1
11,1,1,1,1
12,1,1,1,1
````


### Remarks

* Only **failure times** are used; other fields (e.g., severity, description) are ignored.
* The dataset must be converted into intervals before using C-SFRAT.
* Effort variables are not provided and must be reasonably assumed.
* Clearly state and justify all assumptions in your report.


#### Additional Note on Effort Variables

Most datasets provided in this assignment do not include explicit effort variables.
Students are expected to recognize this limitation and apply reasonable assumptions (e.g., constant values).

For further understanding of how effort variables are used in practice, students may explore the example datasets included with C-SFRAT:

```
..\C-SFRAT_win_v1-0 (2)\C-SFRAT\datasets
```

These datasets are intended **only for reference and exploration**, and do not replace the requirement to preprocess the provided failure data.



## 2.4 FAMILIARIZATION


### 2.4.1: INSTALL C-SFRAT (Only for Windows-OS)

1. Get C-SFRAT binary from [GitHub](https://github.com/LanceFiondella/C-SFRAT/releases/tag/v1.0). There are a Windows and a Linux executable. Download and unzip the appropriate version on your system.
2. Run and verify its functionalities.


## 2.5  **INSTRUCTIONS**

### 2.5.1 Running C-SFRAT
1. Run C-SFRAT.exe for Windows  
2. Execute steps 2–6 as in Section 2.5.1.

For more information about the input format and features of the tool, you can read [A covariate software tool to guide test activity allocation](https://www.sciencedirect.com/science/article/pii/S2352711021001588)

![](./media/c-sfrat.png)

**Note:** If none of the above mentioned tools work for you, try to find other tools that may work.

1. Software Defect Estimation Tool (SweET): [https://github.com/LanceFiondella/SwEET](https://github.com/LanceFiondella/SwEET)

2. Software Failure and Reliability Assessment Tool (SFRAT): [https://github.com/LanceFiondella/srt.core](https://github.com/LanceFiondella/srt.core)

# 3 Part 2: ASSESSMENT USING RELIABILITY DEMONSTRATION CHART

## 3.1 OBJECTIVES

Reliability Demonstration Chart (RDC) is an efficient way of checking whether the target failure rate or MTTF is met. It is based on collecting failure data at time points. The main objective of this part of the assignment is to familiarize students with the RDC tool and its usage during reliability assessment.

We usually use RDC when failure data is limited to a few failures, failure times are known, and we want to find out what the reliability trend of the system is.

After completing this part, students will:

- be able to decide upon adequacy of testing for a given MTTF of the SUT through plotting the test data.
- become familiar with the features and usage of an RDC tool.

## 3.2 TESTING TOOLS

In this assignment, you will use the following tools to analyze the test data provided.

-  RDC-11 (an EXCEL worksheet and macro).
  
## 3.3 SYSTEM UNDER TEST

The system to be tested for this part is a hypothetical system and its failure data is attached ([failure-data-set2.zip](./failure-data-set2.zip)). There will be a few test data files and the students should select one of them.

## 3.4 FAMILIARIZATION

### 3.4.1 INSTALL RDC (**Suggestion**)

1. Get Reliability-Demonstration-Chart.xls and its manual RDC-xls-Overview.pdf for the attachment OR download it from the [Sourceforge.net](https://sourceforge.net/projects/rdc/).
2. Open the Excel sheet and verify that it works by setting various risk factors, i.e. check whether the right chart will be generated.
3. Read the document explaining its functionality.

![](install-rdc.png) 


**INSTRUCTIONS**

1. Make yourself familiar with the RDC. Try to understand how it works. Vertical axis is failure number (n), horizontal axis is normalized failure data (Tn), i.e., failure time divided by MTTF.
1. How to use RDC? You need to input the failure data (failure number and failure time); identify the target MTTF and anticipated confidence levels; and draw the failure points on the graph and analyze the trend. Consult with the examples in the lecture slides and RDC manual.
1. You can experiment with &quot;what-if&quot; scenarios by setting various values for MTTF and draw the plot.
1. Select the minimum MTTF (MTTF_min) for which the SUT becomes acceptable. Set MTTF to twice and half MTTFmin and plot the failure data.
1. Document the results at the end of your report file.

# 4 Submission

Submit the results for part 1 and part 2.

1. Document the results (plot/diagrams as well as explanation of each).
2. Compare the results of Part 1 and Part 2 and justify the case that each technique can be used.

# 5 Evaluation Criteria:

## 5.1 Demo (15%)

The objectives for the demo are a) Preparing you for technical presentations, b) an early assessment of your work to give you a second chance to submit a high-quality report, and c) making sure everybody in the team contributes evenly.

It is mandatory for all team members to attend the demo session and explain to the TAs in the lab what they have done for this assignment. For this particular assignment, you are expected to almost finish the assignment by the lab hour. All the team members should attend the lab. The TAs will go through the groups and each group must demonstrate the results of each part of the assignment.


**NOTE: Student who miss the demo session or are unable to demo what is detailed above are considered as less- contributors and may lose up to the entire assignment's mark.**

## 5.2 Lab report (85%)

Students will be required to submit a report on their work in the lab as a group. To be consistent, please use the template file “Assignment5-ReportTemplate.md”. If desired, feel free to rename the sections, as long as the headings are still descriptive and accurate.



A portion of the grade for the lab report will be allocated to organization and clarity. The report marking scheme is as follows:

|                                                                                                          |     |
| -------------------------------------------------------------------------------------------------------- | --- |
| **Reliability Growth Testing (40)**                                                                      |     |
| Result of model comparison (selecting top two models)                                                    | 5   |
| Result of range analysis (an explanation of which part of data is good for proceeding with the analysis) | 5   |
| Plots for failure rate and reliability of the SUT for the test data provided                             | 15  |
|                                                                                                          |     |
| A discussion on decision making given a target failure rate                                              | 10  |
|                                                                                                          |     |
| A discussion on the advantages and disadvantages of reliability growth analysis                          | 5   |
| **RDC Testing (30)**                                                                                     |     |
| 3 plots for MTTFmin, twice and half of it for your test data                                             | 15  |
| Explain your evaluation and justification of how you decide the MTTFmin                                  | 10  |
| A discussion on the advantages and disadvantages of RDC                                                  | 5   |
| **Other (15)**                                                                                           |     |
| Comparison of the results with the Part 1                                                                | 10  |
| A discussion on similarity and difference of the two techniques. Any lessons learned in this lab?        | 5   |
# 6 REFERENCES

1. Open Channel Foundation: [http://www.openchannelsoftware.org/discipline/Reliability_Analysis](http://www.openchannelsoftware.org/discipline/Reliability_Analysis)

2. ReliaSoft (commercial software): [http://www.reliasoft.com/products.htm](http://www.reliasoft.com/products.htm)
