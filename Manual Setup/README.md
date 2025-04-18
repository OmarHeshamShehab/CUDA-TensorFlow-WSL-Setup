# Setting Up CUDA 12.3, cuDNN, and TensorRT with TensorFlow on WSL: A Step-by-Step Guide for GPU-Accelerated Machine Learning

    1- Open powershell as admin and type wsl --install
    2- Restart your password once it is opened create user name and password on PowerShell opened 
    3- Then open Ubuntu
    4- ![Point Number 4](image-1.png)
    5- Run this command sudo apt update && sudo apt upgrade -y
    6- Then we will need to install all essential packages required for upcoming installation sudo apt install build-essential -y
    7- Before starting installation of any component navigate to this https://www.tensorflow.org/install/source#gpu to verify the version compatibility for components 
    8- Specify your installation to which OS will be installed this is done as we don't need to install Nvidia driver through wsl it will passed through nvidia-smi to validate installation 
    9- Navigate to CUDA Toolkit Archive | NVIDIA Developer and download the version required.
    10- ![Point Number 10](image.png)
    
    11- Download cuda 12.3 wget https://developer.download.nvidia.com/compute/cuda/12.3.2/local_installers/cuda_12.3.2_545.23.08_linux.run
    12- Install Cuda Toolkit using this command sudo sh cuda_12.3.2_545.23.08_linux.run
    13- Navigate to cuDNN Archive | NVIDIA Developer and download below
    14- ![Point Number 14](image.png)
    15- https://developer.nvidia.com/downloads/compute/cudnn/secure/8.9.7/local_installers/12.x/cudnn-linux-x86_64-8.9.7.29_cuda12-archive.tar.xz/
    16- Navigate to your user path inside ubuntu and paste downloaded file for example mine is \\wsl.localhost\Ubuntu\home\tensorflow
    17- Also download tensorRT 8 as it is current supported version till now TensorRT Download | NVIDIA Developer it says it supports CUDA 12.0 & 12.1 but I tested it and supports also 12.3
    18- ![Point Number 18](image.png)
    19- Extract Cuda Files using this command tar -xvf cudnn-linux-x86_64-8.9.7.29_cuda12-archive.tar.xz
    20- Navigate inside extracted file cd cudnn-linux-x86_64-8.9.7.29_cuda12-archive
    21- Copy all cudnn with extension h inside include directory sudo cp include/cudnn*.h /usr/local/cuda-12.3/include
    22- Do same for lib files sudo cp lib/libcudnn* /usr/local/cuda-12.3/lib64
    23- Grant read permissions to all users for the cuDNN header files and shared libraries in the specified CUDA installation directories. This can be useful when you’re compiling or running software that relies on cuDNN.  sudo chmod a+r /usr/local/cuda-12.3/include/cudnn*.h /usr/local/cuda-12.3/lib64/libcudnn*
    24- Go one step back to main directory cd..
    25- Extract and Move TensorRT files using below commands :
        a. tar -xzvf TensorRT-8.6.1.6.Linux.x86_64-gnu.cuda-12.0.tar.gz
        b. sudo mv TensorRT-8.6.1.6 /usr/local/TensorRT-8.6.1
    26- Install gedit Sudo apt install gedit
    27- Open bashrc gedit ~/.bashrc
    28- Add Cuda Toolkit, cuDNN and TensorRT to .bashrc :
        a. export PATH=/usr/local/cuda-12.3/bin:/usr/local/TensorRT-8.6.1/bin:$PATH
        b. export LD_LIBRARY_PATH=/usr/local/cuda-12.3/lib64:/usr/local/TensorRT-8.6.1/lib:$LD_LIBRARY_PATH
        c. export CUDNN_PATH=/usr/local/cuda-12.3/lib64
    29- Then save and close
    30- Run this command for changes to take effect source ~/.bashrc
    31- To check cuda version run this command nvcc --version
    32- Verify CUDNN installation  cat /usr/local/cuda-12.3/include/cudnn_version.h | grep CUDNN_MAJOR -A 2

Optional but preferable from my point of view ubuntu latest one installed using wsl already comes with python 3.10.12 but I will install miniconda 

    33- Download with wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
    34- Install with this command bash ./Miniconda3-latest-Linux-x86_64.sh
    35- Create new folder mkdir projects
    36- Create another folder mkdir .tf217
    37- Create environment with miniconda  conda create --name .tf217 python=3.11
    38- Activate environment conda activate .tf217 
    39- Install TensorFlow using this command python -m pip install tensorflow[and-cuda]==2.17
    40- Command to verify TensorFlow installation with GPU python -c "import tensorflow as tf; print(tf.config.list_physical_devices('GPU'))"
    41- You might get some warnings related to NUMA which I guess is fine as they are capabilities that might not be available in all motherboards 
    42- Please take in consideration if you installed tensorflow 2.17.0 you will get below errors which I guess is normal as they are already mentioned in the docs below
    
    https://www.tensorflow.org/tutorials/quickstart/beginner#set_up_tensorflow
    ![Point Number 42](image.png)
    
    43- Don't forget to run below commands to install tensorrt inside your environment:
        pip install nvidia-pyindex nvidia-tensorrt pycuda
    44- Finally use below to validate your installation
    45-  ![Point Number 45](tf_Version.ipynb)
    46- The warnings related to NUMA (Non-Uniform Memory Access) are common and can generally be ignored unless you are working on systems or workloads that     
        heavily rely on NUMA support.
        
        
        
