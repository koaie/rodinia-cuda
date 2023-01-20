include ../../common/make.config

CC := $(CUDA_DIR)/bin/nvcc

INCLUDE := $(CUDA_DIR)/include

ifdef OUTPUT
override OUTPUT = -DOUTPUT
endif

# link objects(binaries) together
heartwall: main.o ./AVI/avilib.o ./AVI/avimod.o 
	$(CC) main.o ./AVI/avilib.o ./AVI/avimod.o -I $(INCLUDE) -lm -o heartwall

# compile main function file into object (binary)
main.o: main.cu kernel.cu define.c
	$(CC) $(OUTPUT) $(KERNEL_DIM) main.cu -I./AVI -c -O3

./AVI/avilib.o ./AVI/avimod.o:
	cd AVI; make;

# delete all object files
clean:
	rm -f *.o AVI/*.o heartwall *.linkinfo
