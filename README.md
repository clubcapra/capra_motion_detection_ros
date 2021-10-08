# capra_motion_detection_ros

capra_motion_detection detects motion in a camera feed in ROS

## OpenCV installation

Since ROS Melodic, OpenCV needs to be installed manually. However, the process is relatively easy.

This section follow the step presented in this article : <https://linuxize.com/post/how-to-install-opencv-on-ubuntu-18-04/>

Be careful, following the website exactly installs the latest version of OpenCV, which is not functional with this repo. The adjustements are accounted below.

- 1 Updating Ubuntu
  - `sudo apt update && sudo apt upgrade`
- 2 Install dependencies
  - `sudo apt install build-essential cmake git pkg-config libgtk-3-dev libavcodec-dev libavformat-dev libswscale-dev libv4l-dev libxvidcore-dev libx264-dev libjpeg-dev libpng-dev libtiff-dev gfortran openexr libatlas-base-dev python3-dev python3-numpy libtbb2 libtbb-dev libdc1394-22-dev`
- 3 Get the right repositories
    - 3.1 Get the OpenCV and OpenCV contrib repositories
      - `mkdir ~/opencv_build && cd ~/opencv_build`
      `git clone https://github.com/opencv/opencv.git`
      `git clone https://github.com/opencv/opencv_contrib.git`
    - 3.2 Change versions of the repos to 3.2.0
      - 3.2.1 Change version of the OpenCV repository
        - `cd ~/opencv_build/opencv`
        `git checkout 3.2.0`
      - 3.2.2 Change version of the OpenCV_contrib repository
        - `cd ~/opencv_build/opencv_contrib`
        `git checkout 3.2.0`
- 4 Build and Install OpenCV
  - 4.1 Go into opencv folder
    - `cd ~/opencv_build/opencv`
  - 4.2 Create a `build` folder and go to it
    - `mkdir build && cd build`
  - 4.3 Generate CMake configuration
    - `cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D INSTALL_C_EXAMPLES=ON -D INSTALL_PYTHON_EXAMPLES=ON -D OPENCV_GENERATE_PKGCONFIG=ON -D OPENCV_EXTRA_MODULES_PATH=~/opencv_build/opencv_contrib/modules -D BUILD_EXAMPLES=ON .. -DENABLE_PRECOMPILED_HEADERS=OFF`
  - 4.4 Compile OpenCV
    - `make -j4`
  - 4.5 Install OpenCV
    - `sudo make install`
  - 4.6 Exit terminal
    - `exit`
- 5 Check if OpenCV was install
  - `pkg-config --modversion opencv`
  - It should return `3.2.0`
- 6 Install OpenCV lib for ROS
  - 6.1 There a library for ROS to use OpenCV
    - image_geometry
    - cv_bridge
    - image_transport
  - 6.2 Install them
    - `sudo apt install ros-melodic-image-geometry`


## Test with webcam 
- Install `usb_cam` and `rqt_image_view`
  - `sudo apt install ros-melodic-usb-cam ros-melodic-rqt-image-view`
- Reboot
- Launch a roscore in a terminal 
  - `roscore`
- Launch `usb_cam`
  - `rosrun usb_cam usb_cam_node`
- Launch `rqt_image_view`
  - `rosrun rqt_image_view rqt_image_view`
- In the rqt_image_view select the `usb_cam/image_raw` topic
