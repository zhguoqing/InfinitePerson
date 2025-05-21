# InfinitePerson: Innovating Synthetic Data Creation for Generalization Person Re-Identification

## Data Synthesis Toolkit

The data synthesis toolkit includs four parts: Makehuman plugin, Controlnet, several UE4 blueprints and data annotation scripts.

There are some steps you must do:

1. Download our prepared UE4 content package. It includes texture materials, anim blueprint,  character blueprint, 3D human models and an example level. [BaiduNetdisk link](https://pan.baidu.com/s/15yz7XQoY1bRejRkwzJEwfQ) (verification code: **wn4m**)

2. Use ControlNet to create clothing textures.

3. Prepare UE4 and UnrealCV plugin. A compiled UnrealCV plugin for win64 UE4.27 has been included in the above link. 

4. Get familar with the scripts and have fun synthesizing data with UE4. 



### 1. Prepare 3D Human Models 

(1) Download [Makehuman](http://www.makehumancommunity.org/content/downloads.html)

(2) Download some free clothing models from the community

(3) After all steps above, you can now (a) go to tab "Geometries->Eyes" and select "Low-poly" (otherwise it looks weird in UE4), (b) go to tab "Pose/Animate->Skeleton" and select "Game engine", (c) go to tab "Community->Mass produce", in "Export settings" choose file format "FBX", in the middle panel and the left panel choose your preferred configurations, click "Produce" after entering the number of models you want. 

(4) Import the generated fbx files to UE4.



### 2. Prepare UE4 and UnrealCV plugin. 

(1) Install [UnrealEngine 4](https://www.unrealengine.com/en-US/). The version number is 4.27. 

(2) Install and enable UnrealCV in UE4. [UnrealCV](https://github.com/unrealcv/unrealcv) is an excellent tool for computer vision researchers. We fix some small issues when compiling this plugin for UE 4.27. 



### 3. Prepare UV texture maps 

(1) Clone [ControlNet](https://github.com/lllyasviel/ControlNet-v1-1-nightly).

(2) Download `control_v11p_sd15_normalbae`.

(3) Put in the UV texture map you want to generate and click generate. 

(4) Import the generated clothing texture into UE4 and add it to the character models.



### 4. Introduction to Blueprints

In this section, we introduce how the character and level work together to mimic the virtual surveillance. After configuring the charactor BP and editing the level BP, we can run the game and collect images. 

(1) Character BP:

![Character_BP](C:\Users\Xary\Desktop\Data Synthesis Toolkit\Character_BP.png)

(2) Level: 

![Level_BP](C:\Users\Xary\Desktop\Data Synthesis Toolkit\Level_BP.png)

(3) Run the game and collect camera information.

Run the game in UE4 first and then run the script caminfo_collect.py in Unrealtool.

Then, you can execute `ce Add_actor` in UE4 console to generate some actors and help you locate the virtual cameras.

Adjust the view and call `gc()` in the python console to record current camera location and rotation. If you call `gc()` for 6 times, it means person images will be captured from these 6 positions. Use `sa()` to save the camera location and rotation information in a plk file.

Stop the game after saving the camera information. 

(4) Re-run the Game and collection images.

Run the game again and run the python script generate_datasets.py. Of course, you need to rewrite the parameters in generate_datasets.py. The file provided in this repo is only an example to show how to communicate with UE4 with python. 

### 5. Post process

#### Cut to images

We prepare a python script unrealtool/postprocess.py. It includes all functions you need to cut person images and form a person re-id dataset. 





































