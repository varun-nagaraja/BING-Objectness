#Do not include files (from libraries) with a main function to avoid conflict 
#with the main function in the project.
add_library(liblinear linear.cpp tron.cpp)
add_library(blas blas/daxpy.c blas/ddot.c blas/dnrm2.c blas/dscal.c)
