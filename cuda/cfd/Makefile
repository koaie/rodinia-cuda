include ../../common/make.config

CC := $(CUDA_DIR)/bin/nvcc

INCLUDE := $(CUDA_DIR)/include

# https://docs.nvidia.com/cuda/cuda-compiler-driver-nvcc/index.html#virtual-architecture-feature-list
SM := compute_60

CC_ARGS := -Xptxas -v -O3 --gpu-architecture=$(SM) --gpu-code=$(SM)

SDK_ARGS := -I$(SDK_DIR)/Common -L$(SDK_DIR)/lib $(CUTIL_LIB)

# Determine the correct version of the cutil library
CUTIL_LIB = # -lcutil
ifeq ($(shell uname -m), x86_64)
     ifeq ($(shell if test -e $(SDK_DIR)/lib/libcutil_x86_64.a; then echo T; else echo F; fi), T)
        CUTIL_LIB = #-lcutil_x86_64
     endif
endif


all: euler3d euler3d_double  pre_euler3d  pre_euler3d_double 

euler3d: euler3d.cu
	$(CC) $(KERNEL_DIM) -O2 -Xptxas -v --gpu-architecture=$(SM) --gpu-code=$(SM) euler3d.cu -o euler3d $(SDK_ARGS)

euler3d_double: euler3d_double.cu
	$(CC) $(CC_ARGS) euler3d_double.cu -o euler3d_double $(SDK_ARGS)


pre_euler3d: pre_euler3d.cu
	$(CC) $(CC_ARGS) pre_euler3d.cu -o pre_euler3d $(SDK_ARGS)

pre_euler3d_double: pre_euler3d_double.cu
	$(CC) $(CC_ARGS) pre_euler3d_double.cu -o pre_euler3d_double $(SDK_ARGS)


clean:
	rm -f euler3d euler3d_double pre_euler3d pre_euler3d_double *.linkinfo
