# 2024-Team 3: Automating RNA Interference Screening with Opentron OT-2
### Authors: Zhuming Lin & Lin Xiong (Ash)

---

## Overview  
This protocol automates RNA interference (RNAi) screening using the Opentrons OT-2 robot. It is based on the study *"RNA Interference Screening to Identify Proliferation Determinants in Breast Cancer Cells."* The protocol generates automation scripts from an input `.xlsx` template. The RNAi screening process for each 96-well plate can be divided into four major steps, which may be reordered as needed:  

1. **siRNA Addition**  
2. **Transfection Lipid Medium Addition**  
3. **Cell Suspension Addition**  
4. **Additional Steps According to Experimental Design**  

---

## Source  

---

## Category  
**Synthetic Biology**  

---

## Created and Last Modified  
- **Created:** 2024-12-04  
- **Last Modified:** 2024-12-05  

---

## Protocol Steps  

### Introduction to Excel Template  
The input template consists of eight sheets, three of which must remain unaltered for script generation. The remaining five sheets can be adjusted based on experimental design.  

#### **Non-Editable Sheets**  
These sheets are essential for script generation and must not be modified beyond their intended inputs.  

1. **Labwares**  
   This sheet contains five columns:  
   - **Labwares Type:** Acceptable inputs are `Tips Racks`, `Reservoirs`, and `Well Plates`. (Note: You may include up to two well plates, but the total number of labwares must not exceed 14 slots.)  
   - **Specific Type:** Inputs include `20` or `300` for tip racks (P20 and P300 pipettes), `12` for reservoirs, and `96` for well plates.  
   - **Location on Opentron:** Specify slot numbers (1–14) for labware placement, following the schematic below to minimize robotic arm movement and reduce spills.  
   - **Names:** Assign unique, sequential names to labware.  
   - **API:** Specify compatible Opentrons labware. Ensure lab supplies match the inputs.  
   ![Labwares Example](https://github.com/user-attachments/assets/fc871f97-f45c-4ed1-9a01-cd5a164f5777)  

2. **Reservoir and Reagents**  
   This sheet includes:  
   - **Reagent Types:** Inputs include `Transfection Reagent Medium`, `siRNA`, and `Cell Suspension`.  
   - **Reagents:** Names of specific reagents, formatted in Python variable style (e.g., `Opti_Mem_1`).  
   - **Reservoir:** Assign the reservoir where the reagent will be added.  
   - **Reservoir Well:** Specify the well within the reservoir.  
   ![Reservoir and Reagents Example](https://github.com/user-attachments/assets/c4fb9760-24ed-46ff-b7ea-ab05f8e194a3)  

3. **Addition_V&T**  
   This sheet specifies the volume, wait time, and order for reagent additions:  
   - **Reagent Types:** Same inputs as the previous sheet.  
   - **Addition Volume:** Volume for each reagent.  
   - **Wait Time (s):** Incubation time for specific steps.  
   - **Order:** Sequence of experimental steps.  
   ![Addition V&T Example](https://github.com/user-attachments/assets/da59aed5-e717-4c98-ac99-a7c198a45e23)  

---

#### **Editable Sheets**  
The following five sheets are customizable to suit experimental designs:  

1. **Step Layout Sheets**  
   - Three `StepX Layout 96 Well Plate` sheets for designing plate layouts and inputting data for each experimental step.  
   - One `Z Score Layout 96 Well Plate` sheet for experimental analysis. The name of this sheet must remain unchanged unless you update the code accordingly.  
   - Each sheet should only contain additions of one reagent type with uniform amounts as specified in the `Addition_V&T` sheet.  

   Examples:  
   - **Empty Layout:**  
     ![Empty Layout Example](https://github.com/user-attachments/assets/177ecc24-7948-4a86-8a25-7f4c2e4fbcc3)  
   - **Filled Z Score Layout:**  
     ![Filled Z Score Example](https://github.com/user-attachments/assets/e30fa3c3-a4af-47d9-a8f3-4ea50ad89220)  

2. **96 Well +Index Template**  
   This sheet offers an alternative visual method to plan 96-well plate layouts. In this sheet, you can specify reagents for each step in one location instead of across three separate sheets.  
   ![96 Well +Index Template Example](https://github.com/user-attachments/assets/e13191c7-29a3-45a9-b099-f0dacefe2153)  

---
