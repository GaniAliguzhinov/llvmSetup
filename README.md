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
