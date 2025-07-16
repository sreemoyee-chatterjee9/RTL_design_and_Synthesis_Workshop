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

A cell in a standard cell library may be represented like this in Verilog.

<img width="464" height="521" alt="image" src="https://github.com/user-attachments/assets/f49c2f10-2853-48d5-9826-08606afc4998" />

<img width="1066" height="321" alt="image" src="https://github.com/user-attachments/assets/8e8c28a4-eb87-4928-8106-031c308ee1f0" />

### 🔹 Impact of Transistor Size on Performance and Power

Larger transistors offer faster switching speeds due to increased drive strength, but they also lead to **higher power consumption** and **increased delay** in some cases. This tradeoff is important in digital circuit design.

---

#### ⚡ Increased Drive Strength

- **Wider transistors** can drive more current.
- They **charge/discharge capacitive loads faster**, reducing gate delay.
- Beneficial for speeding up signal transitions.

---

#### ⚠️ Increased Capacitance

- Larger transistors have **higher gate capacitance**.
- This added capacitance must be **charged/discharged** during switching.
- Can **slow down preceding stages**, offsetting the speed advantage.

---

#### 🔋 Power Consumption

- **Dynamic Power** increases due to the need to switch higher capacitance.
  - More energy is required to toggle the gate.
- **Leakage Power** also rises as wider transistors allow more **leakage current**, even in the off state.

---

#### 📌 Summary

- There's a **tradeoff** between speed and power.
- Wider transistors offer faster performance but at the cost of **higher energy consumption** and potential impact on **neighboring stages**.

<img width="1205" height="507" alt="image" src="https://github.com/user-attachments/assets/a7d3c07d-3dc2-4a92-aa87-e83982e75350" />

### 🔹 Hierarchical and Flat Synthesis

<img width="696" height="246" alt="image" src="https://github.com/user-attachments/assets/315add08-c9bd-4c31-849f-3bf9c24007e5" />
<img width="440" height="354" alt="image" src="https://github.com/user-attachments/assets/44f5cca0-be29-492f-9202-1d196ce67675" />
<img width="748" height="329" alt="image" src="https://github.com/user-attachments/assets/0756e80e-8f7b-4754-977d-6733220a9eef" />
<img width="408" height="996" alt="image" src="https://github.com/user-attachments/assets/ffc891c5-4451-4e9c-ab26-f6ce3a1e8283" />
<img width="628" height="44" alt="image" src="https://github.com/user-attachments/assets/61b00a35-62bf-4484-9e69-589e42962605" />
<img width="296" height="39" alt="image" src="https://github.com/user-attachments/assets/e2c2c579-67f1-4159-aef7-a14501ef6f53" />
### Hierarchical Design:
<img width="1205" height="265" alt="image" src="https://github.com/user-attachments/assets/a540489f-f76a-43a2-8d3f-b1eacc0033b0" />
<img width="553" height="238" alt="image" src="https://github.com/user-attachments/assets/d343f28d-18b5-490c-8cab-9f37d4577a15" />
<img width="389" height="1016" alt="image" src="https://github.com/user-attachments/assets/1522e6a6-2756-495f-a139-4dcde0fa054f" />
- **Hierarchical Synthesis**:
  ➤ Hierarchies are **preserved** during synthesis.
  ➤ Useful for managing large designs in a modular way.

- **Flat Synthesis**:
  ➤ All module hierarchies are **flattened** into a single-level netlist.
  ➤ The synthesis tool **may implement NAND gates** instead of AND gates with stacked PMOS transistors.
  ➤ This is because **stacked PMOS is avoided** due to its **poor mobility**.

- **Command to Flatten Hierarchy**:
    flatten

