# llvmSetup
How to set up llvm

Add the GPG key: `wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key|sudo apt-key add -`

Go to [apt page](https://apt.llvm.org/) and copy relevant `deb ... main` command.

Run:

```sh
sudo add-apt-repository 'deb ... main'
```
Do the same for `deb-src ... main`.

Run commands to install everything:

```sh
sudo apt-get install libllvm-10-ocaml-dev libllvm10 llvm-10 llvm-10-dev llvm-10-doc llvm-10-examples llvm-10-runtime
sudo apt-get install clang-10 clang-tools-10 clang-10-doc libclang-common-10-dev libclang-10-dev libclang1-10 clang-format-10 python-clang-10 clangd-10 
sudo apt-get install libfuzzer-10-dev
sudo apt-get install lldb-10
sudo apt-get install lld-10
sudo apt-get install libc++-10-dev libc++abi-10-dev
sudo apt-get install libomp-10-dev
sudo apt-get install clang-format clang-tidy clang-tools clang clangd libc++-dev libc++1 libc++abi-dev libc++abi1 libclang-dev libclang1 liblldb-dev libllvm-ocaml-dev libomp-dev libomp5 lld lldb llvm-dev llvm-runtime llvm python-clang 
```

Maybe install `python3-clang-10` instead of `python-clang-10`.

Assume we want to compile C++ code with includes like in the [Kaleidoscope tutorial](https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/):

```c++
#include "llvm/ADT/APFloat.h"
#include "llvm/ADT/STLExtras.h"
#include "llvm/IR/BasicBlock.h"
#include "llvm/IR/Constants.h"
#include "llvm/IR/DerivedTypes.h"
#include "llvm/IR/Function.h"
#include "llvm/IR/IRBuilder.h"
#include "llvm/IR/Instructions.h"
#include "llvm/IR/LLVMContext.h"
#include "llvm/IR/LegacyPassManager.h"
#include "llvm/IR/Module.h"
#include "llvm/IR/Type.h"
#include "llvm/IR/Verifier.h"
#include "llvm/Support/TargetSelect.h"
#include "llvm/Target/TargetMachine.h"
#include "llvm/Transforms/InstCombine/InstCombine.h"
#include "llvm/Transforms/Scalar.h"
#include "llvm/Transforms/Scalar/GVN.h"
#include <algorithm>
#include <cassert>
#include <cctype>
#include <cstdint>
#include <cstdio>
#include <cstdlib>
#include <map>
#include <memory>
#include <string>
#include <vector>

using namespace llvm;
using namespace llvm::orc;
```

We can use a simple script like:

```sh
cpp=${1:-toy.cpp}
out=${2:-${cpp%.cpp}.out}

clang++ -g -O3 $cpp `llvm-config --cxxflags --ldflags --system-libs --libs core` -fno-rtti -rdynamic -o $out
```
