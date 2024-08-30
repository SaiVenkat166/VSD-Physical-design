# DAY 1 Design preparation and Synthesis using OPENLANE Flow #

## Design prep
![image](https://github.com/user-attachments/assets/9fec2a7f-a71d-46f9-bea4-0b0ec1edc980)

## Synthesis results
![image](https://github.com/user-attachments/assets/87af39aa-062b-4b0f-ace5-e19d240cf93c)

chip area after synthesis

![image](https://github.com/user-attachments/assets/76dbd9ca-5222-4032-aef5-5b73beb80f52)

Flop ratio = Number of flops / Number of cells = 1613/14876 = 0.1084 => 10.84%

# DAY 2 
## run_floorplan
![image](https://github.com/user-attachments/assets/853d6c5e-4e2e-443d-a6b4-6e51d3072482)

![image](https://github.com/user-attachments/assets/a38703ca-5c46-4249-a7ab-88eafc707ec6)

## floorplan config:
![image](https://github.com/user-attachments/assets/bc0f5a39-a31e-42a4-9ebb-2c46879ab7ee)

## Die area from floorplan DEF
![image](https://github.com/user-attachments/assets/048fbc5a-390a-4298-a40f-32c32efdfaf6)
``` 1000 DBS = 1 Micron
Die width = 660685/1000 = 660.685 um
Die height =  671405/1000 = 671.405 um 
Die Area = 660.685 * 671.405 = 443587.212425 sq.um
```

## floorplan snapshot
Using **MAGIC tool**

command: ```magic -T home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &```
![image](https://github.com/user-attachments/assets/b7cba886-54cf-4687-9d84-ddf4e3fbb168)

## equi-distance pins
![image](https://github.com/user-attachments/assets/a0d7b255-fbb3-41a2-ab8e-770193d9d120)

## horizontal metal 3
![image](https://github.com/user-attachments/assets/0f77f189-1376-4cd7-93e6-37f57230e9dd)

## Standard cells in lower left corner (origin)
![image](https://github.com/user-attachments/assets/dd01e8b1-0072-4588-b01a-9eb7f9fe6223)

## Placement
### With default configuration
![image](https://github.com/user-attachments/assets/f26bf173-4817-4820-a785-c4b44257aec1)

![image](https://github.com/user-attachments/assets/f22f2e1c-a2c3-456e-8876-9fed9f1141f6)

### Timing driven placement
![image](https://github.com/user-attachments/assets/b6a575fb-20a9-4ecc-abd1-36005fe19e09)

### What happens when PL_ROUTABILITY_DRIVEN and PL_TIME_DRIVEN are set to true?
![image](https://github.com/user-attachments/assets/5eda957a-83d1-409c-88f2-37cc5d2a17f9)
![image](https://github.com/user-attachments/assets/d34c6bbd-a669-46e0-810d-a59d96d6befa)

### Routability driven
![image](https://github.com/user-attachments/assets/8f301451-efae-47a2-9389-8be477876d41)

![image](https://github.com/user-attachments/assets/9e530148-3199-40ad-b3ae-724cb21fed67)






