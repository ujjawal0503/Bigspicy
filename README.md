# BigSpicy - Merging SPEF, Verilog and Spice information into Circuit protobuf and generating the spice file <br/>
This repo shows the steps for merging the SPEF, verilog and spice netlist into a circuit protobuf and generating the spice file of the design which can further be used to perform various tests and analysis.<br/>
In this repo, I have used the design of 3-bit ring counter implemented using SKY130 PDKS. The RTL to GDS2 flow of the given design can be referred from the following github repo.<br/>
https://github.com/ArshKedia/iiitb_3bit_rc <br/>

## FLOWCHART : <br/>
![200117467-c5c6d165-5011-4002-9b82-d756f3bbd48d](https://user-images.githubusercontent.com/64605104/206892403-9238ee48-5b2f-43e7-86d4-9f81d6f67f62.png)
<br/>
## PREREQUISITES : <br/>
1. We need the pdk files in Xyce format.<br/>
   To convert any PDK in Xyce format refer the following github repo.<br/>
   https://github.com/LokeshMaji <br/>
   
To install the python dependencies, follow the below steps: <br/>
```
git clone https://github.com/ArshKedia/BigSpicy
cd BigSpicy/
sudo apt-get update
pip install -e ".[dev]"
pip install -r requirements.txt
sudo apt install -y protobuf-compiler iverilog
```
<br/>

Another prerequisite for this step is to compile protobufs into python file.(_pb2.py).<br/>
To compile the protobufs, type the below command in terminal in the BigSpicy(cloned_repo) directory:<br/>
```
git submodule update --init  
protoc --proto_path vlsir vlsir/*.proto vlsir/*/*.proto --python_out=.
protoc proto/*.proto --python_out=.
```
## Merging <br/>
We merge the files into circuit protobuf(final.pb) which is used to generate the whole module spice models and to conduct the various tests using Xyce.<br/>
To merge the files, follow the below steps in the BigSpicy directory: <br/>
```
./bigspicy.py \
   --import \
   --spef example_inputs/iiitb_3bit_rc/iiitb_3bit_rc.spef \
   --spice lib/sky130_fd_sc_hd.spice \
   --verilog example_inputs/iiitb_3bit_rc/iiitb_3bit_rc.v \
   --spice_header lib/sky130_fd_pr__pfet_01v8.pm3.spice \
   --spice_header lib/sky130_fd_pr__nfet_01v8.pm3.spice \
   --spice_header lib/sky130_ef_sc_hd__decap_12.spice \
   --spice_header lib/sky130_fd_pr__pfet_01v8_hvt.pm3.spice \
   --top iiitb_3bit_rc \
   --save final.pb \
```
This will generate final.pb file.<br/>
To specify the location of the final.pb file, go to bigspicy.py file and search for "def withoptions()" function. Change the "output_dir" variable to your desired path.<br/>

## Generating whole-module spice file <br/>
After generating the "final.pb" file, we now generate the spice file("spice.sp" in this case) for our design which can be further used to run tests.<br/>
This step takes the pdks, and the design as input and gives the spice file as output.<br/>
To generate the spice file, follow the below steps in BigSpicy directory: <br/>
```
./bigspicy.py --import \
    --verilog example_inputs/iiitb_3bit_rc/iiitb_3bit_rc.v \
    --spice lib/sky130_fd_sc_hd.spice \
    --spice_header lib/sky130_fd_pr__pfet_01v8.pm3.spice \
    --spice_header lib/sky130_fd_pr__nfet_01v8.pm3.spice \
    --spice_header lib/sky130_ef_sc_hd__decap_12.spice \
    --spice_header lib/sky130_fd_pr__pfet_01v8_hvt.pm3.spice \
    --save final.pb \
    --top iiitb_3bit_rc \
    --flatten_spice --dump_spice spice.sp
```
The above steps will generate "spice.sp" file in the mentioned directory.<br/>


## ACKNOWLEDGMENTS <br/>
- Kunal Ghosh, Director, VSD Corp. Pvt. Ltd.<br/>
- Madhav Rao, Professor, IIIT-Bangalore<br/>
- Nanditha Rao, Professor, IIIT-Bangalore<br/>


