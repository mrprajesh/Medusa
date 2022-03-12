CUDA_SDK_PATH :=/usr/local/cuda-9.2
CUDPP_PATH := ../cudpp-2.0
OPT=-O3
CFLAGS=$(OPT) -c -w -fopenmp -lgomp
INCLUDES :=  -I$(CUDA_SDK_PATH)/samples/common/inc -I../cudpp-2.0/include
CULIBS := -L$(CUDA_SDK_PATH)/samples/lib -lcutil_x86_64 -L/lib -lcudpp
NVFLAGS=$(OPT) -arch=sm_50 $(INCLUDES)
LDFLAGS=$(OPT) $(CULIBS)
CC=g++ -Wcpp
NVCC=/usr/local/cuda-9.2/bin/nvcc -Xcompiler -fopenmp
LD=/usr/local/cuda-9.2/bin/nvcc  -lgomp -lpthread
OBJS=main.o CPUFunctorHoster.o MessageDataType.o VertexDataType.o EdgeDataType.o\
../MedusaRT/Combiner.o  ../MedusaRT/GraphConverter.o  ../MedusaRT/GraphRenderingAPI.o    ../MedusaRT/OpenglSettings.o  ../MedusaRT/Utilities.o \
../MedusaRT/GraphGenerator.o  ../MedusaRT/GraphStorage.o         ../MedusaRT/PublicAPI.o \
 ../MedusaRT/CUDAOpenglInterop.o  ../MedusaRT/GraphReader.o    ../MedusaRT/MessageArrayManager.o  ../MedusaRT/SystemLibCPU.o ../MultipleGPU/PartitionManager.o ../MultipleGPU/MultiGraphStorage.o \
../MultipleGPU/WEQueue.o ../Tools/ReplicaNumberAnalysis.o ../Tools/RegularityAnalysis.o

.PHONY: test
test: $(OBJS)
	$(LD) $(LDFLAGS) -o test $(OBJS)
%.o : %.cxx
	$(CC) $(CFLAGS) -c $< -o $*.o
.cpp.o :
	$(NVCC) $(NVFLAGS) -c $< -o $*.o
%.o : %.cu
	$(NVCC) $(NVFLAGS) -c $< -o $*.o
clean:
	-rm test $(OBJS)

