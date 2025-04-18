> [!IMPORTANT]
> Seeking input about the ongoing maintenance and future shape of the project. Please provide any thoughts and suggestions in issue [#114](https://github.com/bbc/bmx/issues/114)

# bmx Library and Utilities

bmx is a library and set of utilities to read and write the [SMPTE ST 377-1 MXF file format](https://ieeexplore.ieee.org/document/7292073).

bmx is used to support standardisation efforts in the broadcast industry. It provides utilities for creating standard compliant sample files. It serves as an example implementation for MXF file format standards.

bmx includes the [libMXF](./deps/libMXF) low-level MXF C library and the [libMXF++](./deps/libMXFpp) C++ wrapper library.

bmx provides a set of commandline applications:

* **raw2bmx**: create MXF files from raw essence files
* **bmxtranswrap**: re-wrap from one MXF file to another MXF file
* **mxf2raw**: output MXF file metadata and raw essence
* **bmxparse**: text dump raw essence files using the bmx library's parser class

bmx provides a set of file format text dumper and essence extraction tools:

* **h264dump**: text dump raw H.264 bitstream files
* **j2cdump**: text dump raw JPEG 2000 codestreams
* **jp2extract**: extract JPEG 2000 codestream from a JP2 file (ISO/IEC 15444-1 / ITU T.800 Annex I)
* **movdump**: text dump Quicktime / MP4 files
* **rdd36dump**: text dump SMPTE RDD 36 (Apple ProRes) bitstream files
* **vc2dump**:  text dump SMPTE ST 2042 VC-2 bitstream files
* **MXFDump**: text dumper for MXF files from the [AAF SDK](https://sourceforge.net/projects/aaf/). This utility is made available and built as part of [libMXF](./deps/libMXF).

The following input and output wrapper formats and flavours are supported:

* [AMWA AS-02](https://www.amwa.tv/specifications) MXF Versioning
* [AMWA AS-10](https://www.amwa.tv/specifications) MXF for Production
* [AMWA AS-11](https://www.amwa.tv/specifications) Media Contribution File Formats (MXF)
* [SMPTE ST 378](https://ieeexplore.ieee.org/document/7291764) MXF OP1a
* [SMPTE RDD 9](https://ieeexplore.ieee.org/document/7290714) MXF MPEG Long GOP (Sony XDCAM)
* [SMPTE ST 386](https://ieeexplore.ieee.org/document/7291350) MXF D-10 (Sony MPEG IMX)
* [SMPTE ST 2067-5](https://ieeexplore.ieee.org/document/9099734) Interoperable Master Format (IMF) - Essence Component
* [Avid native MXF OPAtom](https://www.avid.com/static/resources/common/documents/mxf.pdf)
* [WAV](https://en.wikipedia.org/wiki/WAV)

The following essence formats are supported:

* [SMPTE RP 2027](https://ieeexplore.ieee.org/document/7290936) AVC-Intra video, class 50 / 100 / 200
* [SMPTE ST 356](https://ieeexplore.ieee.org/document/7290684) D-10 video, 30 / 40 / 50 MBit/s
* [DV](https://en.wikipedia.org/wiki/DV) video, 25 / 50 / 100 MBit/s
* [MPEG-2](https://www.itu.int/rec/T-REC-H.262) Long GOP video, 422P@HL, MP@HL (1920 and 1440) and MP@H14
* [JPEG 2000](https://www.itu.int/rec/T-REC-T.800) video
* [JPEG XS](https://jpeg.org/jpegxs/) video
* [H.264](https://www.itu.int/rec/T-REC-H.264) video
* [SMPTE ST 2019](https://ieeexplore.ieee.org/document/7291983) VC-3 video (Avid DNxHD)
* [SMPTE ST 2042](https://ieeexplore.ieee.org/document/7967896) VC-2 video
* [SMPTE RDD 36](https://ieeexplore.ieee.org/document/7438722) video (Apple ProRes)
* Uncompressed video, UYVY / v210
* Avid [MJPEG](https://en.wikipedia.org/wiki/Motion_JPEG) video
* [WAV](https://en.wikipedia.org/wiki/WAV) PCM audio
* [SMPTE ST 436](https://ieeexplore.ieee.org/document/7290051) encapsulated ANC and VBI data
* [IMSC 1 Timed Text](https://www.w3.org/TR/ttml-imsc1.0.1/)

## Topics

A number of topics are described in more detail in the [docs/](./docs/) directory,
including the following:

* [Timed Text](./docs/timed_text.md)
* [RDD 6 XML Creator](./meta/rdd6_xml_creator/README.md)
* [MCA Labels Format](./docs/mca_labels_format.md)
* [IMF Track Files](./docs/imf_track_files.md)
    * [IMF JPEG 2000 Track Files](./docs/imf_jpeg_2000_track_files.md)
    * [IMF Audio Track Files](./docs/imf_audio_track_files.md)
    * [IMF ProRes Image Track Files](./docs/imf_prores_track_files.md)
* [(Beta) Audio Definition Model (ADM) & metadata RIFF chunks](./docs/audio_definition_model.md)

## Build, Test and Install

bmx is developed on Ubuntu Linux but is supported on other Unix-like systems and Windows.

The [cmake](https://cmake.org/) build system is used, with minimum version **3.12**. The build requires the `git` tool along with the C/C++ compilers.

The build process has been tested on Ubuntu, Debian, MacOS and Windows (Microsoft Visual C++ 2017 v15.9.51 and later versions).

### Dependencies

The [libMXF](./deps/libMXF/) and [libMXF++](./deps/libMXFpp/) libraries are provided in the [deps/](./deps) directory.

The [uriparser](https://github.com/uriparser/uriparser) and [expat](https://github.com/libexpat/libexpat) libraries are required. These libraries are typically provided as software packages on Unix-like systems; the Ubuntu / Debian package names are `liburiparser-dev` and `libexpat1-dev`. The libraries are built from the GitHub source when building on Windows using Microsoft Visual Studio C++.

The uuid library (Ubuntu / Debian package name `uuid-dev`) is also required for non-Apple Unix-like systems.

The [libcurl](https://curl.haxx.se/libcurl/) (Ubuntu / Debian package name `libcurl4-openssl-dev`) library is an optional dependency for Unix-like systems. It enables support for reading MXF files over HTTP(S). Add the `-DBMX_BUILD_WITH_LIBCURL=ON` option to the cmake configure command to include it in the build.

### Commands

A basic commandline process is described here for platforms that default to the Unix Makefiles or Visual Studio cmake generators. See [build.md](./docs/build.md) for more detailed build options.

Replace `<build type>` in the commandlines below with `Debug` or `Release`. Note that the Visual Studio generator supports multiple build types for a configuration, which is why the build type is selected _after_ configuration.

The default generator can be overridden using the cmake `-G` option. The list of available generators is shown at the end of the output of `cmake --help`.

Start by creating a build directory and change into it. The commandlines below use a `out/build` build directory in the working tree, which follows the approach taken by Microsoft Visual Studio C++.

#### Unix-like (Unix Makefiles)

Build and test using

```bash
mkdir -p out/build
cd out/build
cmake ../../ -DCMAKE_BUILD_TYPE=<build type>
cmake --build .
make test
```

Install using

```bash
sudo make install
```

The installation may require root permissions. Add `-DCMAKE_INSTALL_PREFIX=<install dir>` (fill in `<install dir>`) to the first `cmake` command above to change the installation directory.

If not using macOS, run `ldconfig` to update the runtime linker cache. This avoids library link errors similar to "error while loading shared libraries".

```bash
sudo /sbin/ldconfig
```

#### Windows (Visual Studio)

Build and test using

```console
mkdir out\build
cd out\build
cmake ..\..\
cmake --build . --config <build type>
ctest -C <build type>
```

Install using

```console
cmake --build . --config <build type> --target install
```

The installation may require administrator privileges. Add `-DCMAKE_INSTALL_PREFIX=<install dir>` (fill in `<install dir>`) to the first `cmake` command above to change the installation directory.


## Building External Applications

External applications that require bmx can be built using cmake similar to the simple executable example shown below.

```text
cmake_minimum_required(VERSION 3.12 FATAL_ERROR)
project(example_project LANGUAGES CXX)

include(FetchContent)
FetchContent_Declare(bmx
    GIT_REPOSITORY "https://github.com/bbc/bmx"
    GIT_TAG "origin/main"
)
FetchContent_GetProperties(bmx)
if(NOT bmx_POPULATED)
    FetchContent_Populate(bmx)
    add_subdirectory(${bmx_SOURCE_DIR} ${bmx_BINARY_DIR})
endif()

add_executable(example example.cpp)
target_link_libraries(example bmx)
```

The `BMX_BUILD_LIB_ONLY` cmake option can be set to `ON` to avoid building the apps and examples in bmx, [libMXF](./deps/libMXF) and [libMXF++](./deps/libMXFpp). Setting the option to `ON` will disable the bmx tests because they requires the apps. Add this line to the cmake

```text
set(BMX_BUILD_LIB_ONLY ON CACHE BOOL "Build bmx, MXF and MXF++ libraries only")
```

## Docker

The [bmxtools](https://github.com/orgs/bbc/packages?repo_name=bmx) Docker images are made available in the GitHub Container Registry. Pull the latest version using,

```bash
docker pull ghcr.io/bbc/bmxtools:latest
```

The [docker/bmx_docker.sh](./docker/bmx_docker.sh) shell script is provided to make it easier to run the Docker container. Run

```bash
./docker/bmx_docker.sh
```

See [Docker Run](#docker-run) for more details on the script.

### Docker Build

The [Dockerfile](./Dockerfile) is used for building a Docker image containing a set of tools from bmx, [libMXF](./deps/libMXF) and [AAF SDK](https://sourceforge.net/projects/aaf/).

The Dockerfile contains a **build** and **runtime** layer:

* **build**: builds and checks the [libMXF](./deps/libMXF), [libMXF++](./deps/libMXFpp) and bmx code.
* **runtime**: provides the commandline tool executables built in the `build` layer.

The runtime Docker image can be built in the top-level directory using docker build,

```bash
DOCKER_BUILDKIT=1 docker build -t bmxtools .
```

If you are behind a proxy then remember to use the `--build-arg` commandline arguments to set the Docker proxy ARGS.

### Docker Run

The [docker/bmx_docker.sh](./docker/bmx_docker.sh) shell script is provided to make it easier to run the Docker container. Run

```bash
./docker/bmx_docker.sh
```

to see the usage and list of available tools.

The script maps the file user and group ID so that files have the user's identity when written to the output directory on the host. This is needed if Docker runs the container as the root user.

The script bind mounts input and output directories on the host to `/input` and `/output` directories on the container. The default is to set input and output directories to the current host directory.

If the input and output directories are the same then that directory is also bind mounted to the container's working directory. If the input or output directory is the current directory then it is also bind mounted to the container's working directory.

This example runs `bmxtranswrap` from input `./in.mxf` to output `./out.mxf`.

```bash
./docker/bmx_docker.sh bmxtranswrap -o out.mxf in.mxf
```

This example runs `bmxtranswrap` from input `./in.mxf` to output `/tmp/out.mxf`.

```bash
./docker/bmx_docker.sh --output /tmp bmxtranswrap -o /output/out.mxf in.mxf
```

This example runs `bmxtranswrap` from input `./sources/in.mxf` to output `./dests/out.mxf`.

```bash
./docker/bmx_docker.sh --input ./sources --output ./dests bmxtranswrap -o /output/out.mxf /input/in.mxf
```

## Source and Binary Distributions

Source distributions, including dependencies, and binaries are made available in the [Releases](https://github.com/bbc/bmx/releases) on GitHub. Older distributions can be found on [SourceForge](https://sourceforge.net/projects/bmxlib/files/).

Source and binary distributions are generally only created when a new feature is required for creating standard compliant sample files for example, or when a release hasn't been made for a long time.

The [release.md](./docs/release.md) document describes the release process.

### Conan

Additionally bmx (including MXF and MXF++) is available via the Conan package manager for C/C++: [bmx Conan recipe](https://conan.io/center/recipes/bmx). Conan Center Index offers precompiled packages for many target systems and otherwise allows to build locally according to a local conan build profile. Follow the code snippets and documentation on the linked page for integrating it.

## License

The bmx library is provided under the BSD 3-clause license. See the [COPYING](./COPYING) file provided with this library for more details.
