cmake_minimum_required(VERSION 3.20)

# 关键：LLVM 是顶级项目
project(LLVMWheel LANGUAGES C CXX)

# 直接把控制权交给 LLVM 官方构建系统, install的权限也给它了
add_subdirectory(llvm-project/llvm)


# install 对应的mlir  DIRECTORY是install的目录，destination会destination/directory,拼起来
# remain issues 
# install的东西在一个临时目录里，随机命名且会被删掉，准备测试单独构建的不走cmake能不能install成功，但是install pip卡住了
# 准备用环境变量，但是环境变量configure的时间更早？没设置也可以我寻思，
# 不用环境变量就只能写死install的目录了，感觉还是环境变量更好一点

# export SCIKIT_BUILD_TEMP=/tmp/my-scikit-build-648648648648648648

message(STATUS "SKBUILD_PLATLIB_DIR = ${SKBUILD_PLATLIB_DIR}")
message(STATUS "[CONFIG] Register MLIR python install")
message(STATUS "Will install MLIR python from:")
message(STATUS "  ${CMAKE_INSTALL_PREFIX}/python_packages/mlir_core/mlir/")
message(STATUS "Into:")
message(STATUS "  ${SKBUILD_PLATLIB_DIR}/mlir")

install(DIRECTORY "${CMAKE_INSTALL_PREFIX}/python_packages/mlir_core/mlir/" 
        DESTINATION "${SKBUILD_PLATLIB_DIR}/mlir")
# install(DIRECTORY "${SKBUILD_PLATLIB_DIR}/python_packages/mlir_core/mlir/" 
#         DESTINATION "mlir")

message(STATUS "[CONFIG] after ... ... Register MLIR python install")
