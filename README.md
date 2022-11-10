# BigSpicy - Merging SPEF, Verilog and Spice information into Circuit protobuf <br/>
This repo shows the steps for merging the SPEF, verilog and spice netlist into a circuit protobuf.<br/>
It takes .spef, .v, and .spice file as input and generate final.pb file as output.<br/>
## PREREQUISITES : </br>
1. We need the pdk files in Xyce format.<br/>
   To convert any PDK in Xyce format refer the following github repo.<br/>
   https://github.com/LokeshMaji <br/>
   In this repo, we have used the design of 3-bit ring counter implemented using SKY130 PDKS. The RTL to GDS2 flow of the given design can be referred from the following github repo.<br/>
https://github.com/ArshKedia/iiitb_3bit_rc <br/>
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
    --verilog iiitb_3bit_rc/iiitb_3bit_rc_synth.v \
    --spef iiitb_3bit_rc/iiitb_3bit_rc.spef \
    --spice_header lib/sky130_fd_sc_hd.spice \
    --top iiitb_3bit_rc \
    --save final.pb \
    --working_dir /tmp/bigspicy
```

