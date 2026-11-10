# dawn-builds

Prebuilt [Dawn](https://dawn.googlesource.com/dawn), Google's open-source implementation of
WebGPU, as one shared library per platform. Nothing here is original code: this repo only
builds Dawn at a pinned version and publishes the result as a GitHub release, so projects can
download it instead of compiling Dawn (an hour or more, with Python, Go and Ninja) on every
machine.

- `DAWN_REF`: the google/dawn tag or commit that is built.
- `BUILD_REV`: bump to rebuild the same Dawn with different options.
- `.github/workflows/build.yml`: builds and publishes release `dawn-<DAWN_REF>-r<BUILD_REV>`
  with `dawn-<platform>.tar.gz` and its SHA-256.

Platforms: `windows-x64` (MSVC), `linux-x64` (Ubuntu 22.04), `macos-arm64`.

Each package holds `include/` (webgpu.h, the C++ wrapper and the `dawn/native/*` interop
headers), the library under `bin/` or `lib/`, CMake config under `lib/cmake/Dawn`, Dawn's
`LICENSE`, and `BUILD_INFO.txt`. When compiling against it without CMake, define
`WGPU_SHARED_LIBRARY` and `DAWN_NATIVE_SHARED_LIBRARY` (the CMake config does this).

Dawn is BSD 3-Clause licensed; see `LICENSE` in each package.
