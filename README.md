# OpenCV GPU Setup

This is a setup page for using camera with GPU access. This can be implemented either in a notebook on the cloud or in a local machine. 

To run Opencv-python using GPU:

```shell
import cv2
net = cv2.dnn.readNetFromCaffe(protoFile, weightsFile)
net.setPreferableBackend(cv2.dnn.DNN_BACKEND_CUDA)
net.setPreferableTarget(cv2.dnn.DNN_TARGET_CUDA)
```

But running the same code will be resulting in a error.

To solve this issue, we need to install cv2 ourselves.

Run the code in order:

```shell
%cd /content
```
```shell
!git clone https://github.com/opencv/opencv
```
```shell
!git clone https://github.com/opencv/opencv_contrib
```
```shell
!mkdir /content/build
```
```shell
%cd /content/build
```
```shell
!cmake -DOPENCV_EXTRA_MODULES_PATH=/content/opencv_contrib/modules  -DBUILD_SHARED_LIBS=OFF  -DBUILD_TESTS=OFF  -DBUILD_PERF_TESTS=OFF -DBUILD_EXAMPLES=OFF -DWITH_OPENEXR=OFF -DWITH_CUDA=ON -DWITH_CUBLAS=ON -DWITH_CUDNN=ON -DOPENCV_DNN_CUDA=ON /content/opencv
```
```shell
!make -j8 install
```

After completion you can check the version of OpenCV.

```shell
import cv2
cv2.__version__
```

Now you should be able to set the dnn to CUDA without error

```shell
net.setPreferableBackend(cv2.dnn.DNN_BACKEND_CUDA)
net.setPreferableTarget(cv2.dnn.DNN_TARGET_CUDA)
```

But the first step takes a lot of time, and you need to do it every time you start
the notebook. This is time-consuming and not ideal.

One thing you can do here is to save the result of the first step to your Google
Drive (you have to mount it).

```shell
!mkdir  "/content/gdrive/My Drive/cv2_gpu"
!cp  /content/build/lib/python3/cv2.cpython-36m-x86_64-linux-gnu.so   "/content/gdrive/My Drive/cv2_gpu"
```

Then copy it to your working directory next time you start the notebook

```shell
!cp "/content/gdrive/My Drive/cv2_gpu/cv2.cpython-36m-x86_64-linux-gnu.so"
```
