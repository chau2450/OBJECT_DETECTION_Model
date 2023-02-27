cmake_minimum_required(VERSION 3.24)
project(OBJECT_DETECTION)

set(CMAKE_CXX_STANDARD 17)

# Set the path to the TensorFlow C++ API libraries
set(TENSORFLOW_LIB_PATHS
        "/home/ivanbliminse/miniconda3/envs/all_ml/lib/python3.10/site-packages/tensorflow/libtensorflow_framework.so.2"
        "/home/ivanbliminse/miniconda3/envs/main_ml_dl/lib/python3.9/site-packages/tensorflow/libtensorflow_framework.so.2"
        "/home/ivanbliminse/miniconda3/envs/vision_tasks/lib/python3.7/site-packages/tensorflow/libtensorflow_framework.so.2"
        "/home/ivanbliminse/miniconda3/lib/python3.10/site-packages/tensorflow/libtensorflow_framework.so.2"
        "/home/ivanbliminse/miniconda3/pkgs/tensorflow-base-2.4.1-gpu_py39h29c2da4_0/lib/python3.9/site-packages/tensorflow/libtensorflow_framework.so.2"
        "/home/ivanbliminse/miniconda3/pkgs/tensorflow-base-2.4.1-mkl_py37h43e0292_0/lib/python3.7/site-packages/tensorflow/libtensorflow_framework.so.2"
        )

# Find OpenCV and link with TensorFlow
set(OpenCV_DIR "/home/ivanbliminse/miniconda3/envs/vision_tasks/lib/cmake/opencv4")
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})

foreach(TF_LIB_PATH ${TENSORFLOW_LIB_PATHS})
    if(EXISTS ${TF_LIB_PATH})
        message("Found TensorFlow C++ API library at ${TF_LIB_PATH}")
        add_executable(OBJECT_DETECTION main.cpp)
        target_link_libraries(OBJECT_DETECTION ${OpenCV_LIBS} ${TF_LIB_PATH})
        return()
    endif()
endforeach()

message(FATAL_ERROR "Could not find TensorFlow C++ API library")
