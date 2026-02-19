# Road Anomaly Detection using Raspberry Pi
An IoT-based dashcam system for real-time pothole and road damage detection using Raspberry Pi 4


Objective: Real-time detection of road anomalies for vehicle safety.

System Components: Raspberry Pi 4, Camera Module, 3A Power Supply.

Key Features: Smart dashcam setup, auto-start via Systemd, and edge-based processing.




## 1. Introduction
Using a Raspberry Pi and a camera module for computer vision with OpenCV, YOLO, and TensorFlow Lite. The aim of this project is to provide a starting point for using RPi & CV in your own DIY / maker projects. Computer vision based on cameras is very powerful and will bring your project to the next level. This allows you to track complicated objects that would otherwise not be possible with other types of sensors (infrared, ultrasonic, LiDAR, etc).

Note the code is based on Python and OpenCV meaning it is cross-platform. You can run this on other Linux-based platforms as well, e.g. x86/x64 PC, IPC, Jetson, Banana Pi, LattaPanda, BeagleBoard, etc.


## 2. Dependency
### 2.1. Packages requirement
This project is dependent on the following packages:
- Python >= 3.6.9
- OpenCV-Python
- OpenCV-Contrib-Python
- NumPy
- SciPy
- Matplotlib
- Ultralytics

### 2.2. Hardware support
- Support Raspberry Pi 1 Model B, Raspberry Pi 2, Raspberry Pi Zero, and Raspberry Pi 3/4/5 (preferable)
  - Different boards will have very varied performances.
  - RPi 3/4/5 are preferable as they have more powerful CPUs;
  - RPi 1/2 may be struggling and produce very low FPS, in which case you can further reduce the camera resolution (160 x 120).
- Nvidia Jetson
  - Jetson Nano (A01) also passed the test.
  - Jetson Orin Nano should work as well.
  - Jetson has its own repo now: [jetson-object-detection](https://github.com/automaticdai/jetson-object-detection)
- Any USB camera supported by Raspberry Pi
  - To see a list of all supportive cameras, visit http://elinux.org/RPi_USB_Webcams
- The official RPi camera module is supported through `Picamera2`.



To use it, download the model and labels into the module directory:
```
cd src/object-detection-tflite

# COCO labels
wget https://raw.githubusercontent.com/google-coral/test_data/master/coco_labels.txt

# EfficientDet-Lite0 model (INT8 quantized, ~4MB)
wget https://storage.googleapis.com/mediapipemodels/object_detector/efficientdet_lite0/int8/1/efficientdet_lite0.tflite
```

Then install the TensorFlow Lite runtime and run:

```
pip install tflite-runtime
python3 src/object-detection-tflite/object_detection_tflite.py
```

## 4. How to Run
### 4.1. Install the environment on Raspberry Pi
```
sudo apt-get install -y libopencv-dev libatlas-base-dev
pip3 install virtualenv Pillow numpy scipy matplotlib opencv-python opencv-contrib-python
```

or use the installation script:

```
chmod +x install.sh
./install.sh
```

### 4.2. Install TensorFlow Lite (optional; only if you want to use the neural network example)
```
wget https://github.com/PINTO0309/Tensorflow-bin/raw/master/tensorflow-2.1.0-cp37-cp37m-linux_armv7l.whl
pip3 install --upgrade setuptools
pip3 install tensorflow-2.1.0-cp37-cp37m-linux_armv7l.whl
pip3 install -e .
```

### 4.3. Run the scripts
Run scripts in the `/src` folder by:

```
python3 src/$FOLDER_NAME$/$SCRIPT_NAME$.py
```

To stop the code, press the `ESC` key on your keyboard.

### 4.4. Change camera resolution
Changing the resolution will significantly impact the FPS. By default it is set to be `320 x 240`, but you can change it to any value that your camera supports at the beginning of each source code (defined by `IMAGE_WIDTH` and `IMAGE_HEIGHT`). Typical resolutions are:

- 160 x 120
- 320 x 240
- 640 x 480 (480p)
- 1280 x 720 (720p)
- 1920 x 1080 (1080p: make sure your camera supports this high resolution.)


## 5. Q&A
**Q: Does this support Nvidia Jetson?**  
A: Yes. I have tested with my Jetson Nano 4GB. Note that Jetson has its own repo now: [jetson-object-detection](https://github.com/automaticdai/jetson-object-detection).

**Q: Does this support the Raspberry Pi camera?**  
A: This is implemented in [issue [#16]](https://github.com/automaticdai/rpi-object-detection/pull/16).

**Q: Does this support Raspberry Pi 5?**  
A: This is not officially tested (as I haven't received my Pi 5 yet) but it should work out of the box.

**Q: Can we run this project on Ubuntu server 22.04/24.04?**  
A4: It is not officially tested but you should be able to run 99% of the things here.

**Q: I am using virtual environment and get a message "no module called libcamera" issue**  
A: A simple solution would be [(Reference)](https://forums.raspberrypi.com/viewtopic.php?t=361758):  
`python3 -m venv --system-site-packages env`

Thanks [VgerTest](https://github.com/VgerTest) for [issue [#20]](https://github.com/automaticdai/rpi-object-detection/issues/20).

#

## License
© This source code is licensed under the [MIT License](LICENSE).
