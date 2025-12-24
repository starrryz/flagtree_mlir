# aligned with LLVM's CMake setup
cmake_minimum_required(VERSION 3.20.0)

project(LLVMWheel LANGUAGES C CXX)

add_subdirectory(llvm-project/llvm)

install(DIRECTORY "${CMAKE_INSTALL_PREFIX}/python_packages/mlir_core/mlir/" 
        DESTINATION "${SKBUILD_PLATLIB_DIR}/mlir")

message(STATUS "[CONFIG] after ... ... Register MLIR python install")
