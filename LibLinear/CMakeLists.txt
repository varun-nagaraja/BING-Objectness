#Do not include files (from libraries) with a main function to avoid conflict 
#with the main function in the project.
set(LIBLINEAR_LIST linear.cpp tron.cpp) 
set(BLAS_LIST blas/daxpy.c blas/ddot.c blas/dnrm2.c blas/dscal.c) 
add_library(LIBLINEAR ${LIBLINEAR_LIST})
add_library(BLAS ${BLAS_LIST})
