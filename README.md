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

### Labs using iverilog and gtkwave:
Design files and the corresponding testbench files are inside the Verilog_files directory.
**Command:** iverilog <design name *.v file> <associated test_bench tb_*.v>
**Output:** a.out file
When we execute the output file, vcd file gets dumped. File format: tb_<design_name>.vcd
This vcd file needs to be loaded in the simulator.
gtkwave <vcd file>
Uut: unit under test

---

### Introduction to YOSYS:
**Synthesizer:** Tool used for converting the RTL to netlist
Yosys is the synthesizer tool.
<img width="661" height="354" alt="image" src="https://github.com/user-attachments/assets/218cb562-10bc-4d41-8be2-edc43a6a2cdf" />

Verify the Synthesis output:

<img width="623" height="354" alt="image" src="https://github.com/user-attachments/assets/eac2697a-69ec-4398-ace5-36b9c7ac59f4" />

---

**Logic Synthesis:**

RTL Design:

* It is the behavioural representation of the required specification:

<img width="460" height="266" alt="image" src="https://github.com/user-attachments/assets/eb16588d-1135-4929-a513-bd578372b2c4" />

- **RTL Code → Digital Logic Circuit**
  - This transformation is done during **synthesis**.
- **RTL → Gate-Level Translation**
  - The result of this translation is called a **netlist** (written-out file).


<img width="1083" height="809" alt="image" src="https://github.com/user-attachments/assets/ee54ab67-03bd-4760-b823-493a1872adec" />

<img width="1100" height="760" alt="image" src="https://github.com/user-attachments/assets/df7bfd6b-ca05-4cab-a209-04cf73ba92c8" />

<img width="1098" height="789" alt="image" src="https://github.com/user-attachments/assets/dcc7b89b-662a-4d5d-ae28-ef5fc58d460f" />

<img width="1096" height="790" alt="image" src="https://github.com/user-attachments/assets/b2692463-4166-42ef-9851-156f842d8f30" />

<img width="1081" height="810" alt="image" src="https://github.com/user-attachments/assets/cd122141-fc44-4bb0-8116-53c6a321b9ce" />

<img width="1050" height="788" alt="image" src="https://github.com/user-attachments/assets/64c19244-d5ec-4cbd-84eb-bd49f68e12bb" />

The current carrying capability of a transistor is a function of its width. Wider transistor, low delay, more power, more area.
## Setup Time and Hold Time

### 🔹 Setup Time

- **Definition**:  
  The minimum time interval that the input data (`D`) must be stable and valid **before** the active edge (rising or falling) of the clock signal.

- **Purpose**:  
  Ensures the input data is available and stable long enough for the flip-flop to reliably latch it when the clock edge arrives.

- **Violation**:  
  If the input data changes too close to the clock edge (within the setup time), the flip-flop might not capture the intended value, potentially leading to incorrect operation.

---

### 🔹 Hold Time

- **Definition**:  
  The minimum time interval that the input data (`D`) must be stable and valid **after** the active edge of the clock signal.

- **Purpose**:  
  Ensures the input data remains stable long enough after the clock edge to allow the flip-flop to properly latch the data before it changes.

- **Violation**:  
  If the input data changes too soon after the clock edge (within the hold time), the flip-flop might not latch the intended value.
