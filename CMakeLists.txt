cmake_minimum_required(VERSION 3.20)

project(LLVMWheel LANGUAGES C CXX)

add_subdirectory(llvm-project/llvm)


install(DIRECTORY "${CMAKE_INSTALL_PREFIX}/python_packages/mlir_core/mlir/" 
        DESTINATION "${SKBUILD_PLATLIB_DIR}/mlir")
# install(DIRECTORY "${SKBUILD_PLATLIB_DIR}/python_packages/mlir_core/mlir/" 
#         DESTINATION "mlir")

message(STATUS "[CONFIG] after ... ... Register MLIR python install successfully")
