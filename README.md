# BigSpicy - Merging SPEF, Verilog and Spice information into Circuit protobuf <br/>
This repo shows the steps for merging the SPEF, verilog and spice netlist into a circuit protobuf. For this step, we need the pdk files in Xyce format.<br/>
To convert any PDK in Xyce format refer the following github repo.<br/>
In this repo, we have used the design of 3-bit ring counter implemented using SKY130 PDKS. The RTL to GDS2 flow of the given design can be referred from the following github repo.<br/>
https://github.com/ArshKedia/iiitb_3bit_rc <br/>

Another prerequisite for this step is to compile protobufs into python file.(_pb2.py).<br/>
To compile the protobufs, follow the below steps:
