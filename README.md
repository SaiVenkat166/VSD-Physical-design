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


