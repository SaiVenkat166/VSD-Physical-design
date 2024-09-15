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

# DAY 3 
Inverter layout

![image](https://github.com/user-attachments/assets/6a6781b3-92e0-46af-b5be-8b00605c2660)

## Some DRC issues with sky130_inv layout (unchanged)
![image](https://github.com/user-attachments/assets/847f023e-7156-4069-8e26-eaadd877a90e)

## generate spice from layout
use following commands:

![image](https://github.com/user-attachments/assets/8d892b35-9dc3-4a40-84ed-973db999a5a5)

## Spice netlist (unchanged)
![image](https://github.com/user-attachments/assets/8b667212-56e9-4a3e-b7ed-2d4d30fd53d8)

## grid size:
![image](https://github.com/user-attachments/assets/75f50304-fe86-412d-9e0a-7b099923dd2b)


``` ext2spice cthresh 0 rthresh 0 ``` to set the threshold of value of cap and resistance to 0. Basically to include every capacitor and resistor in netlist even if it's value is small.

## SPICE netlist after extraction
Changed load cap to ```2fF``` to smoothen the output voltage waveform
![image](https://github.com/user-attachments/assets/37479b73-7094-45c8-a30e-d27d3b0bc10e)

## Run ngspice (install using ```sudo apt install ngspice```)
![image](https://github.com/user-attachments/assets/da179ffb-86a7-43ef-91aa-20ea9127f041)

## 4 important parameters to measure from the output waveform:
1.Rise Transistion -> time taken for output to reach 20% to 80% of ideal voltage
2.Fall Transistion -> time taken for output to reach 80% to 20% of ideal voltage
3.Rise cell delay -> difference between time at which cell input is at 50% of ideal voltage to cell rising output at 50% of ideal voltage
4.Fall cell delay -> difference between time at which cell input is at 50% of ideal voltage to cell falling output at 50% of ideal voltage
```
>>> 0.8*3.3 #80% of ideal voltage
2.64
>>> 0.2*3.3 #20% of ideal voltage
0.66
>>> 0.5*3.3 #50% of ideal voltage
1.65

1.Rise Transistion time:
x0 = 2.23924e-09, y0 = 2.64025
x0 = 2.17956e-09, y0 = 0.66037
>>> 2.23924e-09-2.17956e-09
5.967999999999994e-11s

2.Fall Transistion:
x0 = 4.05083e-09, y0 = 2.64021
x0 = 4.09317e-09, y0 = 0.660208
>>> 4.09317e-09-4.05083e-09
4.23400000000005e-11s

3.Rise cell delay
x0 = 2.15e-09, y0 = 1.65
x0 = 2.2072e-09, y0 = 1.65
>>> 2.2072e-09-2.15e-09
5.7200000000000175e-11s

4.Fall cell delay
x0 = 4.04997e-09, y0 = 1.64995
x0 = 4.07536e-09, y0 = 1.65
>>> 4.07536e-09-4.04997e-09
2.538999999999964e-11s
```

![image](https://github.com/user-attachments/assets/53e64007-d48e-4875-b51c-a8e7d403de18)
![image](https://github.com/user-attachments/assets/c7d733bf-26b4-433a-bdf8-91ad278c7529)
![image](https://github.com/user-attachments/assets/25d4f7fb-9783-4dab-89eb-5e4cbe3847c8)

## conditions:
![image](https://github.com/user-attachments/assets/484ebaf5-625e-4f42-8bfa-eb3936e4fcab)

## pin definitions
![image](https://github.com/user-attachments/assets/f7e7ea80-4c29-4ad0-bd5a-8d1c2678e9f8)
![image](https://github.com/user-attachments/assets/c9da2387-7dea-42b6-a7cd-1a5f17805adb)
![image](https://github.com/user-attachments/assets/05028b18-08b3-4612-8240-512af885af8a)
![image](https://github.com/user-attachments/assets/c63ff159-5431-4b26-b70c-67b08b552ca6)
![image](https://github.com/user-attachments/assets/23dbdab3-aab9-4f1f-8af0-0643246a0669)
![image](https://github.com/user-attachments/assets/1bedb3e4-53c6-4215-9769-13ac8a502a61)

![image](https://github.com/user-attachments/assets/ca7b4bf7-0002-420c-901c-ffa57695fb79)
![image](https://github.com/user-attachments/assets/68bf211e-54dc-4fbc-81eb-25d3e36e145b)

![image](https://github.com/user-attachments/assets/d9846c36-94e5-401a-bae4-1c694186f1fd)
![image](https://github.com/user-attachments/assets/4e541ebf-d283-463a-a1bc-8a118f1c66b0)

## Custom cell placed in design
![image](https://github.com/user-attachments/assets/0427f12b-8f1b-4748-b913-3679e7107885)

# Day 4
## Post-Synthesis timing analysis with OpenSTA tool.
create pre_sta.conf file
![image](https://github.com/user-attachments/assets/e277c1a8-5886-440e-a4a5-0f8eb8e7f27e)

and my_base.sdc file
![image](https://github.com/user-attachments/assets/33d952b3-9710-48a5-b812-3bd2af84f482)

```# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Command to invoke OpenSTA tool with script
sta pre_sta.conf
```
![image](https://github.com/user-attachments/assets/2e9872f5-3e58-4b57-9f9a-160a11c5d1c5)

Try out different things to make the slack positive if it is not met
```
replace_cell instance_name cell_to_be_replaced_with
report_checks -fields {net cap slew input_pins} -digits 4
report_tns
report_wns
write_verilog <path> #to dumpout the final netlist with modifications
```
![image](https://github.com/user-attachments/assets/09a7c356-c608-4ce8-b348-8fe986c53848)

## Run CTS
![image](https://github.com/user-attachments/assets/22ced480-7cf1-482b-9a42-898c80e61f7e)

## After CTS:
![image](https://github.com/user-attachments/assets/f54e1722-35d0-4037-9c91-502b2d521f4e)


## OPENROAD
![image](https://github.com/user-attachments/assets/b71fc801-e5d6-4f51-8d8c-8d97b409d01b)


![image](https://github.com/user-attachments/assets/a90af6d2-633c-421a-bc04-30b84400e682)

## Clock skew for setup and hold:
![image](https://github.com/user-attachments/assets/be7b20cb-3219-4ed3-bc91-aa062549d77f)

# DAY 5

## Routing
gen_pdn
![image](https://github.com/user-attachments/assets/e90c24e6-c67d-43bc-987e-e2e9ecf29d12)
pdn generated successfully
![image](https://github.com/user-attachments/assets/88db6c56-9109-44a8-bcee-00e76ab5e04f)

run_routing
![image](https://github.com/user-attachments/assets/818696b8-a6f6-4e3d-8025-c137bd23acea)

![image](https://github.com/user-attachments/assets/6813a5f7-befb-4545-a124-cd34a000419b)

SPEF file generated after routing is done
![image](https://github.com/user-attachments/assets/872f945b-31a0-4891-8795-8856fc1645f7)











