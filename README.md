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
-     'Labwares Type' only takes 3 types of input: 'Tips Racks', 'Reservoirs' and 'Well Plates'. You may add as many tips racks and reservoirs as you need. (Well Plates number should be smaller than or equal to 2 due to complexity (and thus extensive tip usage) of the screening process.) However, the total amounts of Labwares/rows should not exceed opentron's compatbility (14). Although the inputs in this column is restricted to these 3 types, it leaves room for future updates on the codes to include more standard labwares.
-     'Specific Type': In this column, you should input '20'or '300' for 'Tips Racks' for P20 and P300 pipettes; '12' for 'Reservoirs' and '96' for 'Well Plates'. Although the inputs in this column is restricted to these 5 numbers, it leaves room for future updates on the codes to include more standard labwares.
-     'Location on Opentron': This column takes integer numbers 1-14 as inputs. It specifies where labwares should be placed on opentron platform. Please make sure 
- Reservoir and Reagents: This sheet has 4 columns: 'Reagent Types', 'Reagents', 'Reservoir' and 'Reservoir Well'.
-     
- Addition_V&T: This sheet has 4 columns:'Addition Volume', 'Wait Time (s)' and 'Order'.
##### 5 Adjustable Sheets
- 4 'XXXXXX Layout 96 Well Plate':
-     3 of them are 'StepX Layout 96 Well Plate' for plate layout design and data input of each experimental steps. The last one is named 'Z Score Layout 96 Well Plate', whose name should be left undistrubed if you do not understand how to change codes accordingly. But the contents in the last plate could be for experimental measures other than Z Score plate layout.
-     For sheets following this naming convention, please separate the addition of different   reagents. 1 sheet should only contain addition of 1 type of reagents added with an uniform amount specified in 'Addition_V&T' sheet. There is no limit on the how many different reagents you may use, they just have to be of the same type and same amount.
- 1 '96 Well +Index Template':
-     This template sheet offers an alternative visual display and method for you to plan your 96-well plate layout. In this sheet, you could specify what reagents to add in each step in 1 sheet instead of 3. If this sheet is filled, #######
