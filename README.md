# 🚀 CUDA TensorFlow 2.20 Setup (Ubuntu / WSL2)

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
- [👨‍💻 Author](#-author)

---

## 📦 Overview

This repository provides a complete **automated installation script** for setting up a **GPU-accelerated Python environment** using:
- ✅ CUDA 12.5
- ✅ cuDNN 9.3.0
- ✅ TensorFlow **2.20** with GPU support
- ✅ TensorRT & PyCUDA
- ✅ Miniconda on Ubuntu (20.04 / 22.04 / 24.04, WSL2 & bare-metal)

The script also **auto-detects your NVIDIA GPU and drivers**, ensuring the correct `nvidia-utils` package (`nvidia-smi`) is installed.  
It includes a **Jupyter Notebook** to verify GPU availability inside TensorFlow.

---

## 🛠️ Prerequisites

- Ubuntu **20.04, 22.04, or 24.04** (WSL2 or native Linux)
- A compatible **NVIDIA GPU**:
  - Compute Capability **≥ 6.0** (Pascal or newer)
  - Driver **≥ 550** (required for CUDA 12.5)
- Do **NOT** run the script as `root` or with `sudo`
- Internet connection for package downloads

---

## 📜 What the Script Does

1. Checks that you're not root  
2. Updates the system and installs essential build tools  
3. Installs:
   - **CUDA 12.5**
   - **cuDNN 9.3.0** (auto-selected for your Ubuntu version)  
4. Adds CUDA environment variables to your `.bashrc` and current session  
5. Installs **Miniconda**, initializes Conda, and disables auto base activation  
6. Creates a dedicated Conda environment named `.tf220` with **Python 3.11**  
7. Installs into the `.tf220` environment:
   - **TensorFlow 2.20 with GPU support**
   - **PyCUDA**
   - **TensorRT**
   - `libstdcxx-ng` (to fix `GLIBCXX_3.4.32` compatibility for PyCUDA)  
8. Detects your NVIDIA GPU and installs the **matching `nvidia-utils` package** (`nvidia-smi`)  
9. Cleans up installer files and APT package cache to save space  

---

## 🔧 Installation Steps

### 1. 📥 Clone the Repository

```bash
git clone https://github.com/OmarHeshamShehab/CUDA-TensorFlow-WSL-Setup.git
```

### 2. ✍️ Create the Installation Script

```bash
nano setup_tf220.sh
```

- Paste the contents of `script.txt` into the terminal (select all, copy, then paste)  
- Save the file with: `Ctrl + O`, then `Enter`  
- Exit the editor with: `Ctrl + X`  

### 3. ✅ Make the Script Executable

```bash
chmod +x setup_tf220.sh
```

### 4. 🚫 Run the Script as a Normal User

```bash
./setup_tf220.sh
```

> ⚠️ **Do not use `sudo`** — the script calls `sudo` only when required.

---

## 📂 Conda Environment Details

| Name     | Python Version | Packages Installed                   |
|----------|----------------|--------------------------------------|
| `.tf220` | 3.11           | TensorFlow 2.20 (GPU), PyCUDA, TensorRT, libstdcxx-ng |

To activate later:

```bash
conda activate .tf220
```

---

## 🧪 GPU Test Notebook

Once installation is complete, you can verify the setup using the included notebook:

**➡️ File:** `verify_tensorflow_gpu.ipynb`

### Run with Jupyter:

```bash
conda activate .tf220
jupyter notebook verify_tensorflow_gpu.ipynb
```

### Or from terminal:

```bash
python verify_tensorflow_gpu.ipynb
```

The notebook will output the number of GPUs detected by TensorFlow.

---

## 📁 Customizing TensorFlow Version

This setup script defaults to installing **TensorFlow 2.20**.

However, **you can install any TensorFlow version `>= 2.11`** by editing this line in the script:

```bash
pip install "tensorflow[and-cuda]==2.20.*"
```

For a different version (example: 2.19):

```bash
pip install "tensorflow[and-cuda]==2.19.*"
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
- **nvidia-smi not found?** The script attempts auto-detection, but you can also install manually:
  ```bash
  sudo apt install -y nvidia-utils-<driver-version>
  ```
- **GPU not detected in TF?** Double-check:
  - You’re in the `.tf220` environment
  - You installed correct NVIDIA drivers (≥ 550)
  - Your GPU is **Pascal or newer (Compute Capability ≥ 6.0)**  

---

## 👨‍💻 Author

**Omar Hesham Shehab**  
GitHub: [@OmarHeshamShehab](https://github.com/OmarHeshamShehab)

---
