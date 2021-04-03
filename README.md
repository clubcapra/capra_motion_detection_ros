# capra_motion_detection_ros

capra_motion_detection detect motion in a camera feed in ROS

## OpenCV installation

Since ROS Melodic, OpenCV need to be install manually. Although the process is relatively easy.

This section follow the step presented in this article : <http://www.codebind.com/linux-tutorials/install-opencv-3-2-ubuntu-18-04-lts-linux/>

Although it is made to be use with ROS Melodic, which means it install OpenCV 3.2.0.

- 1 Updating Ubuntu
  - `sudo apt update && sudo apt upgrade`
- 2 Install dependencies
  - 2.1 First we need to add an repository & update
    - `sudo add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main"`
    - `sudo apt update`
  - 2.2 Now we install the dependencies
    - `sudo apt install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev python3.6-dev python3-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff5-dev libjasper-dev libdc1394-22-dev libeigen3-dev libtheora-dev libvorbis-dev libxvidcore-dev libx264-dev sphinx-common libtbb-dev yasm libfaac-dev libopencore-amrnb-dev libopencore-amrwb-dev libopenexr-dev libgstreamer-plugins-base1.0-dev libavutil-dev libavfilter-dev libavresample-dev`
- 3 Get OpenCV
  - 3.1 In a shell with root priviledge (`sudo -s`) download OpenCV 3.2.0 and OpenCV-Contrib 3.2.0 in the `/opt` folder
    - 3.1.1 Download OpenCV
      - `wget -cO - https://github.com/opencv/opencv/archive/refs/tags/3.2.0.zip > opencv.3.2.0.zip`
    - 3.1.2 Download OpenCV_contrib
      - `wget -cO - https://github.com/opencv/opencv_contrib/archive/refs/tags/3.2.0.zip > opencv_contrib.3.2.0.zip`
    - 3.2 Decompress the .zip file and rename their folder name to `opencv` and `opencv_contrib`
      - 3.2.1 `unzip opencv.3.2.0.zip -d opencv`
      - 3.2.2 `unzip opencv_contrib.3.2.0.zip -d opencv_contrib`
- 4 Build and Install OpenCV
  - 4.1 Go into opencv folder
    - `cd opencv`
  - 4.2 Create a `release` folder
    - `mkdir release`
  - 4.3 Generate CMake configuration
    - `cmake -D BUILD_TIFF=ON -D WITH_CUDA=OFF -D ENABLE_AVX=OFF -D WITH_OPENGL=OFF -D WITH_OPENCL=OFF -D WITH_IPP=OFF -D WITH_TBB=ON -D BUILD_TBB=ON -D WITH_EIGEN=OFF -D WITH_V4L=OFF -D WITH_VTK=OFF -D BUILD_TESTS=OFF -D BUILD_PERF_TESTS=OFF -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D OPENCV_EXTRA_MODULES_PATH=/opt/opencv_contrib/modules /opt/opencv/`
  - 4.4 Compile OpenCV
    - `make -j4`
  - 4.5 Install OpenCV
    - `make install`
    - `ldconfig`
  - 4.6 Exit terminal
    - `exit`
- 5 Check if OpenCV was install
  - `pkg-config --modversion opencv`
  - It is supposed to return `3.2.0`
- 6 Install OpenCV lib for ROS
  - 6.1 There a library for ROS to use OpenCV
    - image_geometry
    - cv_bridge
    - image_transport
  - 6.2 Install them
    - `sudo apt install ros-melodic-image-geometry ros-melodic-image-transport ros-melodic-cv-bridge`
