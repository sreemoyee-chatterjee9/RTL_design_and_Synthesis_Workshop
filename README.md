# RTL_design_and_Synthesis_Workshop

## 📘 Index

- [Day 1: Introduction](#day-1-introduction)
- [Day 2: Timing libs, hierarchical vs flat synthesis and efficient flop coding styles](#day-2-timing-libs-hierarchical-vs-flat-synthesis-and-efficient-flop-coding-styles)
- [Day 3: Combinational and Sequential Logic Optimization](#day-3-combinational-and-sequential-logic-optimization)
- [Day 4: Gate Level Simulation (GLS)](#day-4-gate-level-simulation-gls)
- [Day 5: IF-CASE Constructs](#day-5-if-case-constructs)
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

<img width="363" height="289" alt="image" src="https://github.com/user-attachments/assets/1260500a-7cfe-46dd-8c6a-8292a70cd73a" />

<img width="256" height="158" alt="image" src="https://github.com/user-attachments/assets/27a940ef-92e2-4f8a-843c-2fec1c6c8c8e" />

<img width="865" height="207" alt="image" src="https://github.com/user-attachments/assets/88432db6-3579-48dd-b2cb-9756dfa4073a" />

<img width="613" height="228" alt="image" src="https://github.com/user-attachments/assets/36264117-c7d9-4df4-a3f3-befe912ef5e2" />

As no standard cells are there, there is no need of abc -liberty

<img width="746" height="179" alt="image" src="https://github.com/user-attachments/assets/a285d6dd-9d22-4294-8738-dccf476683de" />

<img width="196" height="120" alt="image" src="https://github.com/user-attachments/assets/fc65edc6-322f-4c4b-9a0b-4a75ce02215c" />

---

## Day 3: Combinational Logic Optimization

### 🔹 Why Optimization?

- To **squeeze** the logic to its most **efficient** and **optimized** form.
- Main goals:
  - ✅ **Area savings** (reduce gate count, layout area)
  - ✅ **Power savings** (lower switching activity and capacitance)

---

### 🔧 Optimization Techniques

#### 🔸 Technique 1: Constant Propagation

- Basic direct optimization.
- Replaces expressions where constants are involved.
- Example:
  ```verilog
  assign y = a & 1'b0;  // Can be reduced to y = 1'b0

#### 🔸 Technique 2: Boolean Logic Optimization

- Optimize large and complex Boolean expressions to reduce logic depth and gate count.

  - 🧮 **K-Map (Karnaugh Map)**  
    - Visual method for simplifying Boolean expressions (up to 5-6 variables).  
    - Great for manual simplification.

  - 🧠 **Quine–McCluskey Algorithm**  
    - Tabular method ideal for automated tools.  
    - Systematic and programmable.

---
<img width="1205" height="611" alt="image" src="https://github.com/user-attachments/assets/a9467e06-433a-490e-9e1a-f8964958a250" />

### Boolean Optimization:

<img width="1005" height="673" alt="image" src="https://github.com/user-attachments/assets/dc60dcef-1922-4621-8c4f-66842fbfc183" />

---

### 🔧 Why Sequential Logic Optimization?

Sequential logic circuits include memory elements (like flip-flops). Optimizing them improves **performance**, **area**, and **power consumption** in clocked designs.

---

### 🔹 Techniques

#### 🔸 Technique 1: Sequential Constant Propagation

- Identifies and removes unused or constant flip-flop outputs.
- Similar to combinational constant propagation, but across clock cycles.

#### 🔸 Technique 2: Advanced Techniques

- 🧠 **State Optimization**
  - Reduces the number of states in FSMs (Finite State Machines).
  - Combines equivalent or redundant states to minimize logic.

- ⏱️ **Retiming**
  - Moves flip-flops across combinational logic to optimize timing (reduce critical path).
  - Can help balance pipeline stages.

- 🧬 **Sequential Logic Cloning**
  - Duplicates logic for performance improvement.
  - Used to break timing bottlenecks by replicating logic paths.

<img width="954" height="1417" alt="image" src="https://github.com/user-attachments/assets/04818ec6-86d3-467c-bd97-cd0facde0262" />

> 💡 **Note:**  
> Not every flop with a `D` input tied off is considered a sequential constant propagation case.  
> For it to qualify, the `Q` output must always resolve to a **constant value** across all clock cycles.

| **Technique**              | **Description**                                                                 |
|---------------------------|---------------------------------------------------------------------------------|
| **State Optimization**     | - Optimization of unused states<br>- Realization of most condensed state machines<br>- Use of states |
| **Retiming**               | - Technique to improve the performance of the circuit.<br>- Utilizing the useful slack to get the benefit of performance. |
| **Sequential Logic Cloning** | - Physical aware synthesis |

#### 🔸 Technique 2: Advanced Techniques

- 🧠 **State Optimization**
  - Optimizes unused or unreachable states.
  - Results in **condensed**, **efficient** finite state machines (FSMs).
  - Ensures only **useful states** are realized in hardware.

- ⏱️ **Retiming**
  - Technique used to **improve circuit performance**.
  - Involves shifting flip-flops across logic to reduce the **critical path**.
  - Utilizes **available slack** effectively for better timing closure.

- 🧬 **Sequential Logic Cloning**
  - Performance-focused optimization done during **physically aware synthesis**.
  - Duplicates logic to reduce fanout and **relieve timing pressure** on critical paths.
  - Helps with placement-driven improvements during implementation.
 
<img width="771" height="709" alt="image" src="https://github.com/user-attachments/assets/6f7a1f6e-78b3-459e-9c83-e47ef5086b8f" />
<img width="560" height="709" alt="image" src="https://github.com/user-attachments/assets/0b639bc2-632c-473b-b627-63df8f1663dd" />

---

### LAB: Combinational Logic Optimisations: 

### CASE I 

<img width="731" height="214" alt="image" src="https://github.com/user-attachments/assets/a02ada25-70b8-40cd-b7b7-462b50ad8597" />

So, with the Boolean Optimization we are expecting this case to be optimized into a two input AND Gate.
 
<img width="751" height="179" alt="image" src="https://github.com/user-attachments/assets/705cacf8-df1b-4e6f-b290-656598d9d5df" />


### CASE II :

<img width="444" height="71" alt="image" src="https://github.com/user-attachments/assets/56290275-3221-4542-95bc-b7c661a96a3e" />

<img width="132" height="83" alt="image" src="https://github.com/user-attachments/assets/903e2008-250a-4d5f-9126-ab96ceac9e17" />

<img width="381" height="303" alt="image" src="https://github.com/user-attachments/assets/012b1392-b958-4b16-bd2b-54071b56536b" />

<img width="198" height="270" alt="image" src="https://github.com/user-attachments/assets/5a30c644-b4f3-4f88-b5f8-684e5d9c32af" />

<img width="929" height="303" alt="image" src="https://github.com/user-attachments/assets/777476c2-5284-469d-9d5f-981441470165" />

<img width="640" height="191" alt="image" src="https://github.com/user-attachments/assets/2514b5e0-dc0f-4c4b-ab5e-0d8a52911850" />

<img width="660" height="153" alt="image" src="https://github.com/user-attachments/assets/de3bbe9f-6efe-4a68-9ef7-cef097316c58" />

<img width="748" height="184" alt="image" src="https://github.com/user-attachments/assets/1225a726-2df5-4032-9652-e3ca0b618012" />

(A’+B’)’ simplifies to A+B using DeMorgan's Law.


### CASE III:

<img width="523" height="78" alt="image" src="https://github.com/user-attachments/assets/7ebbfb47-b2b1-45d9-b54e-edf6e0f9744f" />

y = a ? (c ? b : 0) : 0

<img width="586" height="373" alt="image" src="https://github.com/user-attachments/assets/0fc2335f-6afd-4b48-8772-b6b568d401b9" />

<img width="240" height="158" alt="image" src="https://github.com/user-attachments/assets/ec6dc9a0-2595-4783-aa17-839637a6fba4" />

<img width="579" height="230" alt="image" src="https://github.com/user-attachments/assets/1be1473a-19f9-4afc-bccd-d89c0fcd06a0" />

<img width="537" height="124" alt="image" src="https://github.com/user-attachments/assets/68f47b18-b495-44e0-888a-1c25bf1323a4" />

<img width="709" height="237" alt="image" src="https://github.com/user-attachments/assets/2c99e55c-5563-4774-990f-8e636799a0b7" />


### CASE IV:

<img width="528" height="63" alt="image" src="https://github.com/user-attachments/assets/3cd5074c-c572-4e67-b626-dd43e779f638" />

<img width="192" height="125" alt="image" src="https://github.com/user-attachments/assets/717e540f-4f9c-407f-845b-02a6cfb11aad" />

<img width="574" height="189" alt="image" src="https://github.com/user-attachments/assets/19bfdc8e-ba99-4a89-bf4c-ec390f4f2247" />


### CASE V:

<img width="585" height="321" alt="image" src="https://github.com/user-attachments/assets/70dcbfaf-1e30-44ce-b6ac-266e80ae1f25" />

sub_module1 : y = a AND b
sub_module2 : y = a XOR b
U1 : n1 = a & b = a & 1 = a
U2 : n2 = n1 ^ b = a XOR b = a XOR 0 = a
U3 : n3 = b ^ d = b XOR d
y = c OR (b AND n1) = c OR ab

<img width="809" height="400" alt="image" src="https://github.com/user-attachments/assets/c091fc9b-dc68-484a-8641-bbcfb8857bc3" />

### CASE VI:

<img width="790" height="355" alt="image" src="https://github.com/user-attachments/assets/f86eff11-1110-4188-9252-ce3abab127ed" />

<img width="520" height="698" alt="image" src="https://github.com/user-attachments/assets/b0d18147-36c5-443c-afcc-25634094102f" />

---

### SEQUENTIAL OPTIMIZATION:

<img width="1205" height="351" alt="image" src="https://github.com/user-attachments/assets/c1fa54d5-080f-416a-a85f-58fd83f9b3bf" />

### 🔸 DFF_CONST1

<img width="591" height="278" alt="image" src="https://github.com/user-attachments/assets/ef4d1669-d1af-42d8-9232-48d70c93b86a" />

### 🔸 DFF_CONST2

<img width="591" height="271" alt="image" src="https://github.com/user-attachments/assets/8bb14587-4748-4bfb-bb47-eaaa257eea5c" />

<img width="1116" height="135" alt="image" src="https://github.com/user-attachments/assets/7aab17b0-b58f-41a1-9592-600c0600221c" />

<img width="1205" height="129" alt="image" src="https://github.com/user-attachments/assets/5f32897b-e8b4-47e2-8adb-2a51cdee59af" />

Q is waiting for the edge of the clock.

<img width="1115" height="114" alt="image" src="https://github.com/user-attachments/assets/5d76cb2e-e900-467e-a421-87bd3f79ce26" />

<img width="1205" height="85" alt="image" src="https://github.com/user-attachments/assets/eca98612-4d85-4775-b030-62118336615e" />

Q is “1” though out.
For Sequential circuits we need to tell the tool by using this command: 

<img width="663" height="29" alt="image" src="https://github.com/user-attachments/assets/4692986d-3215-4c13-824b-64caeefbed9d" />

<img width="434" height="291" alt="image" src="https://github.com/user-attachments/assets/54b475d7-8910-49ab-bb78-265ddd66cda8" />

<img width="1205" height="198" alt="image" src="https://github.com/user-attachments/assets/7d9b2673-bee2-40ba-aa2c-436fcd8c3597" />

We have programmed an active high reset, but library is expecting an active low reset. So, the inverter is there.

<img width="433" height="281" alt="image" src="https://github.com/user-attachments/assets/c7e90579-ae18-437e-a086-553f12243120" />

<img width="354" height="288" alt="image" src="https://github.com/user-attachments/assets/46b0a317-3a06-44f1-a4ec-6f98c8a8b80a" />

### 🔸 DFF_CONST3

<img width="498" height="304" alt="image" src="https://github.com/user-attachments/assets/1f54d0f5-873a-43bd-bacc-885948036fb8" />

<img width="608" height="509" alt="image" src="https://github.com/user-attachments/assets/cab30868-e457-49eb-8362-1789185a7a15" />

<img width="1205" height="124" alt="image" src="https://github.com/user-attachments/assets/1e76ccf3-0048-48f7-9b8d-e520ea6eb8fc" />

VCD: Value Change Dump File

<img width="1205" height="167" alt="image" src="https://github.com/user-attachments/assets/e94b836f-78a9-4d6f-9301-5d813b652152" />

<img width="413" height="321" alt="image" src="https://github.com/user-attachments/assets/b0151e1b-518d-423b-b463-b52ec9b0f2bd" />

<img width="1205" height="184" alt="image" src="https://github.com/user-attachments/assets/de9c443f-e391-4493-ab3f-c89f6823f85b" />

### 🔸 DFF_CONST4

<img width="498" height="296" alt="image" src="https://github.com/user-attachments/assets/ec30ab1d-b722-429e-80a5-ed83aabe69ac" />

<img width="1205" height="186" alt="image" src="https://github.com/user-attachments/assets/efd7f354-f508-4ef7-9ddd-a4666bb3610c" />

<img width="426" height="284" alt="image" src="https://github.com/user-attachments/assets/a0cccc0d-c6ab-46a3-a612-a9970c310afb" />

<img width="531" height="550" alt="image" src="https://github.com/user-attachments/assets/f48a3a78-a976-4f6d-943e-e3426576a752" />

Optimization done as Q values are constant.

### 🔸 DFF_CONST5

<img width="501" height="315" alt="image" src="https://github.com/user-attachments/assets/3bb9bcac-8dbb-44cb-8ed9-77f2ad5068ff" />

<img width="1205" height="114" alt="image" src="https://github.com/user-attachments/assets/df01fc03-c11b-4456-918c-7d3f5df4524c" />

<img width="434" height="295" alt="image" src="https://github.com/user-attachments/assets/f36eccb8-0273-443a-b8ca-4e3dc9f0219c" />

<img width="1205" height="178" alt="image" src="https://github.com/user-attachments/assets/f04d9d14-e98b-499d-a691-0d19e650f9a1" />

---

### Unused Output Optimization:

<img width="503" height="234" alt="image" src="https://github.com/user-attachments/assets/71d10106-1a40-46ee-9707-ffe77d4049b0" />

<img width="531" height="299" alt="image" src="https://github.com/user-attachments/assets/0895418d-b349-44c2-bf39-a22801a333b9" />

<img width="96" height="225" alt="image" src="https://github.com/user-attachments/assets/20dc9ef0-b4ba-4cfd-9cf2-9b1148c42c8a" />

<img width="408" height="321" alt="image" src="https://github.com/user-attachments/assets/3d1114af-c75e-4ab6-b545-9d338c3b45d8" />

<img width="531" height="301" alt="image" src="https://github.com/user-attachments/assets/2576daab-97fd-4173-afb4-27a2e3fd4f94" />

<img width="1205" height="156" alt="image" src="https://github.com/user-attachments/assets/b3d8fb18-6c55-412f-826d-635f9988f70a" />

<img width="496" height="216" alt="image" src="https://github.com/user-attachments/assets/e9c1970f-2386-4b73-9355-b2d7bb07cbd9" />

Using all 3bits of the counter now.

<img width="421" height="403" alt="image" src="https://github.com/user-attachments/assets/2eb06b59-d2ae-4f2a-ae92-d91293ddb4cd" />

<img width="1205" height="273" alt="image" src="https://github.com/user-attachments/assets/07261dc8-619c-46f8-974a-65bdbcafd1ed" />

<img width="887" height="302" alt="image" src="https://github.com/user-attachments/assets/878b63be-dc9e-4d7f-bab3-baaaaab239c9" />

---

## Day 4: Gate Level Simulation (GLS)

### 🔍 What is Gate Level Simulation?
- We validate the functionality of RTL code by testing it.
- We give stimulus to the RTL design and check if the outputs match specifications.
- This setup is called the **Testbench**.
- Initially, **RTL Code** is the DUT (Design Under Test), and the Testbench injects stimulus and observes the output.
- In GLS, we replace RTL with the **Netlist** as the DUT.
- A **Netlist** is the synthesized version of RTL using standard cell gates — logically equivalent to RTL.
- We run the testbench against the **Netlist** to validate correctness post-synthesis.

### ❓ Why do we need GLS?
- ✅ To check **logical correctness** after synthesis.
- ✅ To validate **timing** for complex designs after synthesis.
- ✅ GLS with **SDF annotation** (Standard Delay Format) helps simulate real gate/path delays:
  - Detects **setup and hold violations**
  - Identifies **race conditions** and **clock skew**
- ✅ Detects **glitches** (short-lived, incorrect signals), especially in edge-sensitive logic.


### 🧪 GLS using iVerilog
<img width="886" height="394" alt="image" src="https://github.com/user-attachments/assets/68b4a8d5-cc20-47a5-b226-da4033be16a8" />

<img width="886" height="550" alt="image" src="https://github.com/user-attachments/assets/c4ebeea8-57b6-4a2e-8aad-70213c99baa2" />

## 🛠️ Synthesis vs Simulation Mismatch

Sometimes, the synthesized netlist and simulated RTL behave differently due to certain coding issues. Common causes include:

### ⚠️ Causes of Mismatch:
- Missing sensitivity list
- Improper use of blocking (`=`) vs non-blocking (`<=`) assignments
- Non-standard Verilog coding practices

---

### 📌 Example: Missing Sensitivity List
- The simulator operates based on signal **activity**.
- If a signal is not included in the sensitivity list, the simulator won’t evaluate the block when that signal changes.
- 🔁 **No activity → No evaluation → Incorrect simulation results**

<img width="908" height="522" alt="image" src="https://github.com/user-attachments/assets/8b04a155-a180-4a7c-b0ba-63d0eac10f5a" />

<img width="668" height="355" alt="image" src="https://github.com/user-attachments/assets/dfb730c1-a636-49d2-9a76-616711c939b9" />


## ⚔️ Blocking vs Non-Blocking Assignments

This is a crucial concept when using the `always` block in Verilog.

### 🧱 Blocking Assignment (`=`)
- Executes **in the order** the statements are written — like in C programming.
- One statement **blocks** the execution of the next until it's completed.
- Example behavior: First line is executed → then second line → and so on.

### ⚡ Non-Blocking Assignment (`<=`)
- **Right-hand side (RHS)** of all statements is evaluated **first**.
- Then assignments are **executed in parallel**.
- The order of statements **does not affect** the final outcome (ideal for sequential logic like flops).

<img width="175" height="101" alt="image" src="https://github.com/user-attachments/assets/839e6308-d453-4fd6-a075-6f732933f50a" />

---

### 🚧 Caveats of Blocking Assignments

**Example Goal 1**: Creating a shift register.

> ❌ If you use blocking assignments (`=`), values may be overwritten in the same simulation cycle because each statement updates immediately.

> ✅ For sequential logic like shift registers, **non-blocking (`<=`) assignments are recommended** to ensure correct clocked behavior.

<img width="635" height="392" alt="image" src="https://github.com/user-attachments/assets/453bcf22-bba2-4f71-aa57-a98024e48af7" />

<img width="709" height="481" alt="image" src="https://github.com/user-attachments/assets/e602328a-32e3-41bc-b5ae-42a667c4f249" />

Always use non-blocking in the case of writing the codes for sequential circuits.

---

### 🧪 Summary
| Assignment Type | Symbol | Execution Style      | Use Case               |
|-----------------|--------|----------------------|------------------------|
| Blocking        | `=`    | Sequential (step-by-step) | Combinational logic (sometimes) |
| Non-Blocking    | `<=`   | Parallel (event-driven)   | Clocked logic (flip-flops, registers) |

---

**Example Goal 2**: To create a circuit like mentioned below: (Synthesis Simulation Mismatch)

<img width="304" height="126" alt="image" src="https://github.com/user-attachments/assets/b0a7cedf-2319-4675-9a1b-31c989f9d760" />

<img width="885" height="452" alt="image" src="https://github.com/user-attachments/assets/8a41e28f-52ad-43b0-994d-906baaf4ee0e" />

### 🧪 Why Simulation Mismatches Occur

- Both blocking (`=`) and non-blocking (`<=`) assignment styles can result in the **same synthesized hardware circuit**.
- However, during **RTL simulation**, their behavior may differ significantly due to **timing and ordering of updates**.
- These mismatches are often **not caught** in RTL simulation alone.

### 🔍 Why We Need GLS (Gate Level Simulation)

- GLS simulates the **post-synthesis netlist** and exposes issues that RTL simulation might miss.
- Essential for catching:
  - Mismatches caused by incorrect use of blocking assignments
  - Missing sensitivity lists
  - Glitches or race conditions
- GLS helps **align simulation behavior with actual hardware behavior**, especially when SDF (Standard Delay Format) is used.

---

### LAB WORK:

🔍 How to invoke GLS:

<img width="663" height="496" alt="image" src="https://github.com/user-attachments/assets/425c0048-f3ab-42a8-b598-bdcc7d55207a" />

TERNARY OPRTATOR:
Y = SEL?I1:I0;

<img width="1205" height="105" alt="image" src="https://github.com/user-attachments/assets/13b1506f-205f-4b31-a79f-1864d2c7ebef" />

<img width="1205" height="112" alt="image" src="https://github.com/user-attachments/assets/87d68e84-c39e-43b0-b4dd-baf8190d7e09" />

<img width="751" height="284" alt="image" src="https://github.com/user-attachments/assets/f74a3d5c-12b1-46cf-96b4-6fc063829ef0" />

<img width="434" height="303" alt="image" src="https://github.com/user-attachments/assets/e2e25915-5f2e-4dc8-b1d3-d0ac73399795" />

<img width="591" height="191" alt="image" src="https://github.com/user-attachments/assets/d87ea3de-9ac6-4bc4-8cd4-1fecc16b2db9" />

<img width="520" height="191" alt="image" src="https://github.com/user-attachments/assets/f77d41de-9afd-4947-b25a-f0b76aa123ce" />

<img width="1205" height="90" alt="image" src="https://github.com/user-attachments/assets/9320e36b-bb50-4f08-aff5-3650a6f232f3" />

<img width="1205" height="190" alt="image" src="https://github.com/user-attachments/assets/d8e57b5d-46e5-4a77-bc19-4416f8d32aa1" />

---

## ⚠️ BAD MUX Example:

<img width="566" height="153" alt="image" src="https://github.com/user-attachments/assets/31b9956d-3607-4d83-8b95-d5bbd0524acc" />

<img width="1059" height="246" alt="image" src="https://github.com/user-attachments/assets/8337022a-d55c-4051-95b4-5880b892b776" />

<img width="1205" height="98" alt="image" src="https://github.com/user-attachments/assets/8242d71c-ba7f-4759-b446-f09295d8c4a2" />

<img width="351" height="236" alt="image" src="https://github.com/user-attachments/assets/ccd29078-e6c3-439d-805a-9c470a52f916" />

<img width="428" height="236" alt="image" src="https://github.com/user-attachments/assets/f6b6287a-cb46-4c4e-a9b2-385a1868114d" />

<img width="1205" height="219" alt="image" src="https://github.com/user-attachments/assets/c5532e4a-12db-4eb1-8c56-d5d8c3a50260" />

<img width="1205" height="121" alt="image" src="https://github.com/user-attachments/assets/2e5f1d01-aa40-4a22-9b0b-483e8c6e0dd6" />

## ⚠️ Synthesis-Simulation Mismatch: BAD MUX Due to Missing Sensitivity List

A **BAD MUX** can cause mismatches between RTL simulation and synthesized hardware if the **sensitivity list is incomplete** or **latch behavior is inferred**.

### 🔍 Issue:
Incorrect use of sensitivity lists in combinational always blocks can result in:
- Simulated output behaving differently from synthesized circuit;
- Latch inference instead of a proper multiplexer;

---

## ⚠️ Blocking Statement Caveat

When using **blocking (`=`)** assignments inside `always` blocks, simulation may behave differently from actual synthesized hardware, especially in **sequential logic** like shift registers.

### 🧨 Problem:
Using **blocking assignments** in sequential circuits can lead to **unexpected simulation results** or **incorrect synthesis**.

### ❌ Bad Example (Blocking Assignment):

always @(posedge clk) begin
  
  a = b;
 
  b = a;

end


### ✅ Corrected Example (Non-blocking Assignment)::

always @(posedge clk) begin

  a <= b;
  
  b <= a;

end

<img width="568" height="124" alt="image" src="https://github.com/user-attachments/assets/4a99bfd7-e666-4856-bf70-6d3642761653" />

<img width="304" height="126" alt="image" src="https://github.com/user-attachments/assets/945f9c60-91e1-4078-8512-054b512b92d3" />

<img width="604" height="159" alt="image" src="https://github.com/user-attachments/assets/e9469132-b502-485a-a3dc-7352e56de18e" />

<img width="593" height="260" alt="image" src="https://github.com/user-attachments/assets/b9e54368-0628-4a3f-865f-446b77fa4a60" />

<img width="352" height="283" alt="image" src="https://github.com/user-attachments/assets/8a07bdd5-0b43-4713-912d-ecf6a2a79264" />

<img width="251" height="319" alt="image" src="https://github.com/user-attachments/assets/a8508e3d-464e-40e9-a853-47bb4a74a68a" />

<img width="547" height="177" alt="image" src="https://github.com/user-attachments/assets/d2fb155a-8a8f-415b-b647-a37698989d7b" />

-	It is looking at the latest value.

<img width="1205" height="417" alt="image" src="https://github.com/user-attachments/assets/7684dc47-b826-44db-bb8e-bd1754a52e5d" />

### 🔍 Root Cause:
- ❌ Blocking assignments execute **sequentially** within the `always` block.
- ❌ Each assignment **sees the latest updated value**, not the **previous cycle's value**.
- ⚠️ This breaks time-dependent behavior like shift registers or counters.

---

## Day 5: IF-CASE Constructs
