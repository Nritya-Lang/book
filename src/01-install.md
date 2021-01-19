# Installation

First of all, to install Nritya, your system must meet the prerequisites mentioned in the **README** file [here](https://github.com/Nritya-Lang/Nritya/blob/master/README.md).
The basic installation steps are given in that **README**, but this chapter will describe it to a bit more extent.
Feel free to skip this if you are satisfied with the **README**'s installation procedure.

## Compiler and Virtual Machine

For installing the language compiler, first clone the official GitHub repository: [Nritya-Lang/Nritya](https://github.com/Nritya-Lang/Nritya).
```bash
git clone https://github.com/Nritya-Lang/Nritya
```

Then, `cd` into the directory, create a `build` directory, cd into that, run `cmake ..`, and finally run `make install`.
That will build and install the language interpreter, along with its dynamic libraries.
```bash
cd Nritya && mkdir build && cd build && cmake .. -DCMAKE_BUILD_TYPE=Release && make install
```

Note that you can also specify number of CPU cores using `make -j<number of cores>`. This will greatly improve the build time
of the project. For example, `cmake .. && make -j8 install`

This will generate the Nritya libraries and binaries (as well as the required standard libraries) which can be used to execute Nritya code. The binary which we will use is called `nritya` and it should be generated in `build/bin/` directory of the repository (assuming no `PREFIX_DIR` is set).

You can also install `ccache` to speed up the build process. CMake will autodetect and use it if it finds it.

At this point, you may also want to add the `$PREFIX_DIR/bin` directory in your system's `$PATH` variable to directly use `nritya` command from any directory. Otherwise, you must execute `nritya` as `$PREFIX_DIR/bin/nritya` (replace `$PREFIX_DIR` with actual value).

To run the test suite, execute the command `$PREFIX_DIR/bin/nritya testdir tests` in the Nritya repository directory.

## CMake Environment Variables

### $CXX
This variable is used for specifying the C++ compiler if you do not want to use the ones auto decided by the script which uses `g++` by default for all operating systems except Android and BSD, for which it uses `clang++`.

For example, to explicitly use `clang++` compiler on an ubuntu (linux) machine, you can use:
```bash
CXX=clang++ cmake .. && make install
```

### $PREFIX_DIR
This variable will allow you to set a `PREFIX_DIR` directory for installation of the language after the build.

**NOTE** that once the script is run with a `PREFIX_DIR`, manually moving the generated files to desired directories will not work since the Nritya's codebase uses this `PREFIX_DIR` internally itself.

Generally, the `/usr` or `/usr/local` directories are used for setting the `PREFIX_DIR`, however that is totally up to you. Default value for this is the directory `/usr/local`.

The script will create these directories with respect to `PREFIX_DIR`:
*  `build/bin/nritya` -> `$PREFIX_DIR/bin/`
*  `build/lib/nritya` -> `$PREFIX_DIR/lib/`
*  `include/nritya*` -> `$PREFIX_DIR/include/`

An example usage is:
```bash
PREFIX_DIR=/usr/local cmake .. -DCMAKE_BUILD_TYPE=Release && make install
```