<img width="531" height="271" alt="image" src="https://github.com/user-attachments/assets/c39b6c33-d14e-415e-89f2-bcc599113434" />
<img width="759" height="773" alt="image" src="https://github.com/user-attachments/assets/9d4cc285-97fc-4167-9fa1-73e31d115a9b" />
<img width="1205" height="172" alt="image" src="https://github.com/user-attachments/assets/2f38dfab-4be6-4daa-aff4-86ae3a2913c2" />

- **Flat Synthesis**:
  ➤ All module hierarchies are **flattened** into a single-level netlist.
  ➤ The synthesis tool **may implement NAND gates** instead of AND gates with stacked PMOS transistors.
  ➤ This is because **stacked PMOS is avoided** due to its **poor mobility**.
  ➤ **Whole structure = whole netlist**: The entire design is synthesized as one unified block.


<img width="709" height="1050" alt="image" src="https://github.com/user-attachments/assets/846d7b87-641c-4524-9823-3198d362f63a" />
<img width="333" height="35" alt="image" src="https://github.com/user-attachments/assets/f5d710c2-354e-4f37-a2b8-3a21a201067d" />
<img width="451" height="338" alt="image" src="https://github.com/user-attachments/assets/b03f3c8d-5d0b-40c6-8d57-38e272d953d0" />
### Synthesize at sub_module1 Level
<img width="750" height="175" alt="image" src="https://github.com/user-attachments/assets/7b201656-c172-4bd9-90c3-a94289e09b24" />

### 🔹 Why Perform Submodule-Level Synthesis?

There are specific benefits to synthesizing submodules separately rather than synthesizing the entire design in one go.

### 🔹 Why Perform Submodule-Level Synthesis?

There are specific benefits to synthesizing submodules separately rather than synthesizing the entire design in one go.

- ✅ **Reuse of Synthesized Modules**  
  - ➤ If the same module (e.g., a multiplier) is instantiated multiple times, we can **synthesize it once**, generate the netlist, and **replicate it** as needed.  
  - ➤ Example: Instead of synthesizing the multiplier **6 times**, synthesize it once and stitch it into the top module **6 times**, saving significant time and effort.

- ✅ **Preferred for Repeated Modules**  
  - ➤ Efficient when there are **multiple instances of the same logic block** in a design.

- ✅ **Divide and Conquer Approach**  
  - ➤ For **massive designs**, it's better to break them into smaller parts.  
  - ➤ Each submodule is synthesized separately with **tool-level optimization**, producing an efficient netlist.  
  - ➤ Then, these are **stitched together** at the top-level for a final optimized netlist.
  - Command : synth -top <top_module>

<img width="423" height="241" alt="image" src="https://github.com/user-attachments/assets/cbddc94b-342f-424a-aa6e-5571ef00c654" />


### 🔹 How to Code a Flip-Flop (Flop)

#### 🧠 Why Do We Use Flops?

- Combinational circuits can produce **glitches** due to changes in inputs arriving at **slightly different times**.
- The output of a combinational circuit changes **immediately**, and may toggle unpredictably before settling—this causes glitches.
- The more the **combinational depth**, the more the chances of glitches.
- Continuous toggling or glitching at outputs can make circuits **unreliable** or **power-hungry**.

#### ✅ Role of Flops:

- **Flip-flops** store the signal value and **isolate logic stages**.
- Output (`Q`) changes **only on a clock edge**, making it **stable** and free from glitches caused by intermediate logic.
- Flip-flops **shield `Q` from changes in `D`** between clock edges.
- This provides a **clean timing boundary** and helps in **timing closure**.

#### 🔁 Reset and Set:

- Flops can be initialized using **reset** or **set** signals.
- These signals can be:
  - **Synchronous**: Triggered with the clock.
  - **Asynchronous**: Triggered independent of the clock (immediate action).

---

<img width="586" height="443" alt="image" src="https://github.com/user-attachments/assets/ab739e0f-5c87-45b2-b8ab-9400e48fdb71" />

### Positive asynchronous reset D Flip Flop [irrespective of clock]:

