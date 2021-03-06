include ../../common/make.config

C_C = gcc
OCL_LIB = -lOpenCL

# ====================================================================================================100
#	NVCC
# ====================================================================================================100

# CUD_C = nvcc
# OMP_FLAG = 	-Xcompiler paste_one_here

# ====================================================================================================100
#	PGCC
# ====================================================================================================100

# C_C = pgcc
# OMP_FLAG = -mp
# ACC_FLAG = 	-ta=nvidia \
			# -Minfo \
			# -Mbounds

# ====================================================================================================100
#	END
# ====================================================================================================100

# ======================================================================================================================================================150
#	END
# ======================================================================================================================================================150

# ========================================================================================================================================================================================================200
#	EXECUTABLES (LINK OBJECTS TOGETHER INTO BINARY)
# ========================================================================================================================================================================================================200

all: b+tree_gpu.exe \
     b+tree_fpga.exe

b+tree_gpu.exe:	./main.o \
		./kernel/kernel_gpu_opencl_wrapper.o \
		./kernel/kernel_gpu_opencl_wrapper_2.o \
		./util/timer/timer.o \
		./util/num/num.o \
		./util/opencl/opencl.o
	$(C_C)	./main.o \
			./kernel/kernel_gpu_opencl_wrapper.o \
			./kernel/kernel_gpu_opencl_wrapper_2.o \
			./util/timer/timer.o \
			./util/num/num.o \
			./util/opencl/opencl.o \
			-lm \
			-L$(OPENCL_LIB) \
			-lOpenCL \
	                -o $@

b+tree_fpga.exe:	./main.o \
		./kernel_fpga/kernel_fpga_opencl_wrapper.o \
		./kernel_fpga/kernel_fpga_opencl_wrapper_2.o \
		./util/timer/timer.o \
		./util/num/num.o \
		./util/opencl/opencl.o
	$(C_C)	./main.o \
			./kernel_fpga/kernel_fpga_opencl_wrapper.o \
			./kernel_fpga/kernel_fpga_opencl_wrapper_2.o \
			./util/timer/timer.o \
			./util/num/num.o \
			./util/opencl/opencl.o \
			-lm \
			-L$(OPENCL_LIB) \
			-lOpenCL \
	                -o $@
# ========================================================================================================================================================================================================200
#	OBJECTS (COMPILE SOURCE FILES INTO OBJECTS)
# ========================================================================================================================================================================================================200

# ======================================================================================================================================================150
#	MAIN FUNCTION
# ======================================================================================================================================================150

main.o:	./common.h \
		./main.h \
		./main.c
	$(C_C)	$(KERNEL_DIM) ./main.c \
			-c \
			-o ./main.o \
			-O3

# ======================================================================================================================================================150
#   GPU	KERNELS
# ======================================================================================================================================================150

./kernel/kernel_gpu_opencl_wrapper.o:	./common.h \
										./kernel/kernel_gpu_opencl_wrapper.h \
										./kernel/kernel_gpu_opencl_wrapper.c
	$(C_C)	$(KERNEL_DIM) ./kernel/kernel_gpu_opencl_wrapper.c \
			-c \
			-o ./kernel/kernel_gpu_opencl_wrapper.o \
			-O3 \
			-I$(OPENCL_INC)

./kernel/kernel_gpu_opencl_wrapper_2.o:	./common.h \
										./kernel/kernel_gpu_opencl_wrapper_2.h \
										./kernel/kernel_gpu_opencl_wrapper_2.c
	$(C_C)	$(KERNEL_DIM) ./kernel/kernel_gpu_opencl_wrapper_2.c \
			-c \
			-o ./kernel/kernel_gpu_opencl_wrapper_2.o \
			-O3 \
			-I$(OPENCL_INC)

# ======================================================================================================================================================150
#   FPGA KERNELS
# ======================================================================================================================================================150

./kernel_fpga/kernel_fpga_opencl_wrapper.o:	./common.h \
										./kernel_fpga/kernel_fpga_opencl_wrapper.h \
										./kernel_fpga/kernel_fpga_opencl_wrapper.c
	$(C_C)	$(KERNEL_DIM) ./kernel_fpga/kernel_fpga_opencl_wrapper.c \
			-c \
			-o ./kernel_fpga/kernel_fpga_opencl_wrapper.o \
			-O3 \
			-I$(OPENCL_INC)

./kernel_fpga/kernel_fpga_opencl_wrapper_2.o:	./common.h \
										./kernel_fpga/kernel_fpga_opencl_wrapper_2.h \
										./kernel_fpga/kernel_fpga_opencl_wrapper_2.c
	$(C_C)	$(KERNEL_DIM) ./kernel_fpga/kernel_fpga_opencl_wrapper_2.c \
			-c \
			-o ./kernel_fpga/kernel_fpga_opencl_wrapper_2.o \
			-O3 \
			-I$(OPENCL_INC)

# ======================================================================================================================================================150
#	UTILITIES
# ======================================================================================================================================================150

./util/timer/timer.o:	./common.h \
						./util/timer/timer.h \
						./util/timer/timer.c
	$(C_C)	./util/timer/timer.c \
			-c \
			-o ./util/timer/timer.o \
			-O3

./util/num/num.o:	./common.h \
					./util/num/num.h \
					./util/num/num.c
	$(C_C)	./util/num/num.c \
			-c \
			-o ./util/num/num.o \
			-O3

./util/opencl/opencl.o:	./common.h \
						./util/opencl/opencl.h \
						./util/opencl/opencl.c
	$(C_C)	./util/opencl/opencl.c \
			-c \
			-o ./util/opencl/opencl.o \
			-O3 \
			-I$(OPENCL_INC)

# ======================================================================================================================================================150
#	END
# ======================================================================================================================================================150

# ========================================================================================================================================================================================================200
#	DELETE
# ========================================================================================================================================================================================================200

clean:
	rm	*.o *.exe \
		./kernel/*.o \
		./util/timer/*.o \
		./util/num/*.o \
		./util/opencl/*.o \
                output.txt
# ========================================================================================================================================================================================================200
#	END
# ========================================================================================================================================================================================================200
