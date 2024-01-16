# flexrobotics

Welcome to flexrobotics, the home of roboflex.

Roboflex is a library for distributed robotics. Want to stream from a camera, run tensors through pytorch, integrate with other sensor streams, and control actuators and robots? Roboflex is for you.

Roboflex is:
* Simple to install: `pip install roboflex`, then `pip install roboflex.realsense` etc.
* Simple in concept: distribute `Node`s, which receive and publish `Message`s over pub-sub networks. Threading model is straightforward.
* Simple to implement: use python to create and run Node graphs. Roboflex requires minimal code, and no non-code artifacts (no yaml, no xml).*
* Uses dynamic, not static, message types; more like json than protobuf. Roboflex uses flexbuffers as the message protocol.
* Performant: roboflex is written in c++. Flexbuffer message protocol supports 0-copy serialization into xtensor, eigen, and numpy.
* A library, not a framework: you control main().


## Computation graph for distributed, reactive robotics:

The core idea of roboflex is the 'computation graph'. Nodes send Messages to other nodes, over any transport. You configure this computation graph in a small python script. See the 'core' documentation for more info: (https://github.com/flexrobotics/roboflex).

![image](https://github.com/flexrobotics/.github/assets/132782/d0ae5226-4cfd-4954-b7eb-244b315cbf70)



## Roboflex Components

Roboflex is structured as a single core library (`roboflex`), in the roboflex repository. It supports no physical devices itself. Other repositories support devices, actuators, utilities, etc. This is the current set of repositories in roboflex; each one is named "roboflex_something". If you would like to support other devices or functionality, you can name your repo anything you'd like.

* **roboflex** (core) (https://github.com/flexrobotics/roboflex)

    Definitions and imlpementations of Nodes, RunnableNodes, Messages, python wrappings, and various serialization utilities. Also contains a small library of utility nodes:

    * CallbackFun
    * FilterFun
    * FrequencyGenerator
    * LastOne
    * MapFun
    * MessagePrinter
    * GraphRoot

* **roboflex_examples** (https://github.com/flexrobotics/roboflex_examples)

    Simple examples of roboflex individual components are in those components' examples/ directory. Examples that use two or more components, or are more complex, are here.

    * realsense_tv.py: television for the Intel Realsense camera.
    * webcam_tv.py: television for USB-UVC compatible web cameras.
    * audio_tv.py: displays an audio feed in real-time.

### sensors 📷 🔊 👉

Nodes that broadcast data read from devices, such as images, audio streams, etc.

* **roboflex.audio_alsa** (https://github.com/flexrobotics/roboflex_audio_alsa) 
    
    Audio-broadcasting node that uses linux's Advanced Linux Sound Architecture.

* **roboflex.audio_sdl** (https://github.com/flexrobotics/roboflex_audio_sdl) 
    
    Audio-broadcasting node that uses Simple Directmedia Layer.

* **roboflex.realsense** (https://github.com/flexrobotics/roboflex_realsense)

    RealsenseSensor node, a driver for the Intel Realsense rgb/depth camera.

* **roboflex.webcamuvc** (https://github.com/flexrobotics/roboflex_webcamuvc)

    WebcamSensor node, a driver for USB UVC-compatible web cameras.

* **roboflex.dvs** (https://github.com/flexrobotics/roboflex_dvs)

    DVSSensor node and others, a driver for a particular model of Dynamic Vision Sensor (otherwise known as an 'event camera').

### visualization 📺 

* **roboflex.visualization** (https://github.com/flexrobotics/roboflex_visualization)

    RGBImageTV and DepthTV Nodes, that can visualize rgb and depth camera streams, so far.

* **roboflex.imgui** (https://github.com/flexrobotics/roboflex_imgui)

    Visualizers using IMGUI and IMPLOT.

### actuators 🤖

* **roboflex.dynamixel** (https://github.com/flexrobotics/roboflex_dynamixel)

    Support for dynamixel motors.

### transports 🚡

* **roboflex.transport.zmq** (https://github.com/flexrobotics/roboflex_transport_zmq)

    Zero-mq support for pub-sub.

* **roboflex.transport.mqtt** (https://github.com/flexrobotics/roboflex_transport_mqtt)

    MQTT support for pub-sub.

### utilities ⚒️

* **roboflex.util.jpeg** (https://github.com/flexrobotics/roboflex_util_jpeg)

    Converts (C,H,W) uint8 rgb image tensors to jpegs, in memory and file, and back.

* **roboflex.util.png** (https://github.com/flexrobotics/roboflex_util_png)

    Converts (C,H,W) uint8 rgb image tensors to pngs, in memory and file, and back.

## Building

* In python, roboflex is very simple to install and use. In c++, Roboflex currently uses cmake to build. Yeah, it's a mess. Open to ideas.
