```markdown
# LLVM Wheel Build Guide

This document describes how to build a wheel package from a specific version of llvm-project.

## Quick Start

### 1. Clone the repository
```bash
git clone https://github.com/starrryz/llvm-wheel.git
```

> **Note**: No need to download submodule and `git clone --recursive` unless your version is the same as ours.

### 2. Build the Wheel

```bash
cd llvm-wheel
python -m build -w
```

After building, the `.whl` file will appear in the `./dist` directory.

### 3. Install and Test

```bash
# Install the wheel package (adjust the filename according to the actual one)
pip install ./dist/llvm_wheel-0.1.0-cp312-cp312-linux_x86_64.whl --force-reinstall

# Test import
python -c "import llvm_wheel"
python -c "from mlir import ir"
```

No error is expected.

## Project Structure

Unzip the wheel package, the content is as below:

```
├── llvm_wheel
│   ├── bin
│   ├── include
│   ├── lib
│   ├── python_packages
│   ├── share
│   └── src
├── llvm_wheel-0.1.0.dist-info
└── mlir
    ├── _mlir_libs
    ├── dialects
    ├── extras
    └── runtime
```

## Build Configuration

Our cmake instruction is as below:

```bash
cmake -G Ninja -B build -S llvm \
    -DLLVM_ENABLE_PROJECTS="mlir;llvm;lld" \
    -DLLVM_TARGETS_TO_BUILD="host;NVPTX;AMDGPU" \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_EXPORT_COMPILE_COMMANDS=ON \
    -DCMAKE_C_COMPILER=clang \
    -DCMAKE_CXX_COMPILER=clang++ \
    -DLLVM_ENABLE_LLD=ON \
    -DMLIR_ENABLE_BINDINGS_PYTHON=ON
```

## Customization

You can change the content of `pyproject.toml` to follow your favor.


