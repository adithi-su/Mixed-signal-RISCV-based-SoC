# Mixed-signal-RISCV-based-SoC
Aim: To integrate rvmyth with a PLL (Phase Locked Loop) as a clock multiplier using open-source EDA tools. The whole project focuses on Mixed Signal Physical Design.

## Block design of RVMYTH + PLL
<img src="https://github.com/adithi-su/Mixed-signal-RISCV-based-SoC/blob/master/images/block%20design.png"  width=500px/>
RVMYTH - RISC V Core, test program is loaded into instruction memory. <br>
avsdpll_1v8: PLL designed by <a href="https://www.vlsisystemdesign.com/">VSD</a> works as a multiplier (output_freq = x.input_freq). Depends on the drive strength of the buffers used in designing the PLL.<br>
Generated output frequency is connected to the CLK pin of the processor. The functionality of the setup is tested using RTL and FPGA flows.

## Tools used 
* <a href="https://www.makerchip.com/"> Makerchip </a> is a free web-based IDE as well as available as makerchip-app, a virtual desktop application for developing high-quality integrated circuits. 
* <a href="http://iverilog.icarus.com/"> Icarus Verilog </a> is a Verilog simulation and synthesis tool.
* <a href="http://gtkwave.sourceforge.net/"> GTKWave </a> is a waveform viewer.
* <a href="https://www.xilinx.com/support/university/vivado.html">Xilinx Vivado</a> provides complete SoC-strength, IP-centric and system-centric, next generation development environment. Currently, this project is done using Vivado HL Design Edition 2019.1.

## RTL flow
### Steps to convert TL-Verilog to Verilog/System Verilog
```
pip3 install sandpiper-saas
sandpiper-saas -i design.tlv -o design.sv --iArgs
```
### Steps for RTL Simulation of RVMYTH+PLL using iverilog
```
iverilog rvmyth_pll_tb.v rvmyth_pll.v clk_gate.v
./a.out
gtkwave rvmyth_pll.vcd
```
<p>
<img src="https://github.com/adithi-su/Mixed-signal-RISCV-based-SoC/blob/master/images/gtkwave.png" width=700px>
<br>out[7:0]runs from 0-255, 255-0 and so on.
</p>

<p>
<img src="https://github.com/adithi-su/Mixed-signal-RISCV-based-SoC/blob/master/images/gtkwave%20analog.png" width=700px>
<br>out(analog format) has peak value of 255. 
</p>

## FPGA flow
<img src="https://github.com/adithi-su/Mixed-signal-RISCV-based-SoC/blob/master/images/fpga_block%20design.png" width=500px>
Note: Here, PLL from Xilinx Vivado is used. It converts input frequency of 33 MHz to 100MHz. <br> FPGA board used - Zedboard Zynq-7000 ARM/FPGA SoC Development Board




<!-- refer: https://github.com/shivanishah269/vsdfpga>  
<!-- RISCV Core - https://github.com/shivanishah269/risc-v-core>
<!-- PLL - https://github.com/vsdip/rvmyth_avsdpll_interface>
