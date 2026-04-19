[English](./README_en.md) | [中文](./README.md)

# ONNX Runtime GPU Wheels for NVIDIA Jetson (JetPack 6)

This repository provides pre-compiled **ONNX Runtime GPU** wheels (`.whl`) specifically built for **NVIDIA Jetson** edge devices (such as the Jetson Orin Nano/NX).

## 💡 Why does this repo exist?
Currently, the official Microsoft PyPI repository **does not provide** official `onnxruntime-gpu` wheels for the `aarch64` architecture. While NVIDIA's Jetson AI Lab occasionally releases versions, their updates are often significantly delayed.
To help the community leverage the latest ORT features, inference speedups, and quantization optimizations (crucial for deploying models like Qwen, YOLO, SAM 2 on the edge), I have compiled the full series of fully-featured builds from `v1.23.0` up to `v1.24.4` directly from source.

**Out-of-the-box ready! Save yourself hours of C++ compilation, dependency hell, and Out-of-Memory (OOM) crashes.**

---

## 🛠️ Compatibility & Requirements

**⚠️ STRICT WARNING: Environment Binding!** Due to the nature of C++ dynamic linked libraries (`.so`), these wheels will **ONLY** work on Jetson devices that match the following exact specifications:

* **Architecture:** `aarch64` (ARM64)
* **OS:** Ubuntu 22.04
* **JetPack Version:** JetPack 6.1 / 6.2 / 6.2.1
* **Python Version:** 3.10
* **CUDA Version:** 12.6
* **TensorRT Version:** 10.3
* **cuDNN Version:** 9.x

*(Note: These are NOT backward compatible with JetPack 5.x / 6.0, nor do they work on standard x86 PCs)*

---

## 📦 Available Versions

All builds were configured with `--use_cuda` and `--use_tensorrt` flags to ensure maximum hardware acceleration.

* `v1.24.4` (Latest)
* `v1.24.3`
* `v1.24.2`
* `v1.24.1`
* `v1.23.2`
* `v1.23.1`
* `v1.23.0`

> You can download the `.whl` files from the [Releases page](../../releases) or directly from the repository files.

---

## 🚀 Installation Guide

1. Download the required version, e.g., `onnxruntime_gpu-1.24.4-cp310-cp310-linux_aarch64.whl`.
2. Transfer the file to your Jetson device.
3. Install directly using pip:

```bash
pip3 install onnxruntime_gpu-1.24.4-cp310-cp310-linux_aarch64.whl
```

### ✅ Verification

Open Python in your Jetson terminal and run the following script. If the output includes `TensorrtExecutionProvider` and `CUDAExecutionProvider`, the GPU and TensorRT backends are successfully activated!

```python
import onnxruntime as ort
print("Available Providers:", ort.get_available_providers())
print("Device:", ort.get_device())
```

---

## 🤝 Acknowledgments
* Huge thanks to the official ONNX Runtime team.
* Thanks to the NVIDIA Jetson Community.
* If you encounter `missing .so library` errors during runtime, please double-check that your JetPack and TensorRT versions strictly match the requirements above.
