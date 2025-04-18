# 🚀 CUDA TensorFlow Setup for WSL2 (Ubuntu 24.04)

> **GitHub Repo:** [CUDA-TensorFlow-WSL-Setup](https://github.com/OmarHeshamShehab/CUDA-TensorFlow-WSL-Setup)  
> Maintained by: [@OmarHeshamShehab](https://github.com/OmarHeshamShehab)

---

## 📚 Table of Contents

- [📦 Overview](#-overview)
- [🛠️ Prerequisites](#️-prerequisites)
- [📜 What the Script Does](#-what-the-script-does)
- [🔧 Installation Steps](#-installation-steps)
- [📂 Conda Environment Details](#-conda-environment-details)
- [🧪 GPU Test Notebook](#-gpu-test-notebook)
- [📁 Customizing TensorFlow Version](#-customizing-tensorflow-version)
- [🧹 Clean-Up & Reuse](#-clean-up--reuse)
- [❗ Troubleshooting](#-troubleshooting)
- [📄 License](#-license)
- [👨‍💻 Author](#-author)

---

## 📦 Overview

This repository provides a complete **automated installation script** for setting up a **GPU-accelerated Python environment** using:
- ✅ CUDA 12.5
- ✅ cuDNN 9.3.0
- ✅ TensorFlow with GPU support
- ✅ TensorRT & PyCUDA
- ✅ Miniconda on Ubuntu 24.04 (WSL2 compatible)

It includes a **Jupyter Notebook** to verify GPU availability inside TensorFlow.

---

## 🛠️ Prerequisites

- Ubuntu 24.04 (preferably in WSL2)
- A compatible NVIDIA GPU with latest drivers installed
- Do **NOT** run the script as `root` or with `sudo`
- Internet connection for package downloads

---

## 📜 What the Script Does

1. Checks that you're not root
2. Updates the system & installs build essentials
3. Installs:
   - CUDA 12.5
   - cuDNN 9.3.0
4. Adds CUDA to your environment
5. Installs Miniconda & configures Conda
6. Creates Conda environment `.tf219` with Python 3.11
7. Installs:
   - TensorFlow (GPU)
   - PyCUDA
   - TensorRT
   - `libstdcxx-ng` (for GLIBCXX compatibility)
8. Installs GPU CLI tools (e.g., `nvidia-smi`)
9. Cleans up leftover installers and cache

---

## 🔧 Installation Steps

### 1. 📥 Clone the Repository

```bash
git clone https://github.com/OmarHeshamShehab/CUDA-TensorFlow-WSL-Setup.git
cd CUDA-TensorFlow-WSL-Setup
```

---

### 2. ✅ Make the Script Executable

```bash
chmod +x setup_gpu_env.sh
```

---

### 3. 🚫 Run the Script as a Normal User

```bash
./setup_gpu_env.sh
```

> ⚠️ **Do not use `sudo`** — the script calls `sudo` only when required.

---

## 📂 Conda Environment Details

| Name     | Python Version | Packages Installed                   |
|----------|----------------|--------------------------------------|
| `.tf219` | 3.11           | TensorFlow (GPU), pycuda, tensorrt, libstdcxx-ng |

To activate later:

```bash
conda activate .tf219
```

---

## 🧪 GPU Test Notebook

Once installation is complete, you can verify the setup using the included notebook:

**➡️ File:** `verify_tensorflow_gpu.ipynb`

### Run with Jupyter:

```bash
conda activate .tf219
jupyter notebook verify_tensorflow_gpu.ipynb
```

### Or from terminal:

```bash
python verify_tensorflow_gpu.ipynb
```

The notebook will output the number of GPUs detected by TensorFlow.

---

## 📁 Customizing TensorFlow Version

This setup script defaults to installing the latest available TensorFlow with GPU support.

However, **you can install any TensorFlow version `>= 2.11`** by editing this line in the script:

```bash
pip install "tensorflow[and-cuda]"
```

For a specific version:

```bash
pip install "tensorflow==2.12.0"
```

> ⚠️ When changing TensorFlow versions, you may also need to update the **CUDA and cuDNN versions** accordingly.

Refer to the official TensorFlow compatibility matrix for supported versions of CUDA, cuDNN, and Python:  
🔗 [TensorFlow GPU Build Requirements](https://www.tensorflow.org/install/source#gpu)

---

## 🧹 Clean-Up & Reuse

- All temporary `.deb` and installer files are deleted automatically after installation
- APT cache is cleaned at the end to free up space
- CUDA and Conda environment variables are saved in `.bashrc`

---

## ❗ Troubleshooting

- **CUDA tools not found?** Run `source ~/.bashrc` to reload your environment
- **nvidia-smi not found?** Try `sudo apt install -y nvidia-utils-525`
- **GPU not detected in TF?** Double-check:
  - You’re in the `.tf219` environment
  - You installed correct drivers on Windows side (for WSL)

---

## 📄 License

This repository and script are open-sourced under the MIT License. Use and modify freely.

---

## 👨‍💻 Author

**Omar Hesham Shehab**  
GitHub: [@OmarHeshamShehab](https://github.com/OmarHeshamShehab)

---
