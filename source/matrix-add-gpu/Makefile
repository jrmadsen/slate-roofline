all: checkEnv clean matrix_add

.PHONY: checkEnv clean

PAPI_INCLUDE_OPTS= -I/global/common/software/m1759/papi/papi-20201116hacked/include
PAPI_POST_LINK_OPTS= -L/global/common/software/m1759/papi/papi-20201116hacked/lib -lpapi -lpfm

#module purge; module load cgpu; module load gcc/8.3.0 ; module load cuda/11.0.3; module load openmpi/4.0.3
#export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/global/common/software/m1759/papi/papi-20201116hacked/lib

matrix_add: matrix_add.cu
	nvcc matrix_add.cu -o matrix_add_pinned_papi -I${OPENMPI_DIR}/include -I${CUDA_ROOT}/include ${PAPI_INCLUDE_OPTS} -L${OPENMPI_DIR}/lib -L${CUDA_ROOT}/lib64 ${PAPI_POST_LINK_OPTS} -lmpi -lcudart -DPROFILING -DPAPI -DPINNED
	nvcc matrix_add.cu -o matrix_add_papi -I${OPENMPI_DIR}/include -I${CUDA_ROOT}/include ${PAPI_INCLUDE_OPTS} -L${OPENMPI_DIR}/lib -L${CUDA_ROOT}/lib64 ${PAPI_POST_LINK_OPTS} -lmpi -lcudart -DPROFILING -DPAPI 
	nvcc matrix_add.cu -o matrix_add_pinned -I${OPENMPI_DIR}/include -I${CUDA_ROOT}/include ${PAPI_INCLUDE_OPTS} -L${OPENMPI_DIR}/lib -L${CUDA_ROOT}/lib64 ${PAPI_POST_LINK_OPTS} -lmpi -lcudart -DPROFILING -DPINNED
	nvcc matrix_add.cu -o matrix_add -I${OPENMPI_DIR}/include -I${CUDA_ROOT}/include ${PAPI_INCLUDE_OPTS} -L${OPENMPI_DIR}/lib -L${CUDA_ROOT}/lib64 ${PAPI_POST_LINK_OPTS} -lmpi -lcudart -DPROFILING

checkEnv:
ifndef CUDA_VERSION
	$(Error: cuda module not loaded)
endif
ifndef GCC_VERSION
	$(Error: gcc module not loaded)
endif

clean:
	rm -f matrix_add_pinned_papi matrix_add_papi matrix_add_pinned matrix_add 
