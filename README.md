## YOLOv12 for object detection      (2/2/2026)

### Install YOLOv12 in Nova

#### 1. Go to your work directory
```{bash}
$ cd /......path to your work directory....
```
I did:
```{bash}
$ cd /work/dsroser/bacharya/YOLOv12
```
#### 2. Request compute node
```{bash}
$ salloc --nodes=1 --gres=gpu:a100:1 --ntasks-per-node=16 --mem=32G --time=02:00:00
```
Gives the interactive shell session to run commands directly.

#### 3. Load the cluster-managed required versions of required softwares (CUDA, Python, FFmpeg, and Git) into current shell session, making them ready to use.
```{bash}
$ module load cuda/11.8 python/3.11.11 ffmpeg git
```
To prevent version mismatch, I am using python 3.11.11, and CUDA version: 11.8. These are compatible with YOLOv12 than newer versions of cuda and python.

#### 4. Create a Python Virtual Environment
```{bash}
$ python -m venv --copies yoloenv
```
Creates an isolated Python environment named yoloenv with copied Python binaries in currect directory, allowing safe installation of packages without affecting the system Python.
This is needed on clusters or HPC systems to avoid permission or path issues.

#### 5. Activate the Python Virtual Environment
```{bash}
$ source yoloenv/bin/activate
```
Activates the yoloenv virtual environment so that Python and packages installed there are used in the current session. Any packages installed after this will be installed in the virtual environment yoloenv. This ensures isolation and reproducibility.

Inside the virtual environment yoloenv,

#### 6. Install setup tools
```{bash}
$ pip install --upgrade pip setuptools wheel
```
#### 7. Install compatible torch, torchvision and torchaudio
$ pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118

#### 8. Clone the official yOLOv12 Repository
```{bash}
$ git clone https://github.com/sunsmarterjie/yolov12.git
```
Clones the yOLOv12 repository from GitHub into the current working directory, creating a copy of all files and history for use on the cluster.

#### 7. Change Directory to yolov12 Folder
```{bash}
$ cd yolov12
```
Navigates into the yolov12 folder (downloaded from git) inside the YOLOv12 folder.

#### 8. Install all requirements

To prevent the mismatch between the torch, torchvision, which were downloaded manually as above, I commented out them from requiremets.txt . Also, since, I will be working on Nova, I am not using falsh-attention, actually flash-attention is targeted for running in local machine, in Nova it is creating errors due to unavialability of setup wheels. 
The requirements.txt I used looks like below:
```{bash}
#torch==2.2.2 
#torchvision==0.17.2
#flash_attn-2.7.3+cu11torch2.2cxx11abiFALSE-cp311-cp311-linux_x86_64.whl
timm==1.0.14
albumentations==2.0.4
onnx==1.14.0
onnxruntime==1.15.1
pycocotools==2.0.7
PyYAML==6.0.1
scipy==1.13.0
onnxslim==0.1.31
onnxruntime-gpu==1.18.0
gradio==4.44.1
opencv-python==4.9.0.80
psutil==5.9.8
py-cpuinfo==9.0.0
huggingface-hub==0.23.2
safetensors==0.4.3
numpy==1.26.4
supervision==0.22.0
```
And it is installed as:
```{bash}
$ pip install -r requirements.txt
```
This installation take around 3-4 minutes. Be patient.

Then I cancelled the allocated enviroment to save resources, because I am ready to work via VS-code now. Follow the steps below.

#### Used Nova via remote tunnel connection to local VS-code interface. Refer to my "InstallGroundedSAM2inNova" repository for details to connect VS code to Nova using a registered tunnel
After nova is connected to VS-code via remote tunnel do as below:

### Open reqired directory from Nova on VS-code running on Nova compute node

#### 1. Click on the "Explore" or "command + shift + E " , then navigate to the desired directory and click enter.

#### 2. Open the .ipynb file you want to work on.

### Activate "yoloenv" virtual environment and select correct python kernel

To run the code cells , we should select the correct kernel. Please follow the steps below:

#### 1. Go to terminal and activate the "yoloenv" virtual environment.
```{bash}
source /path to directory that has gsam2 environment/yoloenv/bin/activate
```
If you also see "base", then your conda may be active, so use code:

```{bash}
conda deactivate
```
```{bash}
exit
```
```{bash}
source /path to directory that has gsam2 environment/yoloenv/bin/activate
```
#### 2. Then, "Select kernel" present on the upper right side of the VS-code interface . Then click "Jupyter Environments", you will see something like (Python)(yoloenv)(Python 3.11.11) based on the name of your virtual environemnt and the python version you have. Select it. If you do not see your gsam2 enviroment then go to step 3.

#### 3. In such cases, you will need to install then register your kernel fist. Go to terminal from step 1. Then use code :

```{bash}
pip install jupyter kernel
```
```bash
python -m ipykernel install --user --name yoloenv --display-name "Python (yoloenv)"
```
then , ctrl+shift_p , type reload window. Then select Jupyter environmnets, then something like (yoloenv)(Python 3.11.11).

Now, we are ready to run code (.ipynb file).


