# tensorflow-1.4.2 enable AVX MKL
Environment: 

ubuntu 18.04 (or other linux), x86-64, python 2.7


enable SSE4.1 SSE4.2 AVX AVX2 FMA: [whl link](https://github.com/GTGraphics3/tensorflow-1.4.2-AVX-MKL/releases/download/v1.0/tensorflow-1.4.2-cp27-cp27mu-linux_x86_64.whl)

enable MKL: [whl link](https://github.com/GTGraphics3/tensorflow-1.4.2-AVX-MKL/releases/download/v1.0/tensorflow-1.4.2-cp27-cp27mu-mkl-linux_x86_64.whl)





## How to use?

install tensorflow that enable AVX SSE FMA: 

```
wget https://github.com/GTGraphics3/tensorflow-1.4.2-AVX-MKL/releases/download/v1.0/tensorflow-1.4.2-cp27-cp27mu-linux_x86_64.whl
pip install tensorflow-1.4.2-cp27-cp27mu-linux_x86_64.whl
```



## How to build?

### 1. Check which tensorflow & python & Bazel & gcc version you need install

https://www.tensorflow.org/install/source#linux


### 2. install python 

`sudo apt install python-dev python-pip`     for python 2.7
or `sudo apt install python3-dev python3-pip`   for python 3.6


### 3. Install Bazel

[other Bazel version](https://github.com/bazelbuild/bazel/releases) 

```
sudo apt install g++ unzip zip
wget https://github.com/bazelbuild/bazel/releases/download/0.5.4/bazel-0.5.4-installer-linux-x86_64.sh
chmod +x bazel-0.5.4-installer-linux-x86_64.sh
./bazel-0.5.4-installer-linux-x86_64.sh --user
 ```
 `vim ~/.bashrc`
 
 add `export PATH="$PATH:$HOME/bin"` in .bashrc
 
 `source ~/.bashrc`

### 4. Install gcc

`sudo vim /etc/apt/sources.list`

add this 2 line to sources.list

```
deb http://dk.archive.ubuntu.com/ubuntu/ xenial main
deb http://dk.archive.ubuntu.com/ubuntu/ xenial universe
```

```
sudo apt update
sudo apt-get install gcc-4.8
sudo apt-get install g++-4.8
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 20
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.8 20
gcc --version
```


### 5. Download TensorFlow

```
pip install -U --user pip numpy wheel
pip install -U --user keras_preprocessing --no-deps
git clone https://github.com/tensorflow/tensorflow.git
cd tensorflow
git checkout r1.4     # r1.4 is tensorflow 1.4.2
./configure           # all No
```

### 6. Build 

#### build With AVX2/FMA/etc.

```
bazel build --config=opt //tensorflow/tools/pip_package:build_pip_package     # take time
bazel-bin/tensorflow/tools/pip_package/build_pip_package ~/tensorflow_pkg

pip install ~/tensorflow_pkg/tensorflow-1.8.0-cp27-cp27mu-linux_x86_64.whl    # install tensorflow with AVX2/FMA
```

##### build With MKL

```
bazel build --config=opt --config=mkl //tensorflow/tools/pip_package:build_pip_package      # take time
bazel-bin/tensorflow/tools/pip_package/build_pip_package ~/tensorflow_pkg_mkl

pip install ~/tensorflow_pkg_mkl/tensorflow-1.8.0-cp27-cp27mu-linux_x86_64.whl              # install tensorflow with MKL
```


