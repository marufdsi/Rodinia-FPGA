XILINX_SDACCEL :=/opt/Xilinx/SDAccel/2016.1
XILINX_OPENCL := $(XILINX_SDACCEL)
DSA := xilinx:adm-pcie-7v3:1ddr:3.0
XOCC := $(XILINX_SDACCEL)/bin/xocc
CLFLAGS := -s --xdevice $(DSA)

all : hotspot3D_direct.xclbin \

.PHONY : all

hotspot3D_direct.xclbin: ./hotspot3D_direct.cl
	$(XOCC) $(CLFLAGS) --nk hotspot3D_opt1:1 -k hotspot3D_opt1 --report estimate $< -o $@ ;\
