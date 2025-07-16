# RTL_design_and_Synthesis_Workshop

## 📘 Index

- [Day 1: Introduction](#day-1-introduction)
- [Day 2: Coming Soon](#day-2-coming-soon)
- [Day 3: Coming Soon](#day-3-coming-soon)

---

## Day 1: Introduction

### What is a simulator?

- A **simulator** is a tool for checking the design. RTL Design is an implementation of a spec. The intent of the spec needs to be verified by simulating the design.
  -  Simulator is a software tool used to verify the functionality of a digital circuit described in Verilog code. It executes the Verilog code and simulates the behavior of the circuit based on input stimuli, allowing designers to identify potential errors before physical implementation. This helps in debugging and ensuring the design meets its specifications. 
- **Tool**: iVerilog  
- **Design**: A set of Verilog code that meets the specifications.

### What is a testbench?

- To check whether the design follows specifications, we apply **stimulus** and observe the **output**.
- This stimulus (test vectors) helps verify the expected behavior.
- Testbenches generate input signals (stimuli) to drive the inputs of the DUT.
- By providing a controlled environment and allowing inspection of internal signals, testbenches help in identifying and debugging design errors.
- Testbenches are crucial for verifying the correctness of hardware designs before they are manufactured as ASICs or implemented on FPGAs. 

### How a Simulator Works:

1. Simulator looks for **changes in the input signals**.
2. Upon input change, the **output is evaluated**.
3. If **no change** in the input, there is **no change** in the output.
4. Simulator focuses on detecting value changes in the input.
<img width="730" height="354" alt="image" src="https://github.com/user-attachments/assets/e1b36b8e-129d-4e0e-9b66-99838af8ddab" />

---
### Conditions:

I. Design may have **one or more primary inputs**, and **one or more primary outputs**.  
II. Test Bench (TB) does **not** have a Primary Input or Primary Output.

---

### iVerilog Based Simulation Flow:
<img width="744" height="354" alt="image" src="https://github.com/user-attachments/assets/e39e14fa-b0ff-4c44-beb6-1f00186be3eb" />

