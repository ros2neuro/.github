<p align="center">
  <img src="https://raw.githubusercontent.com/ros2neuro/.github/main/profile/logo.png" alt="ros2neuro logo" width="220">
</p>

# ros2neuro: Closed-Loop Brain–Computer Interfaces with Modular ROS 2 Components

**ros2neuro** is the ROS 2 successor of [ROS-Neuro](https://github.com/rosneuro): an open-source C++17 framework that builds a closed-loop brain–computer interface (BCI) out of ordinary ROS 2 nodes. Acquisition back-ends, filters, decoders, integrators, experimental protocols and feedback displays are interchangeable **plugins** that exchange a handful of typed messages (`NeuroFrame`, `NeuroFeature`, `NeuroPrediction`, `NeuroControl`, `NeuroEvent`). In this way neural signals become a data source at the same level as cameras, inertial sensors and controllers, and the BCI lives in the same graph as the robot it drives.

A closed-loop BCI is a distributed real-time system: neural samples are acquired, filtered, decoded and accumulated into a command while a person watches a feedback and an experimental protocol (calibration, evaluation, control) runs. ros2neuro implements every step of this loop as a separate node, so each research group can replace or add a single component (a new amplifier, a new decoder, a new feedback) without touching the rest.

![ros2neuro closed loop](https://raw.githubusercontent.com/ros2neuro/.github/main/profile/ros2neuro_loop.png)

ros2neuro is designed first of all for endogenous BCIs (e.g. motor imagery) and for continuous, self-paced control of assistive devices such as wheelchairs and telepresence robots.

<p align="center">
  <img src="https://raw.githubusercontent.com/ros2neuro/.github/main/profile/ros2neuro_wheelchair.png" alt="ros2neuro BMI driving a wheelchair" width="480">
</p>

📖 **Documentation, concepts and tutorials: <https://ros2neuro.github.io/docs/>**

---

## 1. Installation

ros2neuro is distributed as Debian packages for **Ubuntu 24.04 (noble) + ROS 2 Jazzy**. [ROS 2 Jazzy](https://docs.ros.org/en/jazzy/Installation.html) must already be installed.

### 1.1 Setup your keys
Setup your computer to accept software signed by ros2neuro.github.io:
```bash
curl -fsSL https://ros2neuro.github.io/ppa/ubuntu/ros2neuro-key.asc | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/ros2neuro-key.gpg > /dev/null
```

### 1.2 Setup your source list
```bash
sudo curl -fsSL -o /etc/apt/sources.list.d/ros2neuro.list https://ros2neuro.github.io/ppa/ubuntu/ros2neuro.list
```

### 1.3 Installation
First, make sure your Debian package index is up-to-date:
```bash
sudo apt update
```
Then, install the whole stack:
```bash
sudo apt install ros-jazzy-ros2neuro-full
```
`ros-jazzy-ros2neuro-full` installs everything **except** the acquisition plugins that need a proprietary SDK (`ros2neuro_acquisition_antneuro`, `ros2neuro_acquisition_gusbamp`), which must be built from source. Single packages can be installed on their own, e.g. `sudo apt install ros-jazzy-ros2neuro-filters`.

### 1.4 Update `rosdep` list (optional)
Add the ros2neuro packages to the `rosdep` list:
```bash
echo "yaml https://ros2neuro.github.io/ppa/ubuntu/rosdep-ros2neuro-packages.yaml" | sudo tee /etc/ros/rosdep/sources.list.d/20-ros2neuro.list
rosdep update
```

### 1.5 Try it (no hardware needed)
```bash
source /opt/ros/jazzy/setup.bash
ros2 launch ros2neuro_acquisition_dummy dummy_acquisition.launch.py
```
The [hardware-free tutorial](https://ros2neuro.github.io/docs/tutorials/hardware-free-pipeline/) replays an EEG recording through a complete motor-imagery chain, from the acquisition to the wheel or bar feedback.

### (1.6 Alternative installation)
Clone the repositories of this organization in the `src/` folder of a colcon workspace (`neurodraw` too: it is plain CMake) and run `colcon build`.

---

## 2. ros2neuro packages

Every package is a separate repository. Each base class (acquisition device, filter, decoder, protocol, feedback) is defined by a package, and each implementation is a separate package that registers against it as a plugin and is chosen at run time by a parameter. Details, parameters and topics of each one are in the [package documentation](https://ros2neuro.github.io/docs/packages/).

![ros2neuro extension points](https://raw.githubusercontent.com/ros2neuro/.github/main/profile/ros2neuro_plugins.png)

**Core**
- [**ros2neuro_msgs**](https://github.com/ros2neuro/ros2neuro_msgs) Standard messages of the ros2neuro framework
- [**ros2neuro_data**](https://github.com/ros2neuro/ros2neuro_data) Data structures of the ros2neuro framework

**Acquisition**
- [**ros2neuro_acquisition**](https://github.com/ros2neuro/ros2neuro_acquisition) Generic interface for acquiring data from different devices
- [**ros2neuro_acquisition_dummy**](https://github.com/ros2neuro/ros2neuro_acquisition_dummy) Acquisition plugin generating synthetic signals (no hardware)
- [**ros2neuro_acquisition_xdf**](https://github.com/ros2neuro/ros2neuro_acquisition_xdf) Acquisition plugin replaying GDF/BDF files
- [**ros2neuro_acquisition_lsl**](https://github.com/ros2neuro/ros2neuro_acquisition_lsl) Acquisition plugin for LSL streams
- [**ros2neuro_acquisition_eegdev**](https://github.com/ros2neuro/ros2neuro_acquisition_eegdev) Acquisition plugin for the eegdev library
- [**ros2neuro_acquisition_antneuro**](https://github.com/ros2neuro/ros2neuro_acquisition_antneuro) Acquisition plugin for ANT Neuro eego amplifiers
- [**ros2neuro_acquisition_gusbamp**](https://github.com/ros2neuro/ros2neuro_acquisition_gusbamp) Acquisition plugin for g.tec g.USBamp amplifiers

**Recording and visualization**
- [**ros2neuro_recorder**](https://github.com/ros2neuro/ros2neuro_recorder) Generic interface for recording neuro data
- [**ros2neuro_recorder_xdf**](https://github.com/ros2neuro/ros2neuro_recorder_xdf) Recorder plugin for GDF/BDF files
- [**ros2neuro_visualizer**](https://github.com/ros2neuro/ros2neuro_visualizer) Scope and spectrum viewer for EEG/EMG data

**Filters**
- [**ros2neuro_filters**](https://github.com/ros2neuro/ros2neuro_filters) Generic filters and filter chain for neuro data
- [**ros2neuro_filters_dc**](https://github.com/ros2neuro/ros2neuro_filters_dc) Filters plugin for DC removal
- [**ros2neuro_filters_butterworth**](https://github.com/ros2neuro/ros2neuro_filters_butterworth) Filters plugin for Butterworth filter
- [**ros2neuro_filters_car**](https://github.com/ros2neuro/ros2neuro_filters_car) Filters plugin for CAR filter
- [**ros2neuro_filters_laplacian**](https://github.com/ros2neuro/ros2neuro_filters_laplacian) Filters plugin for Laplacian filter
- [**ros2neuro_filters_blackman**](https://github.com/ros2neuro/ros2neuro_filters_blackman) Filters plugin for Blackman window
- [**ros2neuro_filters_flattop**](https://github.com/ros2neuro/ros2neuro_filters_flattop) Filters plugin for Flattop window
- [**ros2neuro_filters_hamming**](https://github.com/ros2neuro/ros2neuro_filters_hamming) Filters plugin for Hamming window
- [**ros2neuro_filters_hann**](https://github.com/ros2neuro/ros2neuro_filters_hann) Filters plugin for Hann window

**Processing**
- [**ros2neuro_processing_spectral**](https://github.com/ros2neuro/ros2neuro_processing_spectral) Spectral features (FFT, Welch PSD, spectrogram)
- [**ros2neuro_processing_buffer**](https://github.com/ros2neuro/ros2neuro_processing_buffer) Sliding-window buffer of neuro data

**Decoding and integration**
- [**ros2neuro_decoder**](https://github.com/ros2neuro/ros2neuro_decoder) Generic interface for decoders (`.r2nd` models + `manifest.yaml`)
- [**ros2neuro_decoder_lda**](https://github.com/ros2neuro/ros2neuro_decoder_lda) Decoder plugin for LDA
- [**ros2neuro_decoder_qda**](https://github.com/ros2neuro/ros2neuro_decoder_qda) Decoder plugin for QDA
- [**ros2neuro_decoder_svm**](https://github.com/ros2neuro/ros2neuro_decoder_svm) Decoder plugin for SVM
- [**ros2neuro_decoder_gaussian**](https://github.com/ros2neuro/ros2neuro_decoder_gaussian) Decoder plugin for Gaussian classifier
- [**ros2neuro_decoder_py**](https://github.com/ros2neuro/ros2neuro_decoder_py) Python decoder for deep-learning models
- [**ros2neuro_decoder_converters**](https://github.com/ros2neuro/ros2neuro_decoder_converters) Converters from Matlab decoders to `.r2nd`
- [**ros2neuro_integrator**](https://github.com/ros2neuro/ros2neuro_integrator) Generic interface for evidence accumulation
- [**ros2neuro_integrator_exponential**](https://github.com/ros2neuro/ros2neuro_integrator_exponential) Integrator plugin for exponential smoothing
- [**ros2neuro_integrator_buffer**](https://github.com/ros2neuro/ros2neuro_integrator_buffer) Integrator plugin based on a buffer of predictions

**Protocols and feedback**
- [**ros2neuro_manager**](https://github.com/ros2neuro/ros2neuro_manager) Generic protocol manager (events, layout, reset)
- [**ros2neuro_manager_synchronous**](https://github.com/ros2neuro/ros2neuro_manager_synchronous) Protocol plugin for calibration and evaluation
- [**ros2neuro_manager_asynchronous**](https://github.com/ros2neuro/ros2neuro_manager_asynchronous) Protocol plugin for continuous control
- [**ros2neuro_feedback**](https://github.com/ros2neuro/ros2neuro_feedback) Generic passive feedback
- [**ros2neuro_feedback_wheel**](https://github.com/ros2neuro/ros2neuro_feedback_wheel) Feedback plugin drawing a wheel
- [**ros2neuro_feedback_bar**](https://github.com/ros2neuro/ros2neuro_feedback_bar) Feedback plugin drawing one bar per class
- [**neurodraw**](https://github.com/ros2neuro/neurodraw) SDL2/OpenGL 2D graphics library for BCI feedback

**Examples**
- [**ros2neuro_devel_test**](https://github.com/ros2neuro/ros2neuro_devel_test) Hardware-free launchers (GDF replay) of complete closed loops

---

## References
- Forin P, Simonetto P, et al. ros2neuro: Building Closed-Loop Brain–Computer Interfaces with Modular ROS 2 Components (in preparation)
- Tonin L, Beraldo G, Tortora S, Menegatti E (2022) ROS-Neuro: An Open-Source Platform for Neurorobotics. Front. Neurorobot. 16:886050. doi: 10.3389/fnbot.2022.886050
- Tonin L, Beraldo G, Tortora S, Tagliapietra L, Millàn JdR et al. (2019). ROS-Neuro: A common middleware for BMI and robotics. The acquisition and recorder packages, in Proc of 2019 IEEE International Conference on Systems, Man and Cybernetics (SMC), 2767–2772
- Beraldo G, Tortora S, Menegatti E, Tonin L. (2020). ROS-Neuro: Implementation of a closed-loop BMI based on motor imagery, in Proc of 2020 IEEE International Conference on Systems, Man, and Cybernetics (SMC), 2031–2037
