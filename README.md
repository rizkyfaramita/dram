# DRAM Power Model (DRAMPower)

## Installation

Clone the repository, or download the zip file of the release you would like to use. The source code is available in src folder. To build, use the following:

```bash
make -j4
```

## Required Packages

The tool was verified on Ubuntu 17.10 using:

 * clang

## Usage

```
./ramulator <configs-file> --mode=cpu,dram [--stats <filename>] <trace-filename1> <trace-filename2>
```

An example of using this tool is provided below:

```
./ramulator configs/DDR3-config.cfg --mode=dram --stats my_output.txt dram.trace
```

The output should be something like this:

```
* Parsing memspecs/MICRON_1Gb_DDR3-1066_8bit_G.xml
* Analysis start time: Thu Aug  4 15:43:52 2016
* Analyzing the input trace
* Trace Details:

#ACT commands: 96984
#RD + #RDA commands: 67179
#WR + #WRA commands: 29805
#PRE (+ PREA) commands: 96984
#REF commands: 13168
#Active Cycles: 2519793
  #Active Idle Cycles: 196851
  #Active Power-Up Cycles: 0
    #Auto-Refresh Active cycles during Self-Refresh Power-Up: 0
#Precharged Cycles: 52261474
  #Precharged Idle Cycles: 51649629
  #Precharged Power-Up Cycles: 0
    #Auto-Refresh Precharged cycles during Self-Refresh Power-Up: 0
  #Self-Refresh Power-Up Cycles: 0
Total Idle Cycles (Active + Precharged): 51846480
#Power-Downs: 0
  #Active Fast-exit Power-Downs: 0
  #Active Slow-exit Power-Downs: 0
  #Precharged Fast-exit Power-Downs: 0
  #Precharged Slow-exit Power-Downs: 0
#Power-Down Cycles: 0
  #Active Fast-exit Power-Down Cycles: 0
  #Active Slow-exit Power-Down Cycles: 0
    #Auto-Refresh Active cycles during Self-Refresh: 0
  #Precharged Fast-exit Power-Down Cycles: 0
  #Precharged Slow-exit Power-Down Cycles: 0
    #Auto-Refresh Precharged cycles during Self-Refresh: 0
#Auto-Refresh Cycles: 776912
#Self-Refreshes: 0
#Self-Refresh Cycles: 0
----------------------------------------
Total Trace Length (clock cycles): 54781267
----------------------------------------

* Trace Power and Energy Estimates:

ACT Cmd Energy: 109175234.52 pJ
PRE Cmd Energy: 47764165.10 pJ
RD Cmd Energy: 49155365.85 pJ
WR Cmd Energy: 23486116.32 pJRD I/O Energy: 20872124.58 pJ
WR Termination Energy: 47419587.24 pJ
ACT Stdby Energy: 283653996.25 pJ
  Active Idle Energy: 22159587.24 pJ
  Active Power-Up Energy: 0.00 pJ
    Active Stdby Energy during Auto-Refresh cycles in Self-Refresh Power-Up: 0.00 pJ
PRE Stdby Energy: 5147706163.23 pJ
  Precharge Idle Energy: 5087440004.69 pJ
  Precharged Power-Up Energy: 0.00 pJ
    Precharge Stdby Energy during Auto-Refresh cycles in Self-Refresh Power-Up: 0.00 pJ
  Self-Refresh Power-Up Energy: 0.00 pJ
Total Idle Energy (Active + Precharged): 5109599591.93 pJ
Total Power-Down Energy: 0.00 pJ
  Fast-Exit Active Power-Down Energy: 0.00 pJ
  Slow-Exit Active Power-Down Energy: 0.00 pJ
    Slow-Exit Active Power-Down Energy during Auto-Refresh cycles in Self-Refresh: 0.00 pJ
  Fast-Exit Precharged Power-Down Energy: 0.00 pJ
  Slow-Exit Precharged Power-Down Energy: 0.00 pJ
    Slow-Exit Precharged Power-Down Energy during Auto-Refresh cycles in Self-Refresh: 0.00 pJ
Auto-Refresh Energy: 262371782.36 pJ
Self-Refresh Energy: 0.00 pJ
----------------------------------------
Total Trace Energy: 5991604535.46 pJ
Average Power: 58.30 mW
----------------------------------------
* Power Computation End time: Thu Aug  4 15:43:59 2016
* Total Simulation time: 7 seconds
*
```

As can be noticed, the tool performs DRAM command scheduling and reports the energy consumption of its components. Besides, the IO and Termination components in pJ (pico Joules) and the average power consumption of the trace in mW. It also reports the simulation start/end times and the total simulation time in seconds.

## Authors & Acknowledgment

The tool is based on the prior works in DRAM developed by research group at Carnegie Mellon University.

**Paper**
```
[1] A Case for Exploiting Subarray-Level Parallelism (SALP) in DRAM
Yoongu Kim, Vivek Seshadri, Donghyuk Lee, Jamie Liu, Onur Mutlu
URL: https://users.ece.cmu.edu/~omutlu/pub/salp-dram_isca12.pdf
```

**DRAM Simulator**
```
[2] Ramulator: A DRAM Simulator
Yoongu Kim, Weikun Yang, Kevin Chang, Donghyuk Lee, Vivek Seshadri, Saugata Ghose, Tianshi Li
URL: https://github.com/CMU-SAFARI/ramulator
```

**DRAM power model:**
```
[3] "System and Circuit Level Power Modeling of Energy-Efficient 3D-Stacked Wide I/O DRAMs"
Karthik Chandrasekar, Christian Weis, Benny Akesson, Norbert Wehn, and Kees Goossens
In Proc. Design, Automation and Test in Europe (DATE), 2013
```

## Disclaimer

The tool does not check the timing accuracy of the user's memory. This only employs a DRAM memory simulator, which
satisfies all memory timing constraints and other requirements.