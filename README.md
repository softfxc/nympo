# nympo
This README summarizes the current build for the Nympo project, including external prerequisites and embedded resources

 A. What Nympo currently does

Nympo is a unified CLI that can:

- pack files or directories
- unpack archives
- list archive contents
- test archive integrity
- wrap external tools such as xtool and arc
- embed external helper tools from resources/ into the final executable
- extract embedded helper tools at runtime to the user temp directory under Nympo/Tools
- generate launchers after packing

 B. Embedded resources

Nympo embeds every file found under resources/ and in runtime, embedded tools are materialized to:
%LOCALAPPDATA%\Temp\Nympo\Tools\
This is the Windows temp directory for the current user:
C:\Users\<USER>\AppData\Local\Temp\Nympo\Tools\

 C. Required build dependencies

1. Visual Studio 2026 Community (or Build Tools) with Desktop development with C++
2. CMake
3. Python 3
4. vcpkg & OpenSSL
5. Git

 D. Official download pages

- Visual Studio Community: https://visualstudio.microsoft.com/vs/community/
- Visual Studio downloads overview: https://visualstudio.microsoft.com/downloads/
- C++ workload docs: https://learn.microsoft.com/en-us/cpp/build/vscpp-step-0-installation?view=msvc-170
- CMake download page: https://cmake.org/download/
- Python downloads: https://www.python.org/downloads/
- Python Windows downloads: https://www.python.org/downloads/windows/
- vcpkg repository: https://github.com/microsoft/vcpkg
- vcpkg CMake integration docs: https://learn.microsoft.com/en-us/vcpkg/users/buildsystems/cmake-integration
- vcpkg install command docs: https://learn.microsoft.com/en-us/vcpkg/commands/install
- Git for Windows: https://git-scm.com/install/windows

   External tool pages

- 7-Zip download page: https://www.7-zip.org/download.html
- Zstandard releases: https://github.com/facebook/zstd/releases
- bzip3 releases: https://github.com/iczelia/bzip3/releases
- cmix repository: https://github.com/byronknoll/cmix
- paq8px repository: https://github.com/hxim/paq8px
- lrzip releases: https://github.com/ckolivas/lrzip/releases
- lrzip-next releases: https://github.com/pete4abw/lrzip-next/releases
- NNCP: https://github.com/fire/pytorch-nncp
- Xtool with Freearc: https://github.com/Masquerade64/XTool_2020_Archive

 E. Install prerequisites

* Install Visual Studio

Install Visual Studio 2026 Community and select: Desktop development with C++

* Install CMake

Install the current Windows x64 release of CMake.

* Install Python

Install a current Python 3 x64 build for Windows.

* Install Git

Install Git for Windows if you want to clone vcpkg with `git clone`.

* Install vcpkg

 Clone with Git

cd C:\
git clone https://github.com/microsoft/vcpkg C:\vcpkg
C:\vcpkg\bootstrap-vcpkg.bat


 F. Install Nympo library dependencies with vcpkg

C:\vcpkg\vcpkg install openssl:x64-windows liblzma:x64-windows

 G. Put tools into `resources/`

Everything under Nympo/resources/ is embedded into the final executable, like this:

Nympo/
  resources/
zlib1.dll
libnc.dll
libnc_cuda.dll
libwinpthread-1.dll
    7z.exe
    7z.dll
    Arc.exe
    zstd.exe
    bzip3.exe
    cmix.exe
    paq8px.exe
    nncp.exe
    xtool.exe
The Cygwin DLLs are required for "lrzip.exe" to work.
# Getting the Cygwin DLLs required by `lrzip.exe`

https://cygwin.com/install.html

`lrzip.exe` is a Cygwin-built binary, so it needs the Cygwin runtime and a small set of companion DLLs to run.

1. Download the 64-bit Cygwin installer: `setup-x86_64.exe`.
2. Run the installer.
3. When the package selection screen appears, install these packages:

   * `cygwin`
   * `libbz2_1`
   * `liblzo2_2`
   * `zlib0`
   * `libgcc1`
   * `libstdc++6`
   * `libiconv2`
   * `libintl8`

 After installation, copy the required DLLs from: C:\cygwin64\bin into: Nympo\resources, DLLs you will need are:

* `cygwin1.dll`
* `cygbz2-1.dll`
* `cyglzo2-2.dll`
* `cygz.dll`
* `cyggcc_s-seh-1.dll`
* `cygstdc++-6.dll`
* `cygiconv-2.dll`
* `cygintl-8.dll`


 H. Clean build commands

Open a normal `cmd` or a Developer Command Prompt and go to the project root.

cmake -S . -B build -G "Visual Studio 18 2026" -A x64 ^
  -DCMAKE_TOOLCHAIN_FILE=C:/vcpkg/scripts/buildsystems/vcpkg.cmake ^
  -DVCPKG_TARGET_TRIPLET=x64-windows

cmake --build build --config Release -j

 I. Expected build output

Dinamic output:

build\Release\nympo.exe
build\Release\libcrypto-3-x64.dll
build\Release\liblzma.dll

 J. Current CLI summary

Useful commands:

nympo
nympo pack <input> <output-dir> [options]
nympo unpack <first-part-or-dir> <output> [options]
nympo list <first-part-or-dir>
nympo test <first-part-or-dir> [options]
nympo tool <program> [args...]
nympo xtool [args...]
nympo arc [args...]

Aliases are also supported, including `c`, `d`, `x`, `l`, `t`, and `run`.
