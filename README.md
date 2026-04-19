[English](./README_en.md) | [中文](./README.md)

# ONNX Runtime GPU Wheels for NVIDIA Jetson (JetPack 6)

这是一个为 **NVIDIA Jetson** 系列设备（尤其是 Jetson Orin Nano/NX）提供 **ONNX Runtime GPU** 预编译包（`.whl`）的开源仓库。

## 💡 为什么要有这个仓库？
目前，微软官方的 PyPI 源**不提供**针对 `aarch64` 架构的 `onnxruntime-gpu` 官方预编译包。虽然 NVIDIA 官方 Jetson AI Lab 会提供部分版本，但更新往往非常滞后。
为了让大家能够第一时间在边缘设备上使用最新版 ORT 带来的极速推理和量化优化（如 Qwen、YOLO、SAM 2 等前沿模型的端侧部署），我从源码为大家编译了 `v1.23.0` 到 `v1.24.4` 的全系列满血版本。

**开箱即用，免去长达数小时的 C++ 编译煎熬与各种由于依赖和内存溢出导致的报错！**

---

## 🛠️ 环境要求 (Compatibility)

**⚠️ 警告：环境强绑定！** 由于 C++ 动态链接库（`.so`）的特性，这些包**只能**在满足以下确切环境的 Jetson 设备上运行：

* **硬件架构:** `aarch64` (ARM64)
* **操作系统:** Ubuntu 22.04
* **JetPack 版本:** JetPack 6.1 / 6.2 / 6.2.1
* **Python 版本:** 3.10
* **CUDA 版本:** 12.6
* **TensorRT 版本:** 10.3
* **cuDNN 版本:** 9.x

*(注意：不向下兼容 JetPack 5.x / 6.0，也不支持 x86 电脑)*

---

## 📦 支持的版本 (Available Versions)

编译均开启了 `--use_cuda` 和 `--use_tensorrt`，支持极致性能加速。

* `v1.24.4` (Latest)
* `v1.24.3`
* `v1.24.2`
* `v1.24.1`
* `v1.23.2`
* `v1.23.1`
* `v1.23.0`

> 可以在本仓库的 [Releases 页面](../../releases) 或文件列表中下载对应的 `.whl` 文件。

---

## 🚀 安装指南 (Installation)

1. 下载你需要的版本，例如 `onnxruntime_gpu-1.24.4-cp310-cp310-linux_aarch64.whl`。
2. 将文件传输到你的 Jetson 设备上。
3. 直接使用 pip 安装：

```bash
pip3 install onnxruntime_gpu-1.24.4-cp310-cp310-linux_aarch64.whl
```

### ✅ 验证安装

在终端中打开 Python，运行以下代码。如果输出中包含 `TensorrtExecutionProvider` 和 `CUDAExecutionProvider`，则说明 GPU 和 TensorRT 后端已成功激活！

```python
import onnxruntime as ort
print("Available Providers:", ort.get_available_providers())
print("Device:", ort.get_device())
```

---

## 🤝 贡献与感谢
* 感谢 ONNX Runtime 官方团队的出色工作。
* 感谢 NVIDIA Jetson 社区。
* 如果在使用过程中遇到因为缺少 `.so` 库导致的错误，请检查你的 JetPack 和 TensorRT 版本是否与上述要求完全一致。
