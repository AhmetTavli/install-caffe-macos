[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![macOS](https://github.com/AhmetTavli/Badge/blob/master/badges/mac_badge.svg)](https://www.apple.com)
[![CMake](https://github.com/AhmetTavli/Badge/blob/master/badges/cmake_badge.svg)](https://cmake.org/)
[![Python](https://github.com/AhmetTavli/Badge/blob/master/badges/python_badge.svg)](https://www.python.org/)
[![OpenCV](https://github.com/AhmetTavli/Badge/blob/master/badges/opencv_badge.svg)](https://opencv.org/)
[![Caffe](https://github.com/AhmetTavli/Badge/blob/master/badges/caffe.svg)](https://caffe.berkeleyvision.org/)

# Caffe Installation Instructions for CPU, Python 3, OpenCV 4
Make sure you've downloaded [caffe-master](https://github.com/BVLC/caffe)

Open the [CMakeList.txt](https://github.com/BVLC/caffe/blob/master/CMakeLists.txt)

Compile Caffe from CMakeList :desktop_computer:
============================

We will be modifying the following lines:

1. Set CPU_ONLY mode on

```cmake
caffe_option(CPU_ONLY  "Build Caffe without CUDA support" ON)
```

2. Add C++11 standard

```cmake
if(UNIX OR APPLE)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC -Wall -std=c++11")
endif()
```

3. Set Python 3

```cmake
set(python_version "3" CACHE STRING "Specify which Python version to use")
```

Optional :bust_in_silhouette:
========
1. [Doxygen](http://www.doxygen.nl/)

DeFacto standard tool for generating the documentation

```cmake
brew install doxygen
```

2. [MATLAB](https://www.mathworks.com/products/get-matlab.html?s_tid=gn_getml)

Set MATLAB Build ON

```cmake
caffe_option(BUILD_matlab "Build Matlab wrapper" ON IF UNIX OR APPLE)
```

Then set the following directories:

![alt_text][matlab_directories]

Compilation :trackball:
===========

4. Set the directories

![alt_text][cmake_directories]

5. Make sure both configureaation and Generation executed successfully

![alt_text][caffe_configuration_summary]

6. Go to the build directory

```shell
make all -j4
```

![alt_text][make_all_success]

7. Install the libraries

```shell
make install
```

![alt_text][make_install]

8. Run test

```shell
make runtest
```

![alt_text][runtest_success]


CV_LOAD_IMAGE_COLOR Error :bangbang:
=========================

If OpenCV Version 4 is installed on your system, you might encountered the following problems: 

![alt_text][error1]
![alt_text][error2]
![alt_text][error3]

# Solution :thinking:

change the followings:

```cpp
 CV_LOAD_IMAGE_COLOR     -> cv::IMREAD_COLOR 
 CV_LOAD_IMAGE_GRAYSACLE -> cv::IMREAD_GRAYSCALE
```

[Source](https://groups.google.com/forum/#!topic/caffe-users/lr10Q5RCiTo)

Below are the changed Links: 

|                                  Download the link                                                 |  Paste in the path  |                                          
|--------------------------------------------------------------------------------------------------- | ------------------- |
| [io.cpp](https://github.com/AhmetTavli/install-caffe-macos/blob/master/updated-for-opencv4/io.cpp) |  caffe-master/src/caffe/util/ |
| [test_io.cpp](https://github.com/AhmetTavli/install-caffe-macos/blob/master/updated-for-opencv4/test_io.cpp) | caffe-master/src/caffe/test/ |
| [window_data_layer.cpp](https://github.com/AhmetTavli/install-caffe-macos/blob/master/updated-for-opencv4/window_data_layer.cpp) | caffe-master/src/caffe/layers/ |


## Contributing :thought_balloon:
Pull requests are welcome.

For major changes, please open an issue, then discuss what you would like to change.

 ## License :scroll:
[MIT](https://opensource.org/licenses/MIT)

[cmake_directories]: https://github.com/AhmetTavli/install-caffe-macos/blob/master/images/build_specification.png "source code:caffe-master, binaries: caffe-master/build"

[matlab_directories]: https://github.com/AhmetTavli/install-caffe-macos/blob/master/images/matlab_directories.png "Need to set the following parameters"

[caffe_configuration_summary]:  https://github.com/AhmetTavli/install-caffe-macos/blob/master/images/caffe_configuration_summary.png "Caffe Summary"

[make_all_success]: https://github.com/AhmetTavli/install-caffe-macos/blob/master/images/make_all_success.png 

[make_install]: https://github.com/AhmetTavli/install-caffe-macos/blob/master/images/make_install.png 

[error1]: https://github.com/AhmetTavli/install-caffe-macos/blob/master/images/error1.png 

[error2]: https://github.com/AhmetTavli/install-caffe-macos/blob/master/images/error2.png 

[error3]: https://github.com/AhmetTavli/install-caffe-macos/blob/master/images/error3.png 

[runtest_success]: https://github.com/AhmetTavli/install-caffe-macos/blob/master/images/runtest_success.png 
