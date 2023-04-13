# Introduction

This project is based on FPGA Developer's project [How to accelerate a Python function with PYNQ](https://www.fpgadeveloper.com/2018/03/how-to-accelerate-a-python-function-with-pynq.html/).  

The following modification to the original project: 

- Retargeted design for the [Kria KR206 Board](https://www.xilinx.com/products/som/kria/kr260-robotics-starter-kit.html)

- Upgraded the project for **PYNQ Version 3.0** using **Xilinx Vivado 2022.1**

- Updated the Jupyter Notebook to use memory buffers created by `allocate` DMA library.
  - Read The Docs: https://pynq.readthedocs.io/en/v2.5/pynq_libraries/dma.html
  
- Created a `makefile` similar to the base design in the [PYNQ Z1 repository](https://github.com/odelayIO/PYNQ-Z1-FIR-Acceleration/tree/vivado-2022.1)

  



# Building Overlay

This project uses the Vivado 2022.1 Docker Container from [odelayIO/vivado2022.1_docker](odelayIO/vivado2022.1_docker) repository.  Once the Docker container is created, just execute the run file.  See repository for instructions how to modify the [run.sh](https://github.com/odelayIO/vivado2022.1_docker/blob/master/run.sh) script

```shell
./vivado2022.1_docker/run.sh
```

Clone repo and build project:

```shell
git clone https://github.com/odelayIO/PYNQ-Z1-FIR-Acceleration.git
cd PYNQ-Z1-FIR-Acceleration
make
```

If everything was successful, the following message will be displayed on the terminal:

```shell
Built fir_accel successfully!
```





# Running on the KR260 Board

The following output files will be created in the base directory:

```shell
total 9792
drwxrwxr-x 5 sdr sdr    4096 Apr 13 04:20 .
drwxrwxr-x 6 sdr sdr    4096 Apr 13 04:06 ..
drwxr-xr-x 2 sdr sdr    4096 Apr 13 04:20 .Xil
drwxrwxr-x 8 sdr sdr    4096 Apr 13 04:09 .git
-rw-rw-r-- 1 sdr sdr    3502 Apr 13 04:13 README.md
-rwxrwxr-- 1 sdr sdr    1261 Apr 13 04:08 build_bitstream.tcl
-rwxrwxr-- 1 sdr sdr     508 Apr 13 04:08 check_kr260_fir_accel.tcl
drwxr-xr-x 8 sdr sdr    4096 Apr 13 04:12 kr260_fir_accel
-rw-r--r-- 1 sdr sdr 7797819 Apr 13 04:20 kr260_fir_accel.bit
-rw-r--r-- 1 sdr sdr  349505 Apr 13 04:12 kr260_fir_accel.hwh
-rwxr--r-- 1 sdr sdr  104545 Apr 13 04:08 kr260_fir_accel.ipynb
-rw-r--r-- 1 sdr sdr 1554715 Apr 13 04:20 kr260_fir_accel.xsa
-rw-rwxr-- 1 sdr sdr   55553 Apr 13 04:08 kr260_fir_accel_bd.tcl
-rwxrwxr-- 1 sdr sdr     947 Apr 13 04:08 makefile
-rw-r--r-- 1 sdr sdr     815 Apr 13 04:20 vivado.jou
-rw-r--r-- 1 sdr sdr     911 Apr 13 04:20 vivado.log
-rw-r--r-- 1 sdr sdr     801 Apr 13 04:11 vivado_123.backup.jou
-rw-r--r-- 1 sdr sdr   84943 Apr 13 04:20 vivado_123.backup.log
-rw-r--r-- 1 sdr sdr     806 Apr 13 04:10 vivado_83.backup.jou
-rw-r--r-- 1 sdr sdr    8194 Apr 13 04:11 vivado_83.backup.log

```

Now upload the following files to the KR260 Board:

```shell
make upload
```

Open a web browser and navigate to the Jupyter Notebook, for example:

http://kria:9090/lab/tree/kr260_fir_accel/kr260_fir_accel.ipynb

Follow the instructions in the notebook
