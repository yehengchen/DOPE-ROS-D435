# Synthetic-Data-UE4-DOPE

<img src="https://github.com/yehengchen/Synthetic-Data-UE4/blob/master/ue4_random_background.png" width="60%" height="60%">

## STEP 1 - Download the NDDS Documentation

__[NVIDIA Deep learning Dataset Synthesizer (NDDS) Documentation](https://github.com/yehengchen/Synthetic-Data-UE4/blob/master/NDDS.pdf)__

```
wget https://github.com/yehengchen/Synthetic-Data-UE4/blob/master/NDDS.pdf
```
***
## STEP 2 - Installing NDDS
__Windows Specific:__

First, install Visual Studio.
a. If you are installing Visual Studio or Visual Studio Community, use the 2017 version located [here](https://visualstudio.microsoft.com/zh-hans/vs/community/). (Other versions may not be compatible.)

i. We successfully tested NDDS using Visual Studio 2017 version 15.9.

b. When installing Visual Studio, you will need to perform a CUSTOM INSTALL. Make sure the following are selected

* Desktop development with C++
* Latest Windows 10 SDK
* Windows 8.1 SDK (if you are still on Windows 8.1)

Download the following:

a. [Epic's Launcher](https://www.epicgames.com/unrealtournament/download) so that you can install Unreal Engine.

i. Due to Unreal's requirements, please always ensure that you create your directory starting with a letter and not a number.

b. Installation instructions are found here.

1. Let's start with Unreal. Once you have downloaded Epic Launcher, install it and create an Epic account.

2. Once installed start the Launcher, login with your account and go to the Unreal Engine tab on the upper left corner of the Launcher. From here, make sur eyou have Library highlighted and then click the " + " icon.

a. A pull down menu will appear with various engine versions. Please select Version 4.21.0

3. With the engine is installed, start the Editor by pressing the Launch button. You will need to start the Editor at least once so that it sets file associations.
Creating a blank default project is good enough.

4. Close the Editor and Launcher for now.

__Linux Specific:__

a. for Unreal Engine, refer to the UE4 website instructions: [https://wiki.unrealengine.com/Building_On_Linux](https://wiki.unrealengine.com/Building_On_Linux)
Note NDDS uses UE version 4.21.0, with respect to the unreal first time setup documentation, use git clone -b 4.21

See also [https://docs.unrealengine.com/en-US/Platforms/Linux/GettingStarted](https://docs.unrealengine.com/en-US/Platforms/Linux/GettingStarted/index.html)

b. Note that `NDDS` currently supports only `Ubuntu 16.04.4 LTS`

c. We successfully tested NDDS using NVIDIA driver versions 387.34 and 390.67

d. If you get this warning, select "More options", then "Skip conversion"

__Installation__
1. Download NDDS:

a. Ensure LFS is installed: [https://help.github.com/articles/installing-git-large-file-storage/](https://help.github.com/en/articles/installing-git-large-file-storage).

Install the NDDS files for the dataset synthesizer.
```
git clone https://github.com/NVIDIA/Dataset_Synthesizer.git
```

2. Navigate to the directory containing the files and find NDDS.uproject. This should be under the \Source sub-directory.

3. Run NDDS.uproject and select "Yes" when it prompts you to rebuild binaries. The compilation will occur behind the scene and open the project wh en
completed.

Note: Nvidia Deep Learning Dataset Synthesizer plugins may only be used within a project (game) -- hosting as engine plugins not yet supported.

***

## STEP 3 - Installing Blender

__Download [[Blender]](https://www.blender.org/)__


Make a 3D model in solidworks or CAD etc.,then import a 3D model in Blender (.stl .dae ...) and export it as a __fbx__ file
then import that __fbx__ file into UE4,  __fbx__ file is work in UE4.

***

## STEP 4 - Run the NDDS

Open the Unreal Editor with the `Dataset_Synthesizer/Source/`__NDDS.uproject__, a default level called TestCapturer will load as indicated at the top left hand corner of the 3D view port. This level has a sample scene with a basic simulation capture set up.



## STEP 5 - Train the DOPE model
Training code is also provided but not supported - [train.py](https://github.com/yehengchen/DOPE-ROS-D435/blob/master/dope/scripts/train.py)

```
python train.py --data path/to/data --object soup --outf soup --gpuids 0 1 2 3 4 --lr 0.01 --epochs 100 

```