<img width="733" height="160" alt="image" src="https://github.com/user-attachments/assets/2abfead3-4a50-47c6-818d-a3148fe334cb" />

### Positive asynchronous set D Flip Flop [irrespective of clock]:

<img width="703" height="159" alt="image" src="https://github.com/user-attachments/assets/630c05c2-c292-45ad-b66a-0e30d8e38543" />

### Synchronous Reset D Flip Flop:

<img width="860" height="173" alt="image" src="https://github.com/user-attachments/assets/8e27075e-351c-44f0-b863-f6d2e514e7b0" />

<img width="386" height="531" alt="image" src="https://github.com/user-attachments/assets/798753fc-b7f1-468f-b2e8-773bd07f579e" />

### Asynchronous Reset:

<img width="1153" height="215" alt="image" src="https://github.com/user-attachments/assets/dc735df9-57a0-4e5a-92f5-538479c711e6" />

<img width="1205" height="139" alt="image" src="https://github.com/user-attachments/assets/87116fed-ef98-4c04-a617-9c1bf9769631" />

### Asynchronous Set:

<img width="1181" height="221" alt="image" src="https://github.com/user-attachments/assets/135751b0-9e42-40d8-8c10-a3b1c4db4416" />

<img width="1205" height="118" alt="image" src="https://github.com/user-attachments/assets/93282acf-76f2-4ce7-902e-be43c65751a3" />

### Synchronous Reset:

<img width="1126" height="114" alt="image" src="https://github.com/user-attachments/assets/27483f57-9b47-4cad-893b-8a8391258d64" />

<img width="1205" height="131" alt="image" src="https://github.com/user-attachments/assets/0ce71351-a81e-44e1-bdd0-865936b2cde2" />

Sync reset is higher priority that D as D is in the else portion.

### Synthesize these sync/async set/reset designs:

<img width="865" height="478" alt="image" src="https://github.com/user-attachments/assets/3f661a3b-c792-45f6-861b-cb567c94580d" />

<img width="451" height="296" alt="image" src="https://github.com/user-attachments/assets/8c83a853-3f00-4200-8f3f-9a7fdf591ae6" />

<img width="706" height="40" alt="image" src="https://github.com/user-attachments/assets/b21c1672-b9bc-44c3-a364-1142fb38f961" />

<img width="1084" height="658" alt="image" src="https://github.com/user-attachments/assets/9896980b-652f-43fc-9212-374523d841b5" />

<img width="621" height="40" alt="image" src="https://github.com/user-attachments/assets/8bc59736-f5c3-42be-bf54-f763d7e87d34" />

<img width="584" height="139" alt="image" src="https://github.com/user-attachments/assets/fbb82dfc-db45-46c0-913d-e5c983a80fa8" />

<img width="1205" height="188" alt="image" src="https://github.com/user-attachments/assets/63fb6855-34ab-445e-aba1-ecc13e58ba9a" />

<img width="1205" height="194" alt="image" src="https://github.com/user-attachments/assets/d806e294-832b-490f-b04c-cf9e676d4e07" />

### Synchronous Reset:

<img width="1205" height="244" alt="image" src="https://github.com/user-attachments/assets/3ada6965-b66a-47b6-8c09-bf7fb943c55b" />

| Signal | Meaning        |
|--------|----------------|
| B_N    | Inverted B     |

### OPTIMIZATION:
<img width="530" height="471" alt="image" src="https://github.com/user-attachments/assets/211a04d9-c2f3-4bc5-929d-8d56dd9b41d5" />

<img width="435" height="59" alt="image" src="https://github.com/user-attachments/assets/28fb9caf-4686-47b6-9354-d11a43050765" />

<img width="731" height="289" alt="image" src="https://github.com/user-attachments/assets/942fb653-1df0-4e9c-b168-ef962c6ce856" />

<img width="575" height="177" alt="image" src="https://github.com/user-attachments/assets/2ffcaa36-e0b1-49b6-b636-e2011701737a" />
