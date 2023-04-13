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
make all
```

If everything was successful, the following message will be displayed on the terminal:

```shell
Built fir_accel successfully!
```



# Running on PYNQ Z1 Board

The following output files will be created in the base directory:

```shell
drwxrwxr-x 6 sdr sdr    4096 Nov 14 10:08 .
drwxrwxr-x 6 sdr sdr    4096 Nov 14 10:01 ..
-rw-rw-r-- 1 sdr sdr    1344 Nov 14 10:01 build_bitstream.tcl
-rw-rw-r-- 1 sdr sdr     496 Nov 14 10:01 check_fir_accel.tcl
drwxrwxr-x 8 sdr sdr    4096 Nov 14 10:08 fir_accel
-rw-rw-r-- 1 sdr sdr   47767 Nov 14 10:01 fir_accel_bd.tcl
-rw-rw-r-- 1 sdr sdr 4045677 Nov 14 10:08 fir_accel.bit
-rw-rw-r-- 1 sdr sdr  475114 Nov 14 10:08 fir_accel.hdf
-rw-rw-r-- 1 sdr sdr  299889 Nov 14 10:03 fir_accel.hwh
-rw-rw-r-- 1 sdr sdr  438000 Nov 14 10:01 fir_accel.ipynb
-rw-rw-r-- 1 sdr sdr   12076 Nov 14 10:01 fir_accel.xdc
drwxrwxr-x 8 sdr sdr    4096 Nov 14 10:01 .git
-rw-rw-r-- 1 sdr sdr     951 Nov 14 10:03 makefile
drwxrwxr-x 2 sdr sdr    4096 Nov 14 10:03 NA
-rw-rw-r-- 1 sdr sdr     661 Nov 14 10:01 README.md
-rw-rw-r-- 1 sdr sdr     653 Nov 14 10:03 vivado_26659.backup.jou
-rw-rw-r-- 1 sdr sdr    2848 Nov 14 10:03 vivado_26659.backup.log
-rw-rw-r-- 1 sdr sdr     659 Nov 14 10:03 vivado_26710.backup.jou
-rw-rw-r-- 1 sdr sdr   75406 Nov 14 10:08 vivado_26710.backup.log
-rw-rw-r-- 1 sdr sdr     658 Nov 14 10:08 vivado.jou
-rw-rw-r-- 1 sdr sdr     754 Nov 14 10:08 vivado.log
drwxrwxr-x 2 sdr sdr    4096 Nov 14 10:08 .Xil
```

Now upload the following files to the PYNQ Z1 Board:

```shell
scp fir_accel.bit fir_accel.hdf fir_accel.hdf fir_accel.hwh fir_accel.ipynb xilinx@PYNQ:/home/xilinx/jupyter_notebooks/fir_accel
```

Open a web browser and navigate to the Jupyter Notebook, for example:

```shell
http://PYNQ:9090/notebooks/fir_accel/fir_accel.ipynb
```

Follow the instructions in the notebook
