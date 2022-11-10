# BigSpicy - Merging SPEF, Verilog and Spice information into Circuit protobuf <br/>
This repo shows the steps for merging the SPEF, verilog and spice netlist into a circuit protobuf. 
## PREREQUISITES : </br>
1. We need the pdk files in Xyce format.<br/>
   To convert any PDK in Xyce format refer the following github repo.<br/>
   https://github.com/LokeshMaji <br/>
   In this repo, we have used the design of 3-bit ring counter implemented using SKY130 PDKS. The RTL to GDS2 flow of the given design can be referred from the following github repo.<br/>
https://github.com/ArshKedia/iiitb_3bit_rc <br/>
To install the python dependencies, follow the below steps:
'''
git clone https://github.com/ArshKedia/BigSpicy
sudo apt-get update
pip install -e ".[dev]"
pip install -r requirements.txt
sudo apt install -y protobuf-compiler iverilog
'''
<br/>

Another prerequisite for this step is to compile protobufs into python file.(_pb2.py).<br/>
To compile the protobufs, type the below command in terminal in the BigSpicy(cloned_repo) directory:<br/>
```
git submodule update --init  
protoc --proto_path vlsir vlsir/*.proto vlsir/*/*.proto --python_out=.
protoc proto/*.proto --python_out=.
```

