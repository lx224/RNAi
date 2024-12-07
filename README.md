# 2024-Team 3: Automating RNA Interference Screening with Opentron OT-2
### Authors: Zhuming Lin & Lin Xiong (Ash)

---

## Overview  
This protocol automates RNA interference (RNAi) screening using the Opentrons OT-2 robot. It is based on the study *"RNA Interference Screening to Identify Proliferation Determinants in Breast Cancer Cells."* The protocol consists of two key components: an input `.xlsx` template and a 'Protocol Generator' script. The 'Protocol Generator' reads inputs from the `.xlsx` template and generates a Python script for automation.

---

## Source  

---

## Category  
**Synthetic Biology**

---

## Created and Last Modified  
- **Created:** 2024-12-04  
- **Last Modified:** 2024-12-07  

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

The input template consists of eight sheets. Three sheets must remain unaltered for script generation, while the other five are adjustable based on experimental design.

### Non-Removable Sheets

1. **Labwares**  
   - **Labware Type:** `Tips Racks`, `Reservoirs`, and `Well Plates`. Maximum 14 slots.  
   - **Specific Type:** `20` or `300` for tip racks, `12` for reservoirs, and `96` for well plates.  
   - **Location on Opentron:** Slots 1–14 for labware placement.  
     ![Opentron Layout Example](https://github.com/user-attachments/assets/ad0d7f96-ed5e-4d8f-b4bd-66f607acc91a)  
   - **Names:** Assign unique identifiers.  
   - **API:** Specify compatible Opentrons labware.  
     ![Labwares Example](https://github.com/user-attachments/assets/fc871f97-f45c-4ed1-9a01-cd5a164f5777)  

2. **Reservoir and Reagents**  
   - **Reagent Types:** `Transfection Reagent Medium`, `siRNA`, and `Cell Suspension`.  
   - **Reagents:** Python-formatted names (e.g., `Opti_Mem_1`).  
   - **Reservoir:** Assign reagent to specific reservoir and well.  
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

### Part I: Selection of Transfection Reagents
- **siRNA Addition**: Add **7 µL** siRNA mix per well (siNEG, siDEATH, siAP2A1).
- **Transfection Lipid Medium Addition**: Add **15 µL** lipid (e.g., HiPerfect, RNAiMax) diluted in Opti-MEM.
- **Additional Steps**: Add **100 µL** cell suspension (8,000 cells/well), incubate for 5 days, then measure viability using Cell Titer Blue.

### Part II: Z’-Score Determination
- **siRNA Addition**: Add **10 µL** siNEG and siDEATH siRNAs per well.
- **Transfection Lipid Medium Addition**: Add **10.5 µL** RNAiMax mix.
- **Additional Steps**: Add **100 µL** cell suspension, incubate for 6 days, then measure viability and calculate Z’-scores.

### Part III: ER Network Screening
- **siRNA Addition**: Add **10 µL** siRNA per well from a library of 631 genes.
- **Transfection Lipid Medium Addition**: Add **10.5 µL** RNAiMax mix.
- **Additional Steps**: Add **100 µL** cell suspension, incubate for 6 days, measure viability, and calculate viability indices.

### Code Description
1. **Dictionaries Generation**:
   - Reads `.xlsx` inputs with pandas to create dictionaries for each sheet.
   - Stores data in an output file for script generation.

2. **Python Script Creation**:
   - Automates reagent addition and experimental steps based on input dictionaries.
   - Outputs an OT-2 compatible script.

3. **Execution**:
   - Load the generated script onto the OT-2 platform to execute the experiment.
