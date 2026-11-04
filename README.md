<picture>
  <source media="(prefers-color-scheme: dark)" srcset="img/nexives-logo-light.png">
  <img src="img/nexives-logo-dark.png" alt="NEXIVES" width="240">
</picture>

# NEXIVES ExpertStream

**Run Mixture-of-Experts language models that are larger than your memory — on a Mac, or on Linux with an NVIDIA or AMD GPU.**

Models such as Qwen3.8-Flash-Next use only a small part of their weights for each token: a few of hundreds of
“experts” per layer. ExpertStream keeps in memory what every token needs and the experts in use, and reads the other
experts from the SSD in milliseconds when a token needs them. Qwen3.8-Flash-Next is a 93.7 GB model; with ExpertStream
it runs on a MacBook Pro with 64 GB at about 20 tokens per second. On Linux the same works with models far larger
than the system RAM: DeepSeek-V4.1-Flash, a 459 GB model, runs on one NVIDIA GB10 with 128 GB.

* **Works with what you use:** your apps talk to ExpertStream like to Ollama or to an OpenAI-compatible server. With
  Ollama installed, ExpertStream's models appear in Ollama's own model list.
* **Uses the models you have:** besides its own downloads, ExpertStream on the Mac streams the Mixture-of-Experts models
  Ollama keeps in its MLX format — no second download.
* **Shows what it does:** a web view with speed, cache, memory saved and every request; on the Mac also an icon in the
  menu bar.
* **Private:** everything runs on your computer; prompts and answers never leave it.

## Download

**[Download the latest version](../../releases/latest)** — one file for your computer, with the How-To guide (PDF)
next to it:

| Computer | File |
|---|---|
| Mac with Apple silicon | `NEXIVES-ExpertStream-<version>-macOS-arm64.dmg` |
| Linux PC or server with an NVIDIA GPU | `NEXIVES-ExpertStream-<version>-linux-x86_64-nvidia.tar.gz` (or the `nexives-expertstream-nvidia` .deb / .rpm for `amd64` / `x86_64`) |
| NVIDIA GB10 (Dell Pro Max GB10 and other DGX Spark-class machines), Grace | `NEXIVES-ExpertStream-<version>-linux-aarch64-nvidia.tar.gz` (or the .deb / .rpm for `arm64` / `aarch64`) |
| Linux PC with an AMD GPU — **preview, not yet tested on AMD GPUs** | `NEXIVES-ExpertStream-<version>-linux-x86_64-amd.tar.gz` (or the `nexives-expertstream-amd` .deb / .rpm) |

### Mac

| | Needed |
|---|---|
| Mac | Apple silicon (M1 or later); 32 GB of memory or more, 64 GB for Qwen3.8-Flash-Next |
| macOS | 14 Sonoma or later |
| SSD space | the models you download (Qwen3.8-Flash-Next IQ4_XS: 93.7 GB) plus 1 GB for the app |

### Linux

| | Needed |
|---|---|
| Linux | x86_64 or aarch64 with glibc 2.34 or newer: Ubuntu 22.04 or newer, Debian 12, RHEL / Rocky / AlmaLinux 9 or newer, Amazon Linux 2023, Fedora; DGX OS on the GB10 |
| NVIDIA | Turing or newer (T4, RTX 20 and newer, A / L series, H100, RTX PRO 6000, GB10); driver 580 or newer for the CUDA engine, older drivers use the Vulkan engine |
| AMD | Radeon RX 6000 / 7000 / 9000, Radeon PRO W6000 / W7000, Radeon AI PRO R9700, Ryzen AI Max, with the amdgpu driver — not yet tested on AMD GPUs |
| SSD space | the models you download plus 1–3 GB for ExpertStream; a fast NVMe SSD is recommended |

The CUDA and ROCm libraries are included; only the GPU driver comes from your system (and, for the Vulkan engine, the
Vulkan loader: `libvulkan1` / `vulkan-loader`).

## Install

**Mac**

1. Open the disk image and drag **ExpertStream** to **Applications**.
2. Open ExpertStream from Applications. This version is not yet notarized by Apple: if macOS says it cannot check the
   app, open **System Settings → Privacy & Security** and click **Open Anyway** next to ExpertStream (needed once).
3. The web view opens in your browser at `http://127.0.0.1:11435/`. Download a model there, or use one Ollama already
   has.

**Linux** (here for an NVIDIA PC; use the file for your computer)

