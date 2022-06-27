## Setup Kinect V2 on MacOS


The final solution comes to Kinect V2 + [OpenKinect(Libfreenect 2)](https://github.com/OpenKinect/libfreenect2/blob/master/README.md#macos) Deriver + Pylibfreenect2
Great thanks to [This Bolg](https://www.notaboutmy.life/posts/run-kinect-2-on-ubuntu-20-lts/)

## Installation Of Libfreenect2

Use your favorite package managers (brew, ports, etc.) to install most if not all dependencies:

Make sure these build tools are available: wget, git, cmake, pkg-config. Xcode may provide some of them. Install the rest via package managers.
Download libfreenect2 source

```bash
git clone https://github.com/OpenKinect/libfreenect2.git
cd libfreenect2
#Install dependencies: libusb, GLFW
brew update
brew install libusb
brew install glfw3
#Install TurboJPEG (optional)
brew install jpeg-turbo
#Install CUDA (optional): TODO
#Install OpenNI2 (optional)
brew tap brewsci/science
brew install openni2
export OPENNI2_REDIST=/usr/local/lib/ni2
export OPENNI2_INCLUDE=/usr/local/include/ni2
Build
mkdir build && cd build
cmake ..
make
make install
```

Run the test program: ./bin/Protonect
Test OpenNI2. make install-openni2 (may need sudo), then run NiViewer. Environment variable LIBFREENECT2_PIPELINE can be set to cl, cuda, etc to specify the pipeline.

## Installation Of Pylibfreenect2

```bash
conda activate kinect
pip install wheel
pip install numpy
pip install cython
pip install pylibfreenect2
pip install opencv-python
wget https://raw.githubusercontent.com/r9y9/pylibfreenect2/master/examples/multiframe_listener.py
LIBFREENECT2_INSTALL_PREFIX=$HOME LD_LIBRARY_PATH=$HOME/freenect2/lib python multiframe_listener.py
```

## Note

1. OpenNI2 doesn't seems to support Mac with Apple Silicon, so I don't have any idea of using OpenNI2
2. Libfreenect1 only support Kinect 360 version. Don't mess them up.