# 2024-Team 3: Automating RNA Interference Screening with Opentron OT-2
### Authors: Zhuming Lin & Lin Xiong (Ash)

---

## Created and Last Modified  
- **Created:** 2024-12-04  
- **Last Modified:** 2024-12-09

---

## Overview  
This protocol automates RNA interference (RNAi) screening using the Opentrons OT-2 robot. It is based on the study *"RNA Interference Screening to Identify Proliferation Determinants in Breast Cancer Cells."* The protocol consists of two key components: 
   1. Input `.xlsx` template
   2.  'Protocol Generator' script.
- The 'Protocol Generator' reads inputs from the `.xlsx` template and generates a new Python script for automation.

---

## How-To-Use
**Follow these steps to prepare and execute the RNAi screening protocol using the Opentrons OT-2 platform:**

### 1. Prepare the Input Excel Template
a. Open the provided `.xlsx` input template.  
b. Fill in the sheets according to your experimental design:  
   - Edit the `StepX Layout` or `96 Well +Index Template` sheets to specify which siRNA, transfection reagents, and cell suspensions to add for each well.
   - Double-check the `Labwares`, `Reservoir and Reagents`, and `Addition_V&T` sheets for consistency.  

### 2. Generate the Automation Script
a. Update the import file name in the **Protocol Generator Script** to match your Input Excel Template.  
   - Ensure the script and the filled input `.xlsx` template are in the same directory. 

b. Run the **Protocol Generator Script** provided in the repository.  
   - The script will read the input `.xlsx` file, validate the data, and generate a Python script for automation.

### 3. Execute the Experiment on Opentrons OT-2
a. Confirm that the output Python file is successfully generated.  
b. Transfer the generated Python script to the Opentrons OT-2 robot platform.  
c. Set up the OT-2 workspace as specified in the `Labwares` sheet of your input template:  
   - Load the specified tip racks, reservoirs, and well plates in their respective slots.  

d. Run the script on the OT-2 and monitor the process to ensure proper execution.

### 4. Perform Your Post-Experiment Analysis
Analyze the data collected from the experiment.  
   - Review fluorescence or viability measurements to calculate Z’-scores and viability indices for quality control.  

---

## Study Introduction: *"RNA Interference Screening to Identify Proliferation Determinants in Breast Cancer Cells"*

This study employed RNA interference (RNAi) screening to identify proliferation determinants in breast cancer cells by targeting the estrogen receptor (ER) signaling network. 

**Experimental Design**:
- **Purpose**: Identify genes critical for cell proliferation by knocking down genes using siRNA targeting an ER-related network.
- **Cell Types**: MCF7 (ER-positive breast cancer cells), LCC1, LCC9, MDA-MB-231, A431, HFF1.
- **Transfection Reagents**: HiPerfect, RNAiFect, DharmaFect 1–4, RNAiMax.
- **siRNA Library**: Targeting 631 genes distributed across 11 plates.

The experimental design consisted of three parts:
1. **Part I: Selection of Transfection Reagents**
   - siRNA addition, lipid optimization, and cell viability measurements.
2. **Part II: Z’-Score Determination**
   - Quality control and reproducibility testing.
3. **Part III: ER Network Screening**
   - High-throughput screening using siRNA libraries.

---

## Section 1: Excel Input Template

The input template consists of eight sheets. Three sheets must remain for script generation, while the other can be deleted or duplicated (to add more experimental steps).
- NOTICE: For all sheets, don't change the contents in color-coded cells.
  Blue ones can be added or deleted by copying & pasting. Green cells should not be altered. Please follow these rules unless you know how to change the codes accordingly.

### Non-Removable Sheets