```bash
tar xzf NEXIVES-ExpertStream-0.2.1-linux-x86_64-nvidia.tar.gz
cd NEXIVES-ExpertStream-0.2.1-linux-x86_64-nvidia
./install.sh                 # for your user, no administrator rights; sudo ./install.sh for all users
expertstream doctor          # the GPU, the engine and the memory ExpertStream found
expertstream pull qwen3.6-35b-a3b:q4
expertstream serve           # web view: http://127.0.0.1:11435/
```

Or install the package: `sudo apt install ./nexives-expertstream-nvidia_0.2.1_amd64.deb` (Debian, Ubuntu) or
`sudo dnf install ./nexives-expertstream-nvidia-0.2.1-1.x86_64.rpm` (RHEL, Fedora, Amazon Linux).
`expertstream service install` starts ExpertStream at login (`--at-boot`: when the computer boots); with Ollama
installed as a system service, `sudo expertstream ollama on` once puts ExpertStream's models into Ollama's list.

The How-To guides cover models, settings, Ollama, OpenClaw and other apps, the command line, speed and memory, and
what to do if something does not work.

To check a download, compare its SHA-256 with the `.sha256` file of the release:

```bash
shasum -a 256 NEXIVES-ExpertStream-*-macOS-arm64.dmg      # Mac
sha256sum -c NEXIVES-ExpertStream-*-linux-*.tar.gz.sha256  # Linux
```

## Older versions and switching back

Every version stays on the **[releases page](../../releases)** with all its files: a new version never replaces an
older one. If a new version does not work well for you, install the older file over it. Models and settings in
`~/.expertstream` are kept.

| Installed from | Switch back |
|---|---|
| Mac disk image | open the older disk image and drag ExpertStream to Applications (Replace) |
| Linux tarball | unpack the older tarball and run its `./install.sh` |
| .deb (Debian, Ubuntu) | `sudo apt install --allow-downgrades ./nexives-expertstream-<gpu>_<version>_<arch>.deb` |
| .rpm (RHEL, Fedora, Amazon Linux) | `sudo dnf downgrade ./nexives-expertstream-<gpu>-<version>-1.<arch>.rpm` |

`expertstream --version` shows the version you run. Each release's notes say what changed and which models need it.

## Measured

| Computer and model | Memory used | Speed |
|---|---|---|
| MacBook Pro (M5 Pro, 64 GB), Qwen3.8-Flash-Next IQ4_XS (180B, 93.7 GB file) | 36 GB instead of 62 GB: 42 % less memory for this model, 26 GB of system RAM freed | about 20–22 tokens/s; long prompts about 300–400 tokens/s |
| MacBook Pro (M5 Pro, 64 GB), Qwen3.6-35B (Q4, 22.4 GB file) | 9 GB instead of 22 GB with a third of the experts cached | 38 tokens/s (64 with the whole model in memory) |
| NVIDIA GB10 (128 GB) next to a vLLM service holding 97 GB, Qwen3.6-35B | 11.5 GB instead of 26.9 GB: 57 % less memory, with 22 % of the experts cached | 13–18 tokens/s; prompts up to 790 tokens/s |
| PC with an NVIDIA T4 (16 GB GPU memory), Qwen3.6-35B | 14.8 GB of GPU memory instead of 25.1 GB (41 % less) — the model does not fit the card without ExpertStream | 10–24 tokens/s on a test machine with a slow SSD |
| NVIDIA GB10 (128 GB), DeepSeek-V4.1-Flash (4 bits, 459 GB file: 3.5 times the system RAM) | 123 GB of the 130.6 GB of system RAM, with 35 % of the experts cached | 4–7 tokens/s |

Speed depends on how much memory is free for the expert cache and on the SSD: close memory-heavy programs for the best
result.

<img src="img/web-view.png" alt="The ExpertStream web view: model, speed, expert cache and memory saved" width="720">

## License

Free for personal, non-commercial use. Use by or for a company or other organisation, use as part of a paid product or
service, and serving other computers on the network need a business license: **info@nexives.com**. The license terms
are included in the app and in the Linux packages.

This repository contains the downloads only; NEXIVES ExpertStream is not open source. It contains open source
components, among them llama.cpp (MIT license), and the Linux packages contain NVIDIA CUDA and AMD ROCm libraries, each
under its own license: see [Third-party software](THIRD_PARTY_NOTICES.md) for the list and the license texts.

## Contact

Questions, business licenses and feedback: **info@nexives.com**
