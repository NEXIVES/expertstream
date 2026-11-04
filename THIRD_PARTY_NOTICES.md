# Third-party software in NEXIVES ExpertStream

NEXIVES ExpertStream is proprietary software of NEXIVES (see [License](README.md#license)). It contains the open
source and other third-party components listed here. Each of them is licensed by its authors under its own license,
shown in the table, and that license applies to the component. The full license texts are in the
[licenses](licenses/) folder of this repository.

This list is for **version 0.2.1**. The .deb and .rpm packages contain the same components as the tarball for the
same computer.

Model weights are not part of ExpertStream: you download models yourself, and each model has its own license (see
the model's page on Hugging Face).

## Contents

* [Engine — in every package](#engine--in-every-package)
* [Linux packages](#linux-packages)
* [Mac app](#mac-app)
* [Source code](#source-code)

## Engine — in every package

The engine is built from llama.cpp (commit 79bce0c of 31 October 2026) with the ExpertStream changes.

| Component | Version | License | License text |
| --- | --- | --- | --- |
| llama.cpp and ggml — © The ggml authors | 79bce0c, with changes | MIT | [text](licenses/llama.cpp/) |
| cpp-httplib — © yhirose | 0.64.0 | MIT | [text](licenses/cpp-httplib-0.64.0/) |
| JSON for Modern C++ (nlohmann/json) — © Niels Lohmann | 3.12.0 | MIT | [text](licenses/nlohmann-json-3.12.0/) |
| stb_image — Sean Barrett | 2.30 | Public domain or MIT, at your choice | in the source file |
| miniaudio — David Reid | 0.11.26 | Public domain or MIT No Attribution, at your choice | in the source file |
| subprocess.h (sheredom) |  | The Unlicense (public domain) | in the source file |
| SHA-256 — Igor Pavlov |  | Public domain | in the source file |

On the Mac the engine uses Apple's Metal and Accelerate frameworks of macOS; on Linux it uses the NVIDIA driver or
the Vulkan loader installed on the computer. These are not part of ExpertStream.

## Linux packages

### Command line tool — in every Linux package

The `expertstream` command is a Python program packaged with PyInstaller, together with the Python runtime and the
libraries it needs.

| Component | Version | License | License text |
| --- | --- | --- | --- |
| Python — © Python Software Foundation | 3.12.15 | PSF-2.0 (Python Software Foundation License) | [text](licenses/python-3.12.15/) |
| OpenSSL — © The OpenSSL Project Authors | 3.5.1 | Apache-2.0 | [text](licenses/openssl-3.5.1/) |
| zlib — © Jean-loup Gailly and Mark Adler | 1.2.11 | Zlib | [text](licenses/zlib-1.2.11/) |
| bzip2 / libbzip2 — © Julian R Seward | 1.0.8 | bzip2-1.0.6 (BSD-style) | [text](licenses/bzip2-1.0.8/) |
| XZ Utils (liblzma) | 5.2.5 | Public domain | [text](licenses/xz-5.2.5/) |
| Expat | 2.5.0 | MIT | [text](licenses/expat-2.5.0/) |
| mpdecimal — © Stefan Krah | 2.5.1 | BSD-2-Clause | [text](licenses/mpdecimal-2.5.1/) |
| PyInstaller bootloader | 6.22.3 | GPL-2.0-or-later with the PyInstaller bootloader exception | [text](licenses/pyinstaller-6.22.3/) |

The PyInstaller bootloader exception allows the bootloader to be used in programs under any license.

### NVIDIA packages (x86_64 and aarch64)

| Component | Version | License | License text |
| --- | --- | --- | --- |
| NVIDIA CUDA runtime (libcudart) | 13.0.96 | NVIDIA CUDA Toolkit End User License Agreement | [text](licenses/nvidia-cuda-13/) |
| NVIDIA cuBLAS and cuBLASLt | 13.1.1.3 | NVIDIA CUDA Toolkit End User License Agreement | [text](licenses/nvidia-cuda-13/) |
| GNU OpenMP runtime (libgomp) of GCC | 11.5.0 | GPL-3.0-or-later with the GCC Runtime Library Exception 3.1 | [text](licenses/gcc-libgomp-11.5.0/) |

The NVIDIA libraries are distributed under the NVIDIA CUDA Toolkit End User License Agreement, which lists them as
redistributable (Attachment A). The NVIDIA driver is not part of ExpertStream.

### AMD package (x86_64, ROCm 7.2.4)

| Component | Version | License | License text |
| --- | --- | --- | --- |
| HIP runtime (libamdhip64) | 7.2.53211 | MIT | [text](licenses/rocm-7.2.4/hip-runtime-amd/) |
| hipBLAS | 3.2.0 | MIT | [text](licenses/rocm-7.2.4/hipblas/) |
| hipBLASLt (incl. rocRoller) | 1.2.2 | MIT | [text](licenses/rocm-7.2.4/hipblaslt/) |
| rocBLAS | 5.2.0 | MIT and BSD | [text](licenses/rocm-7.2.4/rocblas/) |
| rocSOLVER | 3.32.0 | BSD-2-Clause | [text](licenses/rocm-7.2.4/rocsolver/) |
| ROCr runtime (libhsa-runtime64) | 1.18.0 | NCSA | [text](licenses/rocm-7.2.4/hsa-rocr/) |
| Code Object Manager (libamd_comgr) | 3.0.0 | NCSA | [text](licenses/rocm-7.2.4/comgr/) |
| ROCTracer (libroctx64) | 4.1 | MIT | [text](licenses/rocm-7.2.4/roctracer/) |
| rocprofiler-register | 0.6.0 | MIT | [text](licenses/rocm-7.2.4/rocprofiler-register/) |
| libdrm and libdrm_amdgpu | 2.4.128 | MIT | [text](licenses/libdrm-2.4.128/) |
| elfutils libelf | 0.194 | LGPL-3.0-or-later (or GPL-2.0-or-later) | [text](licenses/elfutils-libelf-0.194/) |
| numactl libnuma | 2.0.19 | LGPL-2.1 | [text](licenses/numactl-2.0.19/) |
| GNU OpenMP runtime (libgomp) of GCC | 11.5.0 | GPL-3.0-or-later with the GCC Runtime Library Exception 3.1 | [text](licenses/gcc-libgomp-11.5.0/) |

The AMD GPU driver of the computer is not part of ExpertStream.

## Mac app

### Python runtime and libraries — command line tool and MLX engine

The `expertstream` command and the MLX engine (for the models Ollama keeps in its MLX format) are Python programs
packaged with PyInstaller, together with the Python runtime and these libraries.

| Component | Version | License | License text |
| --- | --- | --- | --- |
| Python — © Python Software Foundation | 3.15.0 | PSF-2.0 (Python Software Foundation License) | [text](licenses/python-3.15.0/) |
| OpenSSL — © The OpenSSL Project Authors | 4.0.3 | Apache-2.0 | [text](licenses/openssl-4.0.3/) |
| XZ Utils (liblzma) | 5.8.4 | 0BSD | [text](licenses/xz-5.8.4/) |
| mpdecimal — © Stefan Krah | 4.0.1 | BSD-2-Clause | [text](licenses/mpdecimal-4.0.1/) |
| Zstandard (libzstd) — © Meta Platforms, Inc. and affiliates | 1.5.7 | BSD-3-Clause (dual-licensed with GPL-2.0; used under BSD) | [text](licenses/zstd-1.5.7/) |
| PyInstaller bootloader | 6.22.3 | GPL-2.0-or-later with the PyInstaller bootloader exception | [text](licenses/pyinstaller-6.22.3/) |
| SQLite (MLX engine only) | 3.54.1 | Public domain | — |

### Python packages — MLX engine

| Package | Version | License | License text |
| --- | --- | --- | --- |
| anyio | 4.15.1 | MIT | [text](licenses/python/anyio-4.15.1/) |
| click | 8.5.0 | BSD-3-Clause | [text](licenses/python/click-8.5.0/) |
| filelock | 4.2.4 | MIT | [text](licenses/python/filelock-4.2.4/) |
| fsspec | 2026.9.0 | BSD-3-Clause | [text](licenses/python/fsspec-2026.9.0/) |
| h11 | 0.16.0 | MIT | [text](licenses/python/h11-0.16.0/) |
| hf-xet | 1.7.1 | Apache-2.0 | [text](licenses/python/hf-xet-1.7.1/) |
| httpcore2 | 2.16.0 | BSD-3-Clause | [text](licenses/python/httpcore2-2.16.0/) |
| httpx2 | 2.16.0 | BSD-3-Clause | [text](licenses/python/httpx2-2.16.0/) |
| huggingface_hub | 2.3.0 | Apache-2.0 | [text](licenses/python/huggingface_hub-2.3.0/) |
| idna | 3.20 | BSD-3-Clause | [text](licenses/python/idna-3.20/) |
| Jinja2 | 3.1.6 | BSD-3-Clause | [text](licenses/python/Jinja2-3.1.6/) |
| markdown-it-py | 4.2.0 | MIT | [text](licenses/python/markdown-it-py-4.2.0/) |
| MarkupSafe | 3.0.4 | BSD-3-Clause | [text](licenses/python/MarkupSafe-3.0.4/) |
| mdurl | 0.1.2 | MIT | [text](licenses/python/mdurl-0.1.2/) |
| mlx | 0.32.4 | MIT | [text](licenses/python/mlx-0.32.4/) |
| mlx-lm | 0.32.2 | MIT | [text](licenses/python/mlx-lm-0.32.2/) |
| mlx-metal | 0.32.4 | MIT (Metal C++ headers: Apache-2.0) | [text](licenses/python/mlx-metal-0.32.4/) |
| numpy | 2.5.4 | BSD-3-Clause AND 0BSD AND MIT AND Zlib AND CC0-1.0 | [text](licenses/python/numpy-2.5.4/) |
| packaging | 26.3 | Apache-2.0 OR BSD-2-Clause | [text](licenses/python/packaging-26.3/) |
| protobuf | 7.36.2 | BSD-3-Clause | [text](licenses/python/protobuf-7.36.2/) |
| Pygments | 2.21.0 | BSD-2-Clause | [text](licenses/python/Pygments-2.21.0/) |
| PyYAML | 6.0.3 | MIT | [text](licenses/python/PyYAML-6.0.3/) |
| regex | 2026.9.29 | Apache-2.0 AND CNRI-Python | [text](licenses/python/regex-2026.9.29/) |
| rich | 15.0.0 | MIT | [text](licenses/python/rich-15.0.0/) |
| safetensors | 0.8.0 | Apache-2.0 | [text](licenses/python/safetensors-0.8.0/) |
| sentencepiece | 0.2.2 | Apache-2.0 | [Apache-2.0 text](licenses/apache-2.0/) (the package ships no separate file) |
| setuptools | 84.2.1 | MIT (vendored packages: MIT, Apache-2.0 OR BSD-2-Clause) | [text](licenses/python/setuptools-84.2.1/) |
| tokenizers | 0.23.3 | Apache-2.0 | [Apache-2.0 text](licenses/apache-2.0/) (the package ships no separate file) |
| tqdm | 4.70.1 | MPL-2.0 AND MIT | [text](licenses/python/tqdm-4.70.1/) |
| transformers | 5.21.0 | Apache-2.0 | [text](licenses/python/transformers-5.21.0/) |
| truststore | 0.10.5 | MIT | [text](licenses/python/truststore-0.10.5/) |
| typing_extensions | 4.16.0 | PSF-2.0 | [text](licenses/python/typing_extensions-4.16.0/) |

## Source code

* **tqdm** is licensed under MPL-2.0 (and MIT). ExpertStream contains it unchanged; its source code is available from
  the tqdm project on GitHub (https://github.com/tqdm/tqdm) and from PyPI (https://pypi.org/project/tqdm/4.70.1/).
* **elfutils libelf** and **numactl libnuma** (AMD package) are licensed under the LGPL. ExpertStream contains them as
  separate shared libraries (`libelf.so.1`, `libnuma.so.1`) that you may replace with your own build. They are the
  libraries of the Rocky Linux 9 packages elfutils 0.194-1.el9.rocky.0.1 and numactl 2.0.19-3.el9, unchanged except
  for a library search path (`$ORIGIN`) added to the files. Their complete source code is on the
  [0.2.1 release page](https://github.com/NEXIVES/expertstream/releases/tag/v0.2.1):
  `elfutils-0.194-1.el9.rocky.0.1.src.rpm` and `numactl-2.0.19-3.el9.src.rpm` (the Rocky Linux source packages, each
  with a `.sha256` checksum).
