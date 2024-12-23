cmake_minimum_required(VERSION 3.25 FATAL_ERROR)
# CUDA Standard 17 is only supported by cmake 3.18 and above

project(cudaSamples LANGUAGES CXX CUDA) # CUDA is optional we enable in CUDA section

#includes thrust and cuda runtime libs header file
include_directories(${CMAKE_CUDA_TOOLKIT_INCLUDE_DIRECTORIES})
include_directories(${CMAKE_SOURCE_DIR}/Common)

set(CMAKE_CUDA_STANDARD 17)
set(CMAKE_CUDA_STANDARD_REQUIRED ON)
set(CMAKE_CUDA_EXTENSIONS OFF)
set(CMAKE_CUDA_SEPARABLE_COMPILATION ON)
SET(CMAKE_CUDA_PROPAGATE_HOST_FLAGS ON)
SET(CMAKE_CUDA_VERBOSE_BUILD ON)

# Enable calling constexpr function from device
set(CMAKE_CUDA_FLAGS "${CMAKE_CUDA_FLAGS} --expt-extended-lambda --expt-relaxed-constexpr")

message ("CUDA Architecture: ${CMAKE_CUDA_ARCHITECTURES}")



# List of nvidia samples
set(SAMPLES
    "0_Introduction/c++11_cuda/c++11_cuda.cu"
    "0_Introduction/vectorAdd/vectorAdd.cu"
    "0_Introduction/matrixMul/matrixMul.cu"
    # Add more samples here
)

# Loop through each sample and add executable
foreach(SAMPLE ${SAMPLES})
    get_filename_component(SAMPLE_NAME ${SAMPLE} NAME_WE)
    add_executable(${SAMPLE_NAME} ${CMAKE_SOURCE_DIR}/Samples/${SAMPLE})
endforeach()
