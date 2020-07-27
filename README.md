# Computer Pointer Controller

In this project, you will use a gaze detection model to control the mouse pointer of your computer. You will be using the Gaze Estimation model to estimate the gaze of the user's eyes and change the mouse pointer position accordingly. This project will demonstrate your ability to run multiple models in the same machine and coordinate the flow of data between those models.

04 pre-trained models from the Intel Pre-trained Models Zoo have to be used:
* [Face Detection](https://docs.openvinotoolkit.org/latest/omz_models_intel_face_detection_adas_binary_0001_description_face_detection_adas_binary_0001.html)
* [Head Pose Estimation](https://docs.openvinotoolkit.org/latest/omz_models_intel_head_pose_estimation_adas_0001_description_head_pose_estimation_adas_0001.html)
* [Facial LandMarks Detection](https://docs.openvinotoolkit.org/latest/omz_models_intel_landmarks_regression_retail_0009_description_landmarks_regression_retail_0009.html)
* [Gaze Estimation Model](https://docs.openvinotoolkit.org/latest/omz_models_intel_gaze_estimation_adas_0002_description_gaze_estimation_adas_0002.html)

The flow of data look like this:
![Gameplay Screenshot](./bin/assets/pipeline.png)


## Project Set Up and Installation
* Download [OpenVINO ToolKit](https://docs.openvinotoolkit.org/latest/index.html) and install it locally.
* Clone the Repository  `git clone https://github.com/obeshor/nd131-computer-pointer-controller.git`
* Create and activate a virtual environment 

   `pip install virtualenv`
   
   `virtualenv venv`
   
   `cd venv/Scripts/`
   
   `activate`
   
* Install dependencies

  `pip install -r requirements.txt`

* Initialize OpenVINO environment

  `cd C:\Program Files (x86)\IntelSWTools\openvino\bin\`
  
  `setupvars.bat`
  
 * Download models
 
   `python ./src/download_models.py`

Refer below is the project structure:

The bin folder contains the demo video file, the models folder contains all the Intel's Pretrained models needed for execution, and the src folder contains all necessary python files.
```
📦nd131-computer-pointer-controller
 ┣ 📂bin
 ┃ ┣ 📂assets
 ┃ ┃ ┗ 📜pipeline.png
 ┃ ┣ 📜demo.mp4
 ┃
 ┣ 📂venv
 ┃     
 ┣ 📂models
 ┃ ┗ 📂intel
 ┃   ┣ 📂face-detection-adas-0001
 ┃   ┃ ┣ 📂INT1
 ┃   ┃ ┃ ┣ 📜face-detection-adas-0001.bin
 ┃   ┃ ┃ ┗ 📜face-detection-adas-0001.xml
 ┃   ┣ 📂gaze-estimation-adas-0002
 ┃   ┃ ┣ 📂FP16
 ┃   ┃ ┃ ┣ 📜gaze-estimation-adas-0002.bin
 ┃   ┃ ┃ ┗ 📜gaze-estimation-adas-0002.xml
 ┃   ┃ ┗ 📂FP32
 ┃   ┃   ┣ 📜gaze-estimation-adas-0002.bin
 ┃   ┃   ┗ 📜gaze-estimation-adas-0002.xml
 ┃   ┣ 📂head-pose-estimation-adas-0001
 ┃   ┃ ┣ 📂FP16
 ┃   ┃ ┃ ┣ 📜head-pose-estimation-adas-0001.bin
 ┃   ┃ ┃ ┗ 📜head-pose-estimation-adas-0001.xml
 ┃   ┃ ┗ 📂FP32
 ┃   ┃   ┣ 📜head-pose-estimation-adas-0001.bin
 ┃   ┃   ┗ 📜head-pose-estimation-adas-0001.xml
 ┃   ┗ 📂landmarks-regression-retail-0009
 ┃     ┣ 📂FP16
 ┃     ┃ ┣ 📜landmarks-regression-retail-0009.bin
 ┃     ┃ ┗ 📜landmarks-regression-retail-0009.xml
 ┃     ┗ 📂FP32
 ┃       ┣ 📜landmarks-regression-retail-0009.bin
 ┃       ┗ 📜landmarks-regression-retail-0009.xml
 ┣ 
 ┣ 📂src  
 ┃ ┣ 📜download_models.py
 ┃ ┣ 📜face_detection.py
 ┃ ┣ 📜gaze_estimation.py
 ┃ ┣ 📜head_pose_estimation.py
 ┃ ┣ 📜input_feeder.py
 ┃ ┣ 📜landmarks_detection.py
 ┃ ┣ 📜main.py
 ┃ ┣ 📜mouse_controller.py
 ┃ ┗ stats.txt
 ┃ 
 ┣ 📜README.md
 ┣ 📜models.txt
 ┗ 📜requirements.txt
```
    
## Demo
Step 1:  Go back to the project directory src folder
 
        `cd path_of_project_directory` 
Step 2: Run below commands to execute the project
 * Run on CPU
 ```
python src/main.py -fd models/intel/face-detection-adas-binary-0001/INT1/face-detection-adas-binary-0001.xml -hp models/intel/head-pose-estimation-adas-0001/FP16/head-pose-estimation-adas-0001.xml -fl models/intel/landmarks-regression-retail-0009/FP16/landmarks-regression-retail-0009.xml -ge models/intel/gaze-estimation-adas-0002/FP16/gaze-estimation-adas-0002.xml -d CPU -i bin/demo.mp4 -flags fd fl hp ge

```
![Gameplay Screenshot](./bin/assets/image.png)

* Run on GPU
 ```
python src/main.py -fd <Face detection model name directory> -fl <Facial landmark detection model name directory> -hp <head pose estimation model name directory> -ge <Gaze estimation model name directory> -i <input video directory> -d GPU
```
* Run on FPGA
 ```
python src/main.py -fd <Face detection model name directory> -fl <Facial landmark detection model name directory> -hp <head pose estimation model name directory> -ge <Gaze estimation model name directory> -i <input video directory> -d HETERO:FPGA,CPU
```  
* Run on NSC2
 ```
python src/main.py -fd <Face detection model name directory> -fl <Facial landmark detection model name directory> -hp <head pose estimation model name directory> -ge <Gaze estimation model name directory> -i <input video directory> -d MYRIAD
```     
       
## Documentation
Below are the command line arguments needed and there brief use case.

Argument|Type|Description
| ------------- | ------------- | -------------
-fd | Required | Path to a face detection model xml file with a trained model.
-fl | Required | Path to a facial landmarks detection model xml file with a trained model.
-hp| Required | Path to a head pose estimation model xml file with a trained model.
-ge| Required | Path to a gaze estimation model xml file with a trained model.
-i| Required | Path to image or video file or WEBCAM.
-o| Optional | Specify path of output folder where we will store result.
-l| Optional | Absolute path to a shared library with the kernels impl.
-prod  | Optional | Specify confidence threshold which the value here in range(0, 1), default=0.6
-flags  | Optional | for see the visualization of different model outputs of each frame.
-d | Optional | Provide the target device: CPU / GPU / VPU / FPGA


## Benchmarks
 Include the benchmark results of running your model on multiple hardwares and multiple model precisions. Your benchmarks can include: model loading time, input/output processing time, model inference time etc.
 The Performance tests were run on HP Laptop with **Intel i3-3110M 2.40Ghz** and **16 GB Ram**

#### CPU

| Properties  | FP32        | FP16        | INT8        |
| ------------| ----------- | ----------- | ----------- |
|Model Loading| 0.84s       | 1.17s       | 1.19s       |
|Infer Time   | 83.80s      | 23.12s      | 42.21s      |
|FPS          | 0.70fps     | 0.60fps     | 1.39fps     |


| Models        | FP32 -INT1  | FP16        | INT8        |
| --------------| ----------- | ----------- | ----------- |
|Face detection | 0.428s      | -           | -           |
|facial landmark| 0.114s      | 0.105s      | 0.101s      |
|Head pose      | 0.149S      | 0.176s      | 0.129s      |
|Gaze estimation| 0.178S      | 0.179s      | 0.161s      |

## Results
We notice the models with low precisions generally tend to give better inference time, but it still difficult to give an exact measures as the time spent depend of the performance of the machine used in that given time when running the application. Also we notice that there is a difference between the same model with different precisions.

The models with low precisions are more lightweight than the models with high precisons, so this makes the execution of the network more fast.

