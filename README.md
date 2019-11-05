## OpenCV: Open Source Computer Vision Library

### Resources

* Homepage: <https://opencv.org>
* Docs: <https://docs.opencv.org/master/>
* Q&A forum: <http://answers.opencv.org>
* Issue tracking: <https://github.com/opencv/opencv/issues>

### Contributing

Please read the [contribution guidelines](https://github.com/opencv/opencv/wiki/How_to_contribute) before starting work on a pull request.

#### Summary of the guidelines:

* One pull request per issue;
* Choose the right base branch;
* Include tests and documentation;
* Clean up "oops" commits before submitting;
* Follow the [coding style guide](https://github.com/opencv/opencv/wiki/Coding_Style_Guide).

### Fork of OpenCV 4.1.0
* Added Y16 / GRAY16_LE support on VideoCapture with GStreamer

### Installation Guide with GStreamer

##### First install GStreamer

```
sudo apt-get install gstreamer1.0*
sudo apt install ubuntu-restricted-extras
```

##### Install lib packages

```
sudo apt install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev
```

##### Create python3 virtual environment and install numpy

NOTE: virtualenv can be installed with sudo pip3 install virtualenv
```
virtualenv -p python3 ~/venv
source ~/venv/bin/activate
pip install numpy
```

##### Clone forked repository

```
git clone https://github.com/DaniDeniz/opencv.git
cd opencv
```

##### Build OpenCV

```
mkdir build
cd build
```

```
cmake -D CMAKE_BUILD_TYPE=RELEASE \
-D CMAKE_INSTALL_PREFIX=/usr/local \
-D INSTALL_PYTHON_EXAMPLES=ON \
-D INSTALL_C_EXAMPLES=OFF \
-D PYTHON_EXECUTABLE=$(which python3) \
-D BUILD_opencv_python2=OFF \
-D CMAKE_INSTALL_PREFIX=$(python3 -c "import sys; print(sys.prefix)") \
-D PYTHON3_EXECUTABLE=$(which python3) \
-D PYTHON3_INCLUDE_DIR=$(python3 -c "from distutils.sysconfig import get_python_inc; print(get_python_inc())") \
-D PYTHON3_PACKAGES_PATH=$(python3 -c "from distutils.sysconfig import get_python_lib; print(get_python_lib())") \
-D WITH_GSTREAMER=ON \
-D BUILD_EXAMPLES=ON ..
```

```
make -j$(nproc)
```

##### Install package

```
sudo make install
sudo ldconfig
```