1. **Labwares**  
   - **Labware Type:** `Tips Racks`, `Reservoirs`, and `Well Plates`. Maximum 14 slots.  
   - **Specific Type:** `20` or `300` for tip racks, `12` for reservoirs, and `96` for well plates.  
   - **Location on Opentron:** Slots 1–14 for labware placement.
   - Examples:

     **Layout for PartI:
        `multi-channel P20` will collapse with tip racks if you do not follow this layout**
     <img width="585" alt="{0C4E3FAB-1171-4DF6-B10A-AFCA870688CC}" src="https://github.com/user-attachments/assets/079436da-6711-40f8-9cef-520aea7ffdba">
    **Layout for Part III:**
     <img width="615" alt="{7166208B-7D15-4550-9AC6-13974F48B173}" src="https://github.com/user-attachments/assets/46648810-fa00-4e4e-b528-74ac8a89fec9">
   - **Names:** Python-formatted names (e.g. res_1)
   - **API:** Specify compatible Opentrons labware.  
     ![Labwares Example](https://github.com/user-attachments/assets/fc871f97-f45c-4ed1-9a01-cd5a164f5777)  

2. **Reservoir and Reagents**  
   - **Reagent Types:** `Transfection Reagent Medium`, `siRNA`, and `Cell Suspension`.  
   - **Reagents:** Python-formatted names (e.g., `Opti_Mem_1`).  
   - **Reservoir:** Assign reagent to specific reservoir.
   - **Reservoir Wells:** Assign reagent to sepcific wells.  
     ![Reservoir and Reagents Example](https://github.com/user-attachments/assets/c4fb9760-24ed-46ff-b7ea-ab05f8e194a3)  

3. **Addition_V&T**  
   - **Reagent Types:** Same as above.  
   - **Addition Volume:** Specify volumes.  
   - **Wait Time (s):** Incubation times.  
   - **Order:** Sequence of steps.  
     ![Addition V&T Example](https://github.com/user-attachments/assets/da59aed5-e717-4c98-ac99-a7c198a45e23)  

### Removable Sheets

1. **Step Layout Sheets**  
   - Three `StepX Layout 96 Well Plate` sheets for designing plate layouts.  
   - One `Z Score Layout 96 Well Plate` sheet for analysis.  
   - Each sheet should only include one reagent type per step with uniform volumes.  

     Examples:  
     - **Empty Layout:**  
       ![Empty Layout Example](https://github.com/user-attachments/assets/177ecc24-7948-4a86-8a25-7f4c2e4fbcc3)  
     - **Filled Z Score Layout:**  
       ![Filled Z Score Example](https://github.com/user-attachments/assets/e30fa3c3-a4af-47d9-a8f3-4ea50ad89220)  

2. **96 Well +Index Template**  
   - Offers an alternative for planning plate layouts.  
     ![96 Well +Index Template Example](https://github.com/user-attachments/assets/e13191c7-29a3-45a9-b099-f0dacefe2153)  

---

## Section 2: Protocol Generator Script

### 2.1 Experimental Steps
#### Part I: Selection of Transfection Reagents
- **siRNA Addition**: Add **7 µL** siRNA mix per well (siNEG, siDEATH, siAP2A1).
- **Transfection Lipid Medium Addition**: Add **15 µL** lipid (e.g., HiPerfect, RNAiMax) diluted in Opti-MEM.
- **Additional Steps**: Add **100 µL** cell suspension (8,000 cells/well), incubate for 5 days, then measure viability using Cell Titer Blue.

#### Part II: Z’-Score Determination
- **siRNA Addition**: Add **10 µL** siNEG and siDEATH siRNAs per well.
- **Transfection Lipid Medium Addition**: Add **10.5 µL** RNAiMax mix (determined in Part I).
- **Additional Steps**: Add **100 µL** cell suspension, incubate for 6 days, then measure viability and calculate Z’-scores.

#### Part III: ER Network Screening
- **Z'-Score Plate Preparation**: Add **100µL** siRNA per well according to Z'-Score Plate Layout.
- **siRNA Addition**: Transfer **10 µL** siRNA per well from Z'-Score Plate.
- **Transfection Lipid Medium Addition**: Add **10.5 µL** RNAiMax mix (determined in Part I).
- **Additional Steps**: Add **100 µL** cell suspension, incubate for 6 days, measure viability, and calculate viability indices.

### 2.2 Code Description

1. **Dictionaries Generation**:
   - Reads `.xlsx` inputs with pandas to create dictionaries for each sheet.
   - Stores data at the start of the output script.

2. **Python Script Creation**:
   - Automates reagent addition and experimental steps based on input dictionaries.
   - Stores codes accordingly to the same ouput scipt and make it OT-2 compatible.

## Problems Encountered and Solved

1. **Problem**: Incompatible hardware usage (pipette type: single or multi-channel pipette) due to different specificity requirements in each part of the experiment.  
   - **Solution**: Adapt and optimize the code for `mp20` and `mp300` pipettes. Used the `pipette.configure_nozzle_layout(style=opentrons.protocol_api.SINGLE)` command to allow multi-channel pipettes to function as single-channel pipettes when needed.

2. **Problem**: Inputs in the `names` column of the Excel file contain empty spaces or special characters, which cannot be directly used in Python scripts.  
   - **Solution**: Enforce Python naming conventions for user inputs. Added code to strip empty spaces and handle special characters for critical inputs.

3. **Problem**: The experimental steps specified in the article sometimes require swapping the order of siRNA and transfection lipid mix additions for different purposes.  
   - **Solution**: Removed strict reagent assignments for `Step X` sheets. Instead, experimental order is defined in the `Addition_V&T` sheet, linking it to the corresponding `Step X Layout Sheets`.

4. **Problem**: During wet run simulations, liquids would drop out during transfer.  
   - **Solution**: Optimized labware placement on the OT-2 deck, ensuring that reservoirs and plates are adjacent and close to the liquid waste position (slot 15). Added code to introduce air gaps during reagent transfer to prevent dripping.

5. **Problem**: Liquid droplets sometimes remain on the outside of pipette tips.  
   - **Solution**: Implemented the `touch_tip` function to shake off residual liquid from the outside of the tips.

6. **Problem**: Small volumes (<100 µL) are challenging to mix effectively with pipette tips.  
   - **Solution**: This issue was not resolved within the scope of this project. However, it can be addressed in future work by incorporating a plate shaker or centrifuge for external mixing.

---

## Future Work

- Incorporate external mixing steps, such as plate shaking or centrifugation, to ensure proper mixing of transfection lipid mix and siRNA.
- Enhance the code to make use of additional information from the input Excel template, which is currently collected but not utilized.
- Expand automation to include advanced error handling and optimization for low-volume pipetting challenges.
- Develop a visual output interface to track and validate protocol execution in real-time on the OT-2 platform.



