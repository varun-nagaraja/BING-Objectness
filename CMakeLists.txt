project(BING)
cmake_minimum_required(VERSION 2.8)

find_package(OpenMP REQUIRED)

#Do not include files (from libraries) with a main function to avoid conflict 
#with the main function in the project.
set(LIBLINEAR_LIST LibLinear/linear.cpp LibLinear/linear.h LibLinear/tron.cpp LibLinear/tron.h)
set(BLAS_LIST LibLinear/blas/blas.h LibLinear/blas/blasp.h LibLinear/blas/daxpy.c LibLinear/blas/ddot.c LibLinear/blas/dnrm2.c LibLinear/blas/dscal.c)
add_library(LIBLINEAR ${LIBLINEAR_LIST})
add_library(BLAS ${BLAS_LIST})

#set(CMAKE_CXX_FLAGS "-fopenmp")
list( APPEND CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fopenmp -ftree-vectorize")

#Modify the opencv directory as required
#set(OPENCV_DIR /usr/local/stow/opencv-2.4.2-gcc460)
include_directories(/usr/local/include) # ${OPENCV_DIR}/include)
link_directories(/usr/local/lib) # ${OPENCV_DIR}/lib)

file(GLOB SRC_LIST Objectness/*.cpp Objectness/*.h)
add_executable(${PROJECT_NAME} ${SRC_LIST} ${LIBLINEAR_LIST} ${BLAS_LIST})
target_link_libraries(${PROJECT_NAME} opencv_highgui opencv_core opencv_imgproc ${EXTERNAL_LIBS})
