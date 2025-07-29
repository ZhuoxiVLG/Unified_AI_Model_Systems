**ADST**（**A**utonomous **D**riving **S**imulation **T**esting）
===============

![logo](logo.png)

**ADST (Autonomous Driving Simulation Testing)** is a simulation-driven framework for testing, training, and validating autonomous driving systems in complex and realistic environments.

Built on **CARLA**, an open-source simulator tailored for autonomous driving research, ADST leverages high-fidelity urban environments, customizable sensor suites, and dynamic traffic scenarios to support comprehensive evaluation pipelines.

### Key Highlights

- **Simulation-First Testing**: ADST emphasizes safe, repeatable, and scalable testing of autonomous systems before real-world deployment.
- **Open and Customizable**: Built on CARLA’s open-source ecosystem, with full access to maps, vehicles, pedestrians, and sensor configurations.
- **Flexible Scenario Generation**: Allows for tailored testing under varied weather, lighting, traffic, and road conditions.
- **Integrated Validation Workflow**: Supports development, regression testing, and benchmarking of perception, planning, and control modules.

[![CARLA Video](Docs/img/carla_ue5_readme_img.webp)](https://www.youtube.com/watch?v=q4V9GYjA1pE)

>[!NOTE]
> This is the development branch `ue5-dev` for the **Unreal Engine 5.5 version of CARLA**. This branch exists in parallel with the Unreal Engine 4.26 version of CARLA, in the `ue4-dev` branch. Please be sure that this version of CARLA is suitable for your needs as there are significant differences between the UE 5.5 and UE 4.26 versions of CARLA. 

### Recommended system

* Intel i7 gen 9th - 11th / Intel i9 gen 9th - 11th / AMD Ryzen 7 / AMD Ryzen 9
* +32 Gb RAM memory 
* NVIDIA RTX 3070/3080/3090 / NVIDIA RTX 4090 or better
* 16 Gb or more VRAM
* Ubuntu 22.04 or Windows 11

 >[!NOTE]
> Ubuntu version 22.04 and Windows version 11 are required, the Unreal Engine 5.5 version of CARLA will not work on Ubuntu 20.04 or Windows 10 or lower. 

## Building ADST with Unreal Engine 5.5
--------------

Clone this repository locally from GitHub, specifying the *ue5-dev* branch:

```sh
git clone -b ue5-dev https://github.com/carla-simulator/carla.git CarlaUE5
```

In order to build CARLA, you need acces to the CARLA fork of Unreal Engine 5.5. In order to access this repository, you must first link your GitHub account to Epic Games by following [this guide](https://www.unrealengine.com/en-US/ue-on-github). You then also need to use your git credentials to authorise the download of the Unreal Engine 5.5 repository. 

__Building in Linux__:

Run the setup script from a terminal open in the CARLA root directory:

```sh
cd CarlaUE5
./CarlaSetup.sh --interactive
```

The setup script will prompt you for your sudo password, in order to install the prerequisites. It will then prompt you for your GitHub credentials in order to authorise the download of the Unreal Engine repository. 

The setup script will install by default Python 3 using apt. If you want to target an existing Python installation, you should use the `--python-root=PATH_TO_PYTHON` argument with the relevant Python installation path. You can use whereis python3 in your chosen environment and strip the `/python3` suffix from the path.

__Building in Linux unattended__:

If you want to run the setup script unattended, your git credentials need to be stored in an environment variable. Add your github credentials to your `.bashrc` file:

```sh
export GIT_LOCAL_CREDENTIALS=username@github_token
```

Then run the setup script using the following command:

```sh
cd CarlaUE5
sudo -E ./CarlaSetup.sh
```

This will download and install Unreal Engine 5.5, install the prerequisites and build CARLA. It may take some time to complete and use a significant amount of disk space.

If you prefer to add the git credentials in the terminal, use the following command:

```sh
cd CarlaUE5
sudo -E env GIT_LOCAL_CREDENTIALS=github_username@github_token ./CarlaSetup.sh 
```

__Building in Windows__:

To build in Windows, run the batch script:

```sh
cd CarlaUE5
CarlaSetup.bat
```

Unattended mode is currently unavailable in Windows, you will need to enter GitHub credentials or administrator privileges when prompted.

## Rebuilding ADST

Once the setup is complete, you can execute subsequent builds with the following commands in a terminal open in the CARLA root directory. In Linux, run these commands in a standard terminal. In Windows, open the x64 Native Tools Command Prompt for Visual Studio 2022.

__Configure__:

Linux:

```sh
cmake -G Ninja -S . -B Build --toolchain=$PWD/CMake/Toolchain.cmake -DCMAKE_BUILD_TYPE=Release -DENABLE_ROS2=ON
```

Windows:

```sh
cmake -G Ninja -S . -B Build --toolchain=$PWD/CMake/Toolchain.cmake -DCMAKE_BUILD_TYPE=Release
```

>[!NOTE]
> If you intend to target a specific Python installation, you should add both these arguments to the above cmake command: `-DPython_ROOT_DIR=PATH` and `-DPython3_ROOT_DIR=PATH`.

__Build__:

Linux and Windows:

```sh
cmake --build Build
```

__Build and install the Python API__:


Linux and windows:

```sh
cmake --build Build --target carla-python-api-install
```

__Launch the editor__:

```sh
cmake --build Build --target launch
```

For more instructions on building CARLA UE5, please consult the build documentation for [Linux](https://carla-ue5.readthedocs.io/en/latest/build_linux_ue5/) or [Windows](https://carla-ue5.readthedocs.io/en/latest/build_windows_ue5/).

