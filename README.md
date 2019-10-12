# Cube

```text
 ______
< Cube >
 ------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

`Cube` is an RPC framework for CUDA runtime. I decided to initiate this project for two main reasons. Firstly, I aim at an open implementation for such a framework. Secondly, I believe it can be better than alternatives or deserves a try. For now, I work on the project on my spare time and would welcome any help. The target operating system and runtime are `Windows` and `CUDA 10` for now.

## How CUDA API works?

This section includes my findings on how the CUDA runtime is linked with `PE` files and how the APIs are called.

### vectorAdd

Here are the observations regarding the analysis of `vectorAdd.exe` of CUDA SDK samples.

`Dependency Walker` shows dependence on `kernel32.dll` only. This indicate the possibility for a `static` linkage with the runtime. The corresponding `VS` project investigated and it turned out that the `/MT` flag for a static linkage is set.  

`Process Monitor` shows calls to two `NVIDIA` DLLs located in `System32`. The files are `nvcuda.dll` and `nvfatbinary.dll`.