# SENG 438 – Assignment 5: Software Reliability Assessment

**Course:** SENG 438 - Software Testing, Reliability, and Quality  
**Group:** 08

| Group \#:              |  08 |
| ---------------------- | --- |
| Student Names:         |     |
| Yazin Abdul Majid      |     |
| Muhammad Zain          |     |
| Fateh Ali Syed Bukhari |     |

---

## Overview

This assignment focuses on **Software Reliability Assessment** using two complementary techniques:

1. **Reliability Growth Testing** — using C-SFRAT to model failure data, compare reliability growth models, and plot failure rate and reliability over time.
2. **Reliability Demonstration Chart (RDC)** — using RDC-11 (Excel) to assess whether the SUT meets a target MTTF under given confidence levels.

The system under test is a hypothetical system whose integration test failure data is provided in the `Failure_Data_Set/` folder.

---

## Guideline

- Read the [assignment guideline](SENG438-A5-Instructions.md)
- Commit and push output on **Github** ([assignment report](SENG438-A5-Group08.md))

---

## Repository Structure

```
Assignment 05/
├── SENG438-A5-Group08.md          ← Lab report (Group 08)
├── SENG438-A5-Instructions.md     ← Official assignment instructions
├── README.md                      ← This file
│
└── Failure_Data_Set/              ← Provided failure data
    ├── Failure_Count/             ← Failure count data files (J1–J5.DAT)
    └── Time_Between_Failures/     ← Time-between-failures data files
```

---

## Tools Used

| Tool | Purpose |
|------|---------|
| **C-SFRAT** | Reliability growth testing — model fitting, failure rate and reliability plots |
| **RDC-11 (Excel)** | Reliability Demonstration Chart — MTTF assessment |
