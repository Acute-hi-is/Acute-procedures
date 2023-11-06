# Acute-procedures

This repository will be used to manage procedures for ACUTE lab equipment. The first procedure is for 
getting started using the 32 channel amplifier on a PC.

## 1. Get python
We recomend using [Pycharm community edition](https://www.jetbrains.com/pycharm/download/?section=windows), but
alternatively we've used MS Visual Studio.

Once you've set up your prefered python compiler, make sure to add it to [path](https://realpython.com/add-python-to-path/), and 
restart the computer if needed.

## 2. Drivers
The drivers used for the equipment is called MADIface USB. Navigate to [here](https://www.rme-audio.de/downloads.html),
select MADIface USB from the drop down menu, select your OS, get the Driver, download the .zip file and follow the instructions.

In case the link stops working, or for some reason the .zip file stops being supported, I've included a file from 11.23 in the test_actuators
folder.

## 3. Install libraries
Install the Numpy and sounddevice packages to your python libraries. You might be able to do this with the command: 

>python pip install Numpy

>python pip install sounddevice

If you're using Pycharm then you can also do it manually by navigating to: 
File -> settings -> Project: -> Python Interpreter -> press the "+ sign" -> search for Numpy and sounddevice -> install package...

## 4. Find sound device ID.
You're almost there. If you haven't already, plug the USB from the audio amp to your computer and turn it on. Navigate to 
"Device Manager" if you're on PC. I haven't tested this on MacOS, so maybe we will edit this in the future to try it out.
Under "Sound, video and game controllers" you should be able to find ASIO MADIface USB, if everything went well with installing the Driver.
Open Command promt (CMD) and type:
>python -m sounddevice

or

>python3 -m sounddevice

depending on the path argument.
This should result in a list of installed sound devices on your system. Things like the speaker on your computer and other drivers.
You are looking for what number "ASIO MADIface USB" is under. On my system its number 8, but I've seen it number 14 elsewhere.

## 5. Run the test code.
Download the folder marked "Test_actuators". In this folder and subfolders we have three files named "Test_actuators".
One is a .sln, another one is a .pyproj, and a third is a .py.
Right click the .sln, and open with pycharm. Open the .py file and navigate to the very end of the code snippet. There you will find
the code:
>with sd.OutputStream(device=X, channels=1, callback=callback,
				samplerate=samplerate, extra_settings=asio_ch):

Change the X to the number you found to be the sound device ID on your device.

Press the play button at the top, and if everything went well, you should see the amplifier responding.

For added effect, you should have pluged in some actuators. The code should send very basic analog signals
to the channels output, from 1 to 32.

## 6. Some elements in the code to change:
In the future we will add more procedures for code to work with, but in this specific code there are a few
variables you can play around with:

If you need to change the amount actuators (coils or speakers), frequency or amplitude, then change:
nCoils = 32, f = 100, a = 0.1

If you need to change duration, change:
stimuliDuration = 0.2