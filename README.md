# RTL_design_and_Synthesis_Workshop
# Verilog Simulator Guide

## 📘 Index

- [Day 1: Introduction](#day-1-introduction)
- [Day 2: Coming Soon](#day-2-coming-soon)
- [Day 3: Coming Soon](#day-3-coming-soon)

---

## Day 1: Introduction

### What is a simulator?

- A **simulator** is a tool for checking the design. RTL Design is an implementation of a spec. The intent of the spec needs to be verified by simulating the design.  
- **Tool**: iVerilog  
- **Design**: A set of Verilog code that meets the specifications.

### What is a testbench?

- To check whether the design follows specifications, we apply **stimulus** and observe the **output**.
- This stimulus (test vectors) helps verify the expected behavior.

### How a Simulator Works:

1. Simulator looks for **changes in the input signals**.
2. Upon input change, the **output is evaluated**.
3. If **no change** in the input, there is **no change** in the output.
4. Simulator focuses on detecting value changes in the input.

---
