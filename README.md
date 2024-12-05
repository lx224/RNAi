# 2024-Team 3-Automating RNA Interference Screening with Opentron OT2
### Authors: Zhuming Lin & Lin Xiong (Ash)
### Overview 
Followed by protocol provided in the study named 'RNA Interference Screening to Identify Proliferation Determinants in Breast Cancer Cells', this protocol takes inputs from a xlsx template file and autogenerates codes based on the input data for application on opentron OT2. The laborious RNA interference screening could be broken down to 4 major steps for each plate as followed, which could have different order according to experimental needs.
1. siRNA Addition to 96 well plates 
2. Transfection Lipid Medium Addtion to 96 well plates
3. Cell Suspension Addition to 96 well plates
4. Additional Steps According to Experimental Designs
### Source

### Category
Synthetic Biology
### Created and Last Modified
- Created at: 2024-12-04
- Last Modified: 2024-12-0
### Protocol Steps:
#### Introduction on Excel template:
This input template consists of 8 separate sheets. 3 of them must be preserved for script generation. 5 of them could be adjusted according to experimental design.
##### 3 Not-To-Be-Disturbed Sheets
- Labwares: This sheet has 5 columns: 'Labwares Type', 'Specific Type', 'Location on Opentron', 'Names' and 'API'.
![image](https://github.com/user-attachments/assets/fc871f97-f45c-4ed1-9a01-cd5a164f5777)
     'Labwares Type' only takes 3 types of input: 'Tips Racks', 'Reservoirs' and 'Well Plates'. You may add as many tips racks and reservoirs as you need. (Well Plates number should be smaller than or equal to 2 due to complexity (and thus extensive tip usage) of the screening process.) However, the total amounts of Labwares/rows should not exceed opentron's compatbility (14). Although the inputs in this column is restricted to these 3 types, it leaves room for future updates on the codes to include more standard labwares.
     'Specific Type': In this column, you should input '20'or '300' for 'Tips Racks' for P20 and P300 pipettes; '12' for 'Reservoirs' and '96' for 'Well Plates'. Although the inputs in this column is restricted to these 5 numbers, it leaves room for future updates on the codes to include more standard labwares.
     'Location on Opentron': This column takes integer numbers 1-14 as inputs. It specifies where labwares should be placed on opentron platform. Please try your best to make sure you follow the schematics below as much as you can. This rough layout design minimizes the length for robotic arm movements and thus drastically decrease possible leak or spill.
![image](https://github.com/user-attachments/assets/5a3c69c8-6690-4705-ae69-37e10b6ad2d7)
    'Names': This column specifies how you wanna refer to each tips rack, reservoir and well plates. Please follow the given format and name the labwares sequentially.
    'API': This column specifies the standard labwares that opentrons could take in. Please check your lab supplies before inputting.
- Reservoir and Reagents: This sheet has 4 columns: 'Reagent Types', 'Reagents', 'Reservoir' and 'Reservoir Well'.
![image](https://github.com/user-attachments/assets/c4fb9760-24ed-46ff-b7ea-ab05f8e194a3)
    'Reagent Types': Within the scope of RNAi screening, this column takes 3 inputs: 'Transfection Reagent  Medium', 'siRNA', 'Cell Suspension'.
    'Reagents': This column takes the names of the specific reagent that you are going to apply to your experiment. Abbreviations of the reagents should follow the general rules of naming variables in python. E.g. Opti_Mem_1.
    'Reservoir': If you have more than 1 reservoirs to use. Please specify in which reservoir should a particular reagent be added in this column.
    'Reservoir Well': Please use this column to specify in which well of the previous defined reservoir a particular reagent should be added.
- Addition_V&T: This sheet has 4 columns:'Reagent Types', 'Addition Volume', 'Wait Time (s)' and 'Order'.
![image](https://github.com/user-attachments/assets/da59aed5-e717-4c98-ac99-a7c198a45e23)
    'Reagent Types': Within the scope of RNAi screening, this column takes 3 inputs: 'Transfection Reagent  Medium', 'siRNA', 'Cell Suspension'.
    'Addition Volume': This column specifies the volume each type of reagents should be added in each experimental step.
    'Wait Time (s)': This column takes integer inputs. It specifies the wait time or incubation time that some experimental steps (e.g. siRNAs and Transfection Lipids Medium forming lipid particles) may need.
    'Order': This column takes integer inputs like '1', '2', '3', which specifies the order of each experimental step.
##### 5 Adjustable Sheets
- 4 'XXXXXX Layout 96 Well Plate':
  An empty 'XXXXXX Layout 96 Well Plate':
  ![image](https://github.com/user-attachments/assets/177ecc24-7948-4a86-8a25-7f4c2e4fbcc3)
  An example filled 'Z Score Layout 96 Well Plate':
  ![image](https://github.com/user-attachments/assets/e30fa3c3-a4af-47d9-a8f3-4ea50ad89220)
  3 of them are 'StepX Layout 96 Well Plate' for plate layout design and data input of each experimental steps. The last one is named 'Z Score Layout 96 Well Plate', whose name should be left undistrubed if you do not understand how to change codes accordingly. But the contents in the last plate could be for experimental measures other than Z Score plate layout.
  For sheets following this naming convention, please separate the addition of different   reagents. 1 sheet should only contain addition of 1 type of reagents added with an uniform amount specified in 'Addition_V&T' sheet. There is no limit on the how many different reagents you may use, they just have to be of the same type and same amount.
- 1 '96 Well +Index Template':
![image](https://github.com/user-attachments/assets/e13191c7-29a3-45a9-b099-f0dacefe2153)
  This template sheet offers an alternative visual display and method for you to plan your 96-well plate layout. In this sheet, you could specify what reagents to add in each step in 1 sheet instead of 3. If this sheet is filled, #######
