# RTL_design_and_Synthesis_Workshop

## 📘 Index

- [Day 1](#day-1-introduction)
- [Day 2](#day-2-timing-libs-hierarchical-vs-flat-synthesis-and-efficient-flop-coding-styles)
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

---

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

---

### 🔹 Propagation Delay

- **Definition**:  
  Propagation delay refers to the time it takes for a signal to travel from the **input** of a logic gate or circuit to its **output**, specifically when the output changes from one logic state to another.

- **Details**:  
  It is the delay between a change at the input and the corresponding change at the output.  
  This delay is typically **measured at the 50% voltage point** of the signal transition (i.e., when the signal crosses half of its full swing).


---

### 🔹 LAB

<img width="1129" height="815" alt="image" src="https://github.com/user-attachments/assets/6130a530-e30d-4026-8cfe-0d11d5282477" />

<img width="915" height="294" alt="image" src="https://github.com/user-attachments/assets/8de84654-87c6-4dd3-9bca-00e79c7859cc" />

<img width="648" height="153" alt="image" src="https://github.com/user-attachments/assets/2c0df8ea-49b7-474c-ad97-60ad39c7f43b" />

synth -top good_mux

<img width="634" height="433" alt="image" src="https://github.com/user-attachments/assets/75c83f6a-4f5c-4c02-8c8b-e5cfb6e05470" />

<img width="635" height="40" alt="image" src="https://github.com/user-attachments/assets/32a2a28a-26f6-4cb0-993a-accadff61ff3" />

<img width="708" height="189" alt="image" src="https://github.com/user-attachments/assets/d7d3f9d3-a51b-4fb8-98b9-e5e13da919e0" />

<img width="1205" height="391" alt="image" src="https://github.com/user-attachments/assets/65e53f5f-7287-4bdc-879e-7df55a11f113" />

<img width="421" height="178" alt="image" src="https://github.com/user-attachments/assets/38ae491c-5e3c-4a81-91ac-a1dfba6de77e" />

<img width="1003" height="784" alt="image" src="https://github.com/user-attachments/assets/84cf496d-60c6-4a03-a131-bec158fbd77b" />

<img width="559" height="183" alt="image" src="https://github.com/user-attachments/assets/008f5c15-a5a5-4e62-b5dd-0fccec05001f" />

<img width="1063" height="575" alt="image" src="https://github.com/user-attachments/assets/56ff0128-3454-421d-8f2e-e6f632aff62e" />


## Day 2: Timing libs, hierarchical vs flat synthesis and efficient flop coding styles

### What is a .lib?

- .lib is collection of our standard cells. It contains slow cells and fast cells.
- It defines the timing, power, and area characteristics of these cells, enabling accurate timing analysis and synthesis during the chip design process. 
<img width="596" height="121" alt="image" src="https://github.com/user-attachments/assets/d6fa9c14-5daf-4f20-b6db-cbda16702190" />

### 🔹 PVT Corners and Library Characterization

- `tt` → Typical process corner  
- `025c` → Temperature (25°C)  
- `1v8` → Indicates voltage (1.8V)

- **PVT** stands for **Process, Voltage, Temperature**
  - **Process** → Variation due to fabrication
  - **Voltage** → Variation due to supply voltage
  - **Temperature** → Variation due to thermal conditions

These factors determine how the silicon will behave in different conditions.  
Our **timing libraries** are characterized to model these **PVT variations** to ensure correct functionality across all expected conditions.
<img width="435" height="145" alt="image" src="https://github.com/user-attachments/assets/c2078695-09d6-44c4-a8b1-fffe382d87b7" />
<img width="363" height="96" alt="image" src="https://github.com/user-attachments/assets/df620a1b-994c-4d9f-8022-de35140e8be0" />
<img width="310" height="131" alt="image" src="https://github.com/user-attachments/assets/dfc6fa0e-dc29-4b90-8b17-6733bb42f2d1" />

### 🔹 Cell Flavours and Power Ports in Verilog

- Different **flavours of cells** may exist in the library (e.g., low-power, high-speed variants)
- **PP** stands for **Power Ports**

---

### 📦 Module Definition of a Cell in Verilog Models

A cell in a standard cell library may be represented like this in Verilog:

```verilog
module AND2_X1 (
  output Y,
  input A,
  input B,
  input VDD,  // Power Port
  input VSS   // Ground
);
  assign Y = A & B;
endmodule












