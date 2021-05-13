# XiangShan

XiangShan is a processor targeting super-scalar out-of-order execution.
Currently it supports riscv64GC.

## Compile chisel code

* Install `mill`. Refer to [the Manual section in this guide][mill].
* Run `make init` to init git submodules
* Run `make` to generate verilog code. The output file is `build/TopMain.v`.

[mill]: http://lihaoyi.com/mill#manual

## Run programs by simulation

### Prepare environment

* Set a new environment variable `NEMU_HOME` to the **absolute path** of the NEMU project.
* Set a new environment variable `NOOP_HOME` to the **absolute path** of the XiangShan project.
* Clone the [AM project](https://github.com/NJU-ProjectN/nexus-am.git).
* Set a new environment variable `AM_HOME` to the **absolute path** of the AM project.
* Add a new AM `riscv64-noop` in the AM project if it is not provided.

### Verilator simulation

Install verilator:

TBD

Generate verilog files and compile them using verilator:
* Move to project root, run `make emu` to compile verilator simulator. You can use `make emu config=CONFIG_NAME` to choose different size of XiangShan.
* To speed up compiling, use `make emu REMOTE=YOUR_REMOTE_SERVER`. (If you have remote server setuped)

Run program generated by verilator:
* If compile succeed, you can run the application in the AM project by `make ARCH=riscv64-noop run`.
* Or you can run emulator and select image manually: `./build/emu -i PROGRAM_IMAGE`
* Use parameters to control emulator behavior: `./build/emu [-b DUMP_BEGIN_TIME] [-e DUMP_END_TIME] [--force-dump-result] [--dump-wave] -i PROGRAM_IMAGE`.
* Run `./build/emu` for further instructions.

Example:
```makefile
make emu config=MinimalSimConfig
./build/emu -b 0 -e 0 --force-dump-reult -i ./mem.bin
```

`debug` dir provides some scripts for verilator simulation.

### VCS simulation

Make sure you have VCS installed.

* Run `make simv` to compile vcs simulator.
* After that, run `./simv`