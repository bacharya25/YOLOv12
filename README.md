## YOLOv12 for object detection

Used Nova via remote tunnel connection to local VS-code interface. Refer to "Installation   " for details on connection.

Path to YOLOv12 object detection folder: "/work/dsrosero/bacharya/YOLOv12"
Code used: yolov12Baseline.ipynb
Gpu: a100

### Steps followed:

#### 1. Create a virtual environment for reproducibility 

At first navigate to YOLOv12 directory in Nova via VS-code terminal. Then create yolov12 virtual environment as:

```{bash}
python -m venv yolov12
```
#### 2. Activate the virtual environment
```{bash}
source /work/dsrosero/bacharya/YOLOv12/yolov12/bin/activate
```
#### 3. Download the requirement.txt file from YOLOv12 GitHub repository : https://github.com/sunsmarterjie/yolov12 

The requirment.txt has python dependencies used for training the v12 model. So, I want to use the same versions for compatibility. 
