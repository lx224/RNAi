# 2024-Team 3: Automating RNA Interference Screening with Opentron OT-2
### Authors: Zhuming Lin & Lin Xiong (Ash)

---

## Overview  
This protocol automates RNA interference (RNAi) screening using the Opentrons OT-2 robot. It is based on the study *"RNA Interference Screening to Identify Proliferation Determinants in Breast Cancer Cells."* The protocol is composed of 2 documents, 1 input `.xlsx` template and 1 'Protocol Generator' script. The 'Protocol Geberator' script will read inputs from the `.xlsx` template, and generate another python script to be applied for automation step.

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

### Section 1: Excel Input Template  

The input template consists of eight sheets, three of which must remain unaltered for script generation. The remaining five sheets can be adjusted based on experimental design.  

#### **Non-Editable Sheets**  
These sheets are essential for script generation and must not be modified beyond their intended inputs.  

1. **Labwares**  
   This sheet contains five columns:  
   - **Labwares Type:** Acceptable inputs are `Tips Racks`, `Reservoirs`, and `Well Plates`. (Note: You may include up to two well plates, but the total number of labwares must not exceed 14 slots.)  
   - **Specific Type:** Inputs include `20` or `300` for tip racks (P20 and P300 pipettes), `12` for reservoirs, and `96` for well plates.  
   - **Location on Opentron:** Specify slot numbers (1–14) for labware placement, following the schematic below to minimize robotic arm movement, reduce spills and avoid labwares collision.
     ![Opentron Layout Example](https://github.com/user-attachments/assets/ad0d7f96-ed5e-4d8f-b4bd-66f607acc91a)
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
### Section 2: Protocol Generator Script

#### 2.1 Introduction of the Study *"RNA Interference Screening to Identify Proliferation Determinants in Breast Cancer Cells."*
This study conducted RNA interference (RNAi) screening to identify proliferation determinants in breast cancer cells, focusing on genes associated with the estrogen receptor (ER) signaling network. The experimental design is as follows:

Purpose:
To identify genes critical for cell proliferation in breast cancer by knocking down genes using siRNA targeting an ER-related network.

Cell Types Used:

MCF7 (ER-positive breast cancer cells)
Estrogen-independent variants of MCF7 (LCC1 and LCC9)
Triple-negative breast cancer cells (MDA-MB-231)
Epidermoid cancer cells (A431)
Human fibroblast cells (HFF1)
Transfection Lipids Applied:
Seven types of transfection reagents were tested for optimal transfection efficiency in MCF7 cells:

HiPerfect
RNAiFect
DharmaFect 1
DharmaFect 2
DharmaFect 3
DharmaFect 4
RNAiMax
siRNAs Applied:

The siRNA library targeted 631 genes in the ER network.
Each gene was targeted by two siRNAs mixed into one well.
The library comprised 11 plates, with siRNAs distributed into 96-well plates.
Plates Used in Each Experiment:


Part I: Selection of Transfection Reagents: Seven 96-well plates were used, testing different lipid combinations.
Part II: Z’-Score Determination: Two 96-well plates per experiment for quality control.
Part III: ER Network Screening: A total of 11 experimental plates were used for the RNAi library screening.

For all 3 parts, the experimental steps involved could be broken down to 4 steps.
1. **siRNA Addition**  
2. **Transfection Lipid Medium Addition**  
3. **Cell Suspension Addition**  
4. **Additional Steps According to Experimental Design**

#### 2.2 Introduction to Codes in Each Part
#### Part I. Selection of transfection reagents
