# LLAMASharp Unity Demo Modified

This project is a clone of [LLAMASharp Unity Demo](https://github.com/eublefar/LLAMASharpUnityDemo), but it is modified so that it works in newer versions of `LLAMASharp`

## Demo project overview

### Prerequisites to run

To run this project you need to download the `GGUF` model into `Assets/StreamingAssets` folder.

e.g. [Meta-Llama-3.1-8B-Instruct-Q4_K_M.gguf](https://huggingface.co/lmstudio-community/Meta-Llama-3.1-8B-Instruct-GGUF/tree/main)

Note: You only need single `.gguf` file. Files there usually differ by their quantization level, see details in the model's readme.

### Overview

This project contains a single scene at `Assets/Scenes/SampleScene.unity` with a simple chat UI.  
Monobehaviour that has all the logic is named `LLamaSharpTestScript` and it's already added and set up in `Example` GameObject.

It generally follows LLAMASharp readme example and shows how to switch between different chat sessions.

Before running the project you should point `LLamaSharpTestScript.ModelPath` from the inspector to your model path in `StreamingAssets`.

Additionally this project uses the following packages:
- [UniTask](https://github.com/Cysharp/UniTask)  
  For integrating async tasks with Unity and offloading blocking tasks to thread pool.
- [NuGetForUnity](https://github.com/GlitchEnzo/NuGetForUnity)  
  For fetching LLAMASharp and all it's dependencies from NuGet.

## How to run the project
1. Clone this repository
2. Download [Meta-Llama-3.1-8B-Instruct-Q4_K_M.gguf](https://huggingface.co/lmstudio-community/Meta-Llama-3.1-8B-Instruct-GGUF/tree/main) and put it into `Assets/StreamingAssets/models` folder
3. The project should work.
    - If it does not, likely problem is that you need to change the `LLAMASharp.Backend.Cpu` runtime. From NuGet package manager, uninstall and reinstall it (choose same version as LLAMASharp). If there are duplication errors, delete unnecessary runtimes in `Assets/Packages/LLAMASharp.Backend.Cpu` folder.

## Setting up a project from scratch


- Install [UniTask](https://github.com/Cysharp/UniTask) and [NuGetForUnity](https://github.com/GlitchEnzo/NuGetForUnity) via PackageManager.
- Install LLAMASharp via NuGetForUnity.
- ~~Manually download one of the LLAMASharp.Backend.xx NuGet packages (LLamaSharp and Backend versions must match exactly!)~~
  - ~~[CPU](https://www.nuget.org/packages/LLamaSharp.Backend.Cpu)~~
  - ~~[CUDA 11](https://www.nuget.org/packages/LLamaSharp.Backend.Cuda11)~~
  - ~~[CUDA 12](https://www.nuget.org/packages/LLamaSharp.Backend.Cuda12)~~
- ~~Unpack using ZIP, move `runtimes/<your runtime>/libllama.dll` to your Unity project Assets.
  (Note: dll must be called `libllama.dll` to be found. If it's named `llama.dll` - rename it when adding to the Unity project.)~~
- Install one of the LLAMASharp.Backend.xx via NuGetForUnity.
	- Remove unnecessary runtime folders.
- Download the `gguf` file of the model from HuggingFace and put it in the StreamingAssets folder.
- ~~Move `LLamaSharpBuildPostprocessor` into your project, or write your own for targets other than windows (see `Build and distribution`).~~
	- This file is not neccesary, so it is removed from this project.
- ~~Download CUDA Runtime dlls and add them to your project to be able to run the build on systems w/o CUDA installed. 
For Windows-x64 target you can download them from llama.cpp releases [here](https://github.com/ggerganov/llama.cpp/releases), you need files named cudart-llama-bin-win-cu#.#.#-x64.zip where #.#.# is your LLamaSharp backend's CUDA version.~~
- Make sure that your LLAMASharp library and backend are of the same version. Same with CUDA version of LLAMASharp.Backend.CUDA and your installed CUDA (or CUDA RT).

At this point you should be able to copy example from this project and run it in yours.

~~## Build and distribution~~

~~There is some issue with LLamaSharp finding `libllama.dll` in build's plugin directory.
As a quick workaround there is `LLamaSharpBuildPostprocessor` that copies libllama.dll into the same directory as the `.exe`.
It only supports windows build target but you can adapt it to work with other targets, or just resolve this manually each build.~~

~~## Projects using LLamaSharp in Unity~~

~~If you have a project using LLamaSharp together with Unity and want it to appear here, please create an issue and I will add it!~~
