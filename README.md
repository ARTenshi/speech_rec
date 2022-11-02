# Speech Recognition
This repo is based on [Whisper](https://github.com/openai/whisper) by OpenAI and on [whisper-mic](https://github.com/mallorbc/whisper_mic).  Also, it's based on [Vosk](https://alphacephei.com/vosk/) by Alpha-cephei an on [ros-vosk](https://github.com/alphacep/ros-vosk).

## Setup

1. Create an env of your choice.

e.g.

First, create a workspace:

```
cd ~
mkdir -p speech_ws/src
```

Then, clone this repository into the src folder:

```
cd ~/speech_ws/src
git clone https://github.com/ARTenshi/speech_rec.git .
```

2. Run ```pip install -r requirements.txt```

3. Build the project:

e.g 

```
cd ~/speech_ws
catkin_make
```

## Speech Recognition Server

### Structure

Topics:

```
/speech_recognition/final_result
```

of type `std_msgs/String`


Services:

```
/speech_recognition/vosk_service
```

of type `ros_whisper_vosk/GetSpeech` 

where GetSpeech.srv:

```
---
string  data
```

### Initialization

Start `ROS` in one terminal:

```
roscore
```

To start a service (only one at a time), in a different terminal run:

**Whisper**

```
source ~/speech_ws/devel/setup.bash
rosrun ros_whisper_vosk whisper_node.py --english
```

**Vosk**

```
source ~/speech_ws/devel/setup.bash
rosrun ros_whisper_vosk vosk_service.py
```

### Usage

**Command line example**

In one terminal, subsribe to the topic:

```
source ~/speech_ws/devel/setup.bash
rostopic echo /speech_recognition/final_result
```

And in a different terminal, call the service:

```
source ~/speech_ws/devel/setup.bash
rosservice call /speech_recognition/vosk_service "{}"
```

