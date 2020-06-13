---
layout: post
title: Intel® Edge AI Fundamentals Course
---

Intel® Edge AI Fundamentals Course is the first phase of the Intel® Edge AI Scholarship Program to train on job relevant skills in Intel® Distribution of OpenVINO™ toolkit fundamentals.

This is a guide to help you walk through the course and deepen your understanding (e.g. what is a meaning of the command you're running). Especially, this focuses on the Exercise sections.

# Prerequisites
- Work on Intel® Edge AI Fundamentals Course on [Intel® Edge AI Scholarship Program](https://www.udacity.com/scholarships/intel-edge-ai-scholarship) or Intel® Edge AI for IoT Developers Nano degree (Not yet available now)

# Goal
Finish Intel® Edge AI Fundamentals Course sucessfully.

# Lesson 2: Leveraging Pre-Trained Models

In this lesson's exercise, you will do the following things:

- Choosing the right Pre-Trained Model for your App
- Loading and Deploying a Basic App with a Pre-Trained Model

## Leveraging Pre-Trained Models
### Loading Pre-Trained Models
The models are available in OpenVINO™ as pre-trained models like:

- Text Detection

- Pose Detection

- Roadside Segmentation

- Pedestrian Detection

You can check out the full list of pre-trained models available in the Intel® Distribution of OpenVINO™ [here](https://software.intel.com/en-us/openvino-toolkit/documentation/pretrained-models).

On the [Intel® Edge AI Fundamentals Course](https://www.udacity.com/scholarships/intel-edge-ai-scholarship), you can see this workspace.

{% include helpers/image.html name="Screen Shot 2019-12-25 at 22.35.27.png" %}

### Find the Right Models

first, press `SOURCE ENV` button (to source the correct environment).

<details>
<summary>log</summary>

<pre>
root@a2c7959d88c3:/home/workspace# pip install requests pyyaml -t /usr/local/lib/python.5/dist-packages && clear && source /opt/intel/openvino/bin/setupvars.sh -pyver 3.5Collecting requests  Downloading https://files.pythonhosted.org/packages/51/bd/23c926cd341ea6b7dd0b2a00aba99ae0f828be89d72b2190f27c11d4b7fb/requests-2.22.0-py2.py3-none-any.whl (57kB)
    100% |████████████████████████████████| 61kB 2.6MB/s
Collecting pyyaml
  Downloading https://files.pythonhosted.org/packages/8d/c9/e5be955a117a1ac548cdd31e37e8fd7b02ce987f9655f5c7563c656d5dcb/PyYAML-5.2.tar.gz (265kB)
python_version = 3.5
[setupvars.sh] OpenVINO environment initialized
(venv) root@a2c7959d88c3:/home/workspace#
</pre>
</details>

Using the [Pre-Trained Model list](https://software.intel.com/en-us/openvino-toolkit/documentation/pretrained-models), determine which models could accomplish the following tasks:

- Human Pose Estimation

- Text Detection

- Determining Car Type & Color

You obviously find out the correct models, if you goes to the [Pre-Trained Model list page](https://software.intel.com/en-us/openvino-toolkit/documentation/pretrained-models)

{% include helpers/image.html name="Screen Shot 2019-12-26 at 19.28.11.png" %}

### Download the Models

Once you have found the right models, download them into the workspace with the precision levels:

- Human Pose Estimation: All precision levels

- Text Detection: FP16 only

- Determining Car Type & Color: INT8 only

In the first documentation page of each model, the ttitle at the top of the page is the model name to use for downloading. Below example image of Human Pose Estimation shows the name, `human-pose-estimation-0001`.

{% include helpers/image.html name="Screen Shot 2019-12-27 at 21.25.19.png" %}

Using [downloader.py](http://docs.openvinotoolkit.org/latest/_tools_downloader_README.html) and options specifing precision levels, download the models.

First, go to the openvino downloader directory:

```
# cd /opt/intel/openvino/deployment_tools/open_model_zoo/tools/downloader
```

> `cd` - command changes directories

<details>
<summary>log</summary>

<pre>
(venv) root@a2c7959d88c3:/home/workspace# cd /opt/intel/openvino/deployment_to
ols/open_model_zoo/tools/downloader
(venv) root@a2c7959d88c3:/opt/intel/openvino/deployment_tools/open_model_zoo/t
ools/downloader# ls -l
total 292
-rw-r--r-- 1 root root  17645 Dec  5 23:48 common.py-rwxr-xr-x 1 root root   8263 Dec  5 23:48 converter.py
-rwxr-xr-x 1 root root  10631 Dec  5 23:48 downloader.py-rwxr-xr-x 1 root root   1954 Dec  5 23:48 info_dumper.py
-rw-r--r-- 1 root root 213663 Dec  5 23:48 license.txt
-rw-r--r-- 1 root root   4802 Dec  5 23:48 pytorch_to_onnx.py
-rw-r--r-- 1 root root  14188 Dec  5 23:48 README.md
-rw-r--r-- 1 root root     16 Dec  5 23:48 requirements.in
-rw-r--r-- 1 root root     57 Dec  5 23:48 requirements-pytorch.in
(venv) root@a2c7959d88c3:/opt/intel/openvino/deployment_tools/open_model_zoo/t
ools/downloader#
</pre>
</details>

<br>
For Human Pose Estimation: All precision levels:

```
# ./downloader.py --name human-pose-estimation-0001 -o /home/workspace
```

> `--name human-pose-estimation-0001` - --name option specifies the identifier of the model for downloading (this case, human-pose-estimation-0001)
>
> `-o /home/workspace` - -o option specifies the output directory

<details>
<summary>log</summary>

<pre>
(venv) root@a2c7959d88c3:/opt/intel/openvino/deployment_tools/open_model_zoo/tools/downloader# ./downloader.py --name human-pose-estimation-0001 -o /home/workspace
################|| Downloading models ||################

========== Downloading /home/workspace/intel/human-pose-estimation-0001/FP32/h
uman-pose-estimation-0001.xml
... 100%, 65 KB, 943 KB/s, 0 seconds passed

========== Downloading /home/workspace/intel/human-pose-estimation-0001/FP32/h
uman-pose-estimation-0001.bin
... 100%, 16010 KB, 59127 KB/s, 0 seconds passed

========== Downloading /home/workspace/intel/human-pose-estimation-0001/FP16/human-pose-estimation-0001.xml
... 100%, 64 KB, 868 KB/s, 0 seconds passed

========== Downloading /home/workspace/intel/human-pose-estimation-0001/FP16/human-pose-estimation-0001.bin
... 100%, 8005 KB, 63517 KB/s, 0 seconds passed

========== Downloading /home/workspace/intel/human-pose-estimation-0001/INT8/human-pose-estimation-0001.xml
... 100%, 596 KB, 2700 KB/s, 0 seconds passed

========== Downloading /home/workspace/intel/human-pose-estimation-0001/INT8/human-pose-estimation-0001.bin
... 100%, 16010 KB, 67096 KB/s, 0 seconds passed

################|| Post-processing ||################

(venv) root@a2c7959d88c3:/opt/intel/openvino/deployment_tools/open_model_zoo/tools/downloader#
</pre>
</details>

<br>
For Text Detection: FP16 only:

```
# ./downloader.py --name text-detection-0004 --precisions FP16 -o /home/workspace
```

> `--name text-detection-0004` - choosing text-detection-0004 model
>
> `--precisions FP16` - --precisions flag to specify precision. By default, the script will produce models in every precision that is supported for conversion. and FP16 stands for floating point 16 which is related to precision level

<details>
<summary>log</summary>

<pre>
(venv) root@a2c7959d88c3:/opt/intel/openvino/deployment_tools/open_model_zoo/tools/downloader# ./downloader.py --name text-detection-0004 --precisions FP16 -o /home/workspace
################|| Downloading models ||################

========== Downloading /home/workspace/intel/text-detection-0004/FP16/text-detection-0004.xml
... 100%, 70 KB, 1052 KB/s, 0 seconds passed

========== Downloading /home/workspace/intel/text-detection-0004/FP16/text-detection-0004.bin
... 100%, 8453 KB, 55382 KB/s, 0 seconds passed

################|| Post-processing ||################

(venv) root@a2c7959d88c3:/opt/intel/openvino/deployment_tools/open_model_zoo/tools/downloader#
</pre>
</details>

<br>
For Determining Car Type & Color: INT8 only:

```
# ./downloader.py --name vehicle-attributes-recognition-barrier-0039 --precisions INT8 -o /home/workspace
```

> `--precisions INT8` - INT8 stands for integer 8 which is related to precision level

<details>
<summary>log</summary>

<pre>
(venv) root@a2c7959d88c3:/opt/intel/openvino/deployment_tools/open_model_zoo/tools/downloader# ./downloader.py --name vehicle-attributes-recognition-barrier-0039 --precisions INT8 -o /home/workspace
################|| Downloading models ||################

========== Downloading /home/workspace/intel/vehicle-attributes-recognition-barrier-0039/INT8/vehicle-attributes-recognition-barrier-0039.xml
... 100%, 62 KB, 713 KB/s, 0 seconds passed

========== Downloading /home/workspace/intel/vehicle-attributes-recognition-barrier-0039/INT8/vehicle-attributes-recognition-barrier-0039.bin
... 100%, 2445 KB, 38410 KB/s, 0 seconds passed

################|| Post-processing ||################

(venv) root@a2c7959d88c3:/opt/intel/openvino/deployment_tools/open_model_zoo/tools/downloader
</pre>
</details>

### Verify the Downloads

To verify the download of these models by navigating to `/home/workspace/intel`.

```
# cd /home/workspace/intel
```

<details>
<summary>log</summary>

<pre>
(venv) root@a2c7959d88c3:/opt/intel/openvino/deployment_tools/open_model_zoo/tools/downloader# cd /home/workspace/intel
(venv) root@a2c7959d88c3:/home/workspace/intel#
</pre>
</details>

<br>
you should see three directories - one for each downloaded model (`human-pose-estimation-0001`, `text-detection-0004`, and `vehicle-attributes-recognition-barrier-0039`) with listing command `ls -l`.

```
# ls -l
```

> `ls -l` - `ls` command to lists files and directories within the current directory. With the `-l` option, `ls` will list out files and directories in long list format.

<details>
<summary>log</summary>

<pre>
(venv) root@a2c7959d88c3:/home/workspace/intel# ls -l
total 12
drwxr-xr-x 5 root root 4096 Dec 26 12:48 human-pose-estimation-0001
drwxr-xr-x 3 root root 4096 Dec 26 13:12 text-detection-0004
drwxr-xr-x 3 root root 4096 Dec 26 13:23 vehicle-attributes-recognition-barrier-0039
</pre>
</details>

<br>
Within those directories, there should be separate subdirectories for the precisions that were downloaded, and then `.xml` and `.bin` files within those subdirectories, that make up the model. `tree` command will you to check those more easily.

```
# tree
```

> `tree` - command to display the content of a directory in a tree-like format
>
> `.xml` - xml is a format like .txt, text.
>
> `.bin` - bin stands for binary file, which is the format computer able to read.

<details>
<summary>log</summary>

<pre>
(venv) root@a2c7959d88c3:/home/workspace/intel# tree
.
├── human-pose-estimation-0001
│   ├── FP16
│   │   ├── human-pose-estimation-0001.bin
│   │   └── human-pose-estimation-0001.xml
│   ├── FP32
│   │   ├── human-pose-estimation-0001.bin
│   │   └── human-pose-estimation-0001.xml
│   └── INT8
│       ├── human-pose-estimation-0001.bin
│       └── human-pose-estimation-0001.xml
├── text-detection-0004
│   └── FP16
│       ├── text-detection-0004.bin
│       └── text-detection-0004.xml
└── vehicle-attributes-recognition-barrier-0039
    └── INT8
        ├── vehicle-attributes-recognition-barrier-0039.bin
        └── vehicle-attributes-recognition-barrier-0039.xml

8 directories, 10 files
(venv) root@a2c7959d88c3:/home/workspace/intel#
</pre>
</details>

## Preprocessing Inputs

Make sure to click the `SOURCE ENV` button before you get started to source the correct environment.

{% include helpers/image.html name="Screen Shot 2019-12-27 at 22.19.40.png" %}

<br>
<details>
<summary>log</summary>

<pre>
root@7d6bb1391047:/home/workspace# source /opt/intel/openvino/bin/setupvars.sh -pyver 3.5
python_version = 3.5
[setupvars.sh] OpenVINO environment initialized
(venv) root@7d6bb1391047:/home/workspace#
</pre>
</details>

In this exercise, we will preprocess the inputs for each of the models below:

- Human Pose Estimation: [human-pose-estimation-0001](https://docs.openvinotoolkit.org/latest/_models_intel_human_pose_estimation_0001_description_human_pose_estimation_0001.html)

- Text Detection: [text-detection-0004](http://docs.openvinotoolkit.org/latest/_models_intel_text_detection_0004_description_text_detection_0004.html)

- Determining Car Type & Color: [vehicle-attributes-recognition-barrier-0039](https://docs.openvinotoolkit.org/latest/_models_intel_vehicle_attributes_recognition_barrier_0039_description_vehicle_attributes_recognition_barrier_0039.html)

you could find these pre-downloaded models' binary file (.bin) and xml file (.xml) under `/home/workspace/models` on your workspace.

```
# cd /home/workspace/models
# ls -l
```

<details>
<summary>log</summary>

<pre>
root@2a5542b94277:/home/workspace# cd /home/workspace/models
root@2a5542b94277:/home/workspace/models# ls -l
total 32336
-rw-r--r-- 1 root root  8197360 Dec 12 23:48 human-pose-estimation-0001.bin
-rw-r--r-- 1 root root    66557 Dec 12 23:48 human-pose-estimation-0001.xml
-rw-r--r-- 1 root root 13371780 Dec 12 23:48 semantic-segmentation-adas-0001.bin
-rw-r--r-- 1 root root    90790 Dec 12 23:48 semantic-segmentation-adas-0001.xml
-rw-r--r-- 1 root root  8655952 Dec 12 23:48 text-detection-0004.bin
-rw-r--r-- 1 root root    71863 Dec 12 23:48 text-detection-0004.xml
-rw-r--r-- 1 root root  2504004 Dec 12 23:48 vehicle-attributes-recognition-barrier-0039.bin
-rw-r--r-- 1 root root    64190 Dec 12 23:48 vehicle-attributes-recognition-barrier-0039.xml
root@2a5542b94277:/home/workspace/models#
</pre>
</details>

### Human Pose Estimation

This section explains all concepts we faces so it little bit longer but the robust understnading of those commands and code will empower you to go through the rest of the exercise with fulfilment feeling.

Check the [input section](https://docs.openvinotoolkit.org/latest/_models_intel_human_pose_estimation_0001_description_human_pose_estimation_0001.html#inputs) of the `human-pose-estimation-0001` model to make sure what is input expectation.

The expectations are:

| name | B (batch size) | C (number of color channels) | H (image height) | W (image width) | color order |
|-------|----------------|------------------------|------------------|-----------------|-------------|
| input | 1 | 3 | 256 | 456 | BGR |

> B (batch size) - The batch size means the number of images that will be read through the pre-trained model.
>
> C (number of color channels) - it indeicates if image is color or not. If image is grayscale, tuple returned contains only number of rows and columns.

The currently loaded image is in the format BGR with H, W, C order. You will adjust the input image to the above input prerequisites using `preprocess_inputs.py`.

First, you may notice the `import` statement on the top of the file.

```
import cv2
import numpy as np
```

> `import cv2` - import statement to use the OpenCV package in code  
> [OpenCV Tutorial: A Guide to Learn OpenCV](https://www.pyimagesearch.com/2018/07/19/opencv-tutorial-a-guide-to-learn-opencv/)
>
> `import numpy as np` - this imports the numpy package in code and as np statement make it accessible using np in your code

look at the `pose_estimation` function that is used for formating images on `preprocess_inputs.py` at the right top of your workspace.

```
def pose_estimation(input_image):
    '''
    Given some input image, preprocess the image so that
    it can be used with the related pose estimation model
    you downloaded previously. You can use cv2.resize()
    to resize the image.
    '''
    preprocessed_image = np.copy(input_image)

    # TODO: Preprocess the image for the pose estimation model

    return preprocessed_image
```

> `def pose_estimation(input_image):` - using def keyword defines this function named pose_estimation and the input_image argument can be passed into function.
>
> `preprocessed_image = np.copy(input_image)` - this `copy()` function on np copies the image as `numpy.ndarray` which is an object stands for a N-dimensional array and then the returning copy assignes to the preprocessed_image variable. Here `copy()` function works the same as python's `deepcopy()` which means it constructs a new compound object without references.  
> Reference: [8.10. copy — Shallow and deep copy operations](https://docs.python.org/3.5/library/copy.html)
>
> `return preprocessed_image` - return the value of preprocessed_image which is literally processed image on pose_estimation function

To meet the image size expectation, add below to resize the input image.

```
preprocessed_image = cv2.resize(preprocessed_image, (456, 256))
```

> `preprocessed_image = cv2.resize(preprocessed_image, (456, 256))` - resize function of cv2 resizes the preprocessed_image to the desired size, 456 x 256 pixels. resized image assignes preprocessed_image again.

Now check the ndarray shape information and ndarray itself with print statement which is also useful on debugging. The `pose_estimation` function looks like this:

```
def pose_estimation(input_image):
    # omitted some text
    preprocessed_image = np.copy(input_image)

    preprocessed_image = cv2.resize(preprocessed_image, (456, 256))
    print('Shape: {}'.format(preprocessed_image.shape))
    print(preprocessed_image)

    return preprocessed_image
```

> `print('Shape: {}'.format(preprocessed_image.shape))` - this prints "Shape: {}" and the brackets { and } within them are replaced with the preprocessed_image.shape which refers to shape attribute of preprocessed_image ndarray, passed into the str.format() method. So finally it prints like "Shape: (256, 456, 3)" on your console  
> Reference: [7.1. Fancier Output Formatting](https://docs.python.org/3/tutorial/inputoutput.html#fancier-output-formatting)
>
> `print(preprocessed_image)` - this prints preprocessed_image ndarray itself that is 3d array (256, 456, 3)

Run the prepared test on `/home/workspace` directory on your console

```
python test.py
```

<details>
<summary>log</summary>

<pre>
root@5b564e118360:/home/workspace# python test.py
Shape: (256, 456, 3)
[[[254 211 138]
  [255 212 139]
  [254 211 138]
  ...,
  [255 225 176]
  [253 226 175]
  [253 227 181]]

 [[255 212 139]
  [255 213 140]
  [255 213 140]
  ...,
  [255 230 176]
  [255 229 173]
  [254 227 177]]

 [[253 212 139]
  [254 213 140]
  [254 213 140]
  ...,
  [254 227 177]
  [253 230 184]
  [255 237 200]]

 ...,
 [[ 70  50  43]
  [ 75  52  46]
  [ 73  49  43]
  ...,
  [217 233 246]
  [211 228 241]
  [220 238 250]]

 [[ 69  51  40]
  [ 74  53  45]
  [ 75  51  45]
  ...,
  [216 230 242]
  [220 236 247]
  [206 223 234]]

 [[ 67  50  36]
  [ 69  49  38]
  [ 70  47  39]
  ...,
  [214 228 240]
  [205 221 233]
  [223 239 251]]]
# omitted ... (explains later)
root@5b564e118360:/home/workspace#
</pre>
</details>

For now, your ndarray of images looks like this:

```
[[[254 211 138]
  [255 212 139]
  [254 211 138]
  ...,
  [255 225 176]
  [253 226 175]
  [253 227 181]]

 [[255 212 139]
  [255 213 140]
  [255 213 140]
  ...,
  [255 230 176]
  [255 229 173]
  [254 227 177]]

 [[253 212 139]
  [254 213 140]
  [254 213 140]
  ...,
  [254 227 177]
  [253 230 184]
  [255 237 200]]

 ...,
 [[ 70  50  43]
  [ 75  52  46]
  [ 73  49  43]
  ...,
  [217 233 246]
  [211 228 241]
  [220 238 250]]

 [[ 69  51  40]
  [ 74  53  45]
  [ 75  51  45]
  ...,
  [216 230 242]
  [220 236 247]
  [206 223 234]]

 [[ 67  50  36]
  [ 69  49  38]
  [ 70  47  39]
  ...,
  [214 228 240]
  [205 221 233]
  [223 239 251]]]
```

The first level of this compound list preprocessed_image has exactly 256 rows (omitted above), as the first dimension of the array a (# of rows/ image width here).

Each of these elements is itself a list with 456 elements (omitted also), which is equal to the second dimension of a (# of columns/ image height)

```
# omitted ...
 [[254 211 138]
  [255 212 139]
  [254 211 138]
  ...,
  [255 225 176]
  [253 226 175]
  [253 227 181]]
# omitted ...
```

Finally, the most nested lists have 3 elements each, same as the third dimension of a (# of depth/ BGR colors).
below example is composed of three components: Blue 253 (0-255), Green 227 (0-255) and Red 181 (0-255).

```
[253 227 181]
```

Reference: [3-dimensional array in numpy](https://stackoverflow.com/questions/22981845/3-dimensional-array-in-numpy)  
Reference: [What exactly is BGR color space?](https://stackoverflow.com/questions/367449/what-exactly-is-bgr-color-space)

<br>
To format C, H, W order in the image, use transpose function.

```
preprocessed_image = preprocessed_image.transpose((2,0,1))
```

> `preprocessed_image = preprocessed_image.transpose((2,0,1))` - transpose function of numpy.ndarray with tuple data type of ints, converts the shape of image ndarray from (256, 456, 3) to (3, 256, 456).  
> above taple is (2,0,1) which means that 3-rd dimension becomes 1-st dimension, 1-st dimension becomes 2-nd dimension, and 2-nd dimension becomes 3-rd dimension.  
> Importantly, they are numbered starting with 0 in the taple (2,0,1).  
> make sure you are working on 3-dimensional array and shape is information about this array.  
> For more transpose function, [numpy.ndarray.transpose](https://docs.scipy.org/doc/numpy/reference/generated/numpy.ndarray.transpose.html)  
> Reference: [NUMPY AXES EXPLAINED](https://www.sharpsightlabs.com/blog/numpy-axes-explained/)

Check ndarray of `preprocessed_image` with `pose_estimation` function which looks like:

```
def pose_estimation(input_image):
    # omitted some text
    preprocessed_image = np.copy(input_image)

    preprocessed_image = cv2.resize(preprocessed_image, (456, 256))
    print('Shape before: {}'.format(preprocessed_image.shape))
    preprocessed_image = preprocessed_image.transpose((2,0,1))
    print('Shape after: {}'.format(preprocessed_image.shape))
    print(preprocessed_image)

    return preprocessed_image
```

Run test.py
```
python test.py
```

<details>
<summary>log</summary>

<pre>
root@5b564e118360:/home/workspace# python test.py
Shape before: (256, 456, 3)
Shape after: (3, 256, 456)
[[[254 255 254 ..., 255 253 253]
  [255 255 255 ..., 255 255 254]
  [253 254 254 ..., 254 253 255]
  ...,
  [ 70  75  73 ..., 217 211 220]
  [ 69  74  75 ..., 216 220 206]
  [ 67  69  70 ..., 214 205 223]]

 [[211 212 211 ..., 225 226 227]
  [212 213 213 ..., 230 229 227]
  [212 213 213 ..., 227 230 237]
  ...,
  [ 50  52  49 ..., 233 228 238]
  [ 51  53  51 ..., 230 236 223]
  [ 50  49  47 ..., 228 221 239]]

 [[138 139 138 ..., 176 175 181]
  [139 140 140 ..., 176 173 177]
  [139 140 140 ..., 177 184 200]
  ...,
  [ 43  46  43 ..., 246 241 250]
  [ 40  45  45 ..., 242 247 234]
  [ 36  38  39 ..., 240 233 251]]]
# omitted ...
root@5b564e118360:/home/workspace#
</pre>
</details>

Finally, add an extra batch dimension for the desired input shape (batch size, # of channels, height, width) using "reshape" function:

```
preprocessed_image=preprocessed_image.reshape(1, 3, 256, 456)
```

Check `preprocessed_image` adding print after above statement

```
def pose_estimation(input_image):
    # omitted ...
    preprocessed_image = np.copy(input_image)

    preprocessed_image = cv2.resize(preprocessed_image, (456, 256))
    preprocessed_image = preprocessed_image.transpose((2,0,1))
    preprocessed_image = preprocessed_image.reshape(1, 3, 256, 456)
    print('Shape: {}'.format(preprocessed_image.shape))
    print(preprocessed_image)

    return preprocessed_image
```

> `preprocessed_image = preprocessed_image.reshape(1, 3, 256, 456)` - To add one more dimension for batch to reshape the image array from (3, h, w) to (1, 3, h, w).

Run
```
python test.py
```

<details>
<summary>log</summary>

<pre>
root@5b564e118360:/home/workspace# python test.py
Shape: (1, 3, 256, 456)
[[[[254 255 254 ..., 255 253 253]
   [255 255 255 ..., 255 255 254]
   [253 254 254 ..., 254 253 255]
   ...,
   [ 70  75  73 ..., 217 211 220]
   [ 69  74  75 ..., 216 220 206]
   [ 67  69  70 ..., 214 205 223]]

  [[211 212 211 ..., 225 226 227]
   [212 213 213 ..., 230 229 227]
   [212 213 213 ..., 227 230 237]
   ...,
   [ 50  52  49 ..., 233 228 238]
   [ 51  53  51 ..., 230 236 223]
   [ 50  49  47 ..., 228 221 239]]

  [[138 139 138 ..., 176 175 181]
   [139 140 140 ..., 176 173 177]
   [139 140 140 ..., 177 184 200]
   ...,
   [ 43  46  43 ..., 246 241 250]
   [ 40  45  45 ..., 242 247 234]
   [ 36  38  39 ..., 240 233 251]]]]
Passed Pose Estimation test.
Failed Text Detection test, did not obtain expected preprocessed image.
Failed Car Meta test, did not obtain expected preprocessed image.
You passed 1 of 3 tests.
See above for additional feedback.
root@5b564e118360:/home/workspace#
</pre>
</details>

Now you notice the additional dimension for batch size on the shape and the extra square braces on the preprocessed_image itself

The bottom text says that "Passed Pose Estimation test." and finished pre-processing for Pose Estimation pre-trained model.

If you don't need the print statement you can comment out or delete them from your code.

The final `preprocessed_image` function looks like:

```
def pose_estimation(input_image):
    # omitted ...
    preprocessed_image = np.copy(input_image)

    preprocessed_image = cv2.resize(preprocessed_image, (456, 256))
    preprocessed_image = preprocessed_image.transpose((2,0,1))
    preprocessed_image=preprocessed_image.reshape(1, 3, 256, 456)

    return preprocessed_image
```

### Text Detection

In the same way, check the [input section](http://docs.openvinotoolkit.org/latest/_models_intel_text_detection_0004_description_text_detection_0004.html#inputs) of the `text-detection-0004` model to make sure what is input expectation.

the summary of expectations is:

| name | B (batch size) | C (number of color channels) | H (image height) | W (image width) | color order |
|-------|----------------|------------------------|------------------|-----------------|-------------|
| input | 1 | 3 | 768 | 1280 | BGR |

The currently loaded image is in the format BGR with H, W, C order. So no need to change the color order here but H, W, C order to C, H, W order and add B (batch size).

Move on the `text_detection` function on `preprocess_inputs.py`.

```
def text_detection(input_image):
    '''
    Given some input image, preprocess the image so that
    it can be used with the related text detection model
    you downloaded previously. You can use cv2.resize()
    to resize the image.
    '''
    preprocessed_image = np.copy(input_image)

    # TODO: Preprocess the image for the text detection model

    return preprocessed_image
```

The only difference from what we did before is image height and image width.

copy and paste the code from `pose_estimation` function, and replace 456 to 1280 and 256 to 768.

the function looks like:

```
def text_detection(input_image):
    # omitted
    preprocessed_image = np.copy(input_image)

    preprocessed_image = cv2.resize(preprocessed_image, (1280, 768))
    preprocessed_image = preprocessed_image.transpose((2,0,1))
    preprocessed_image=preprocessed_image.reshape(1, 3, 768, 1280)

    return preprocessed_image
```

Run `python test.py` on the `/home/workspace`

<details>
<summary>log</summary>

<pre>
root@5b564e118360:/home/workspace# python test.py
Passed Pose Estimation test.
Passed Text Detection test.
Failed Car Meta test, did not obtain expected preprocessed image.
You passed 2 of 3 tests.
See above for additional feedback.
root@5b564e118360:/home/workspace#
</pre>
</details>

As you can see, the Text Detection test are passed. pre-processing are done for `text-detection-0004`.

### Determining Car Type & Color

As the same manner to the above two models, check the [input section](https://docs.openvinotoolkit.org/latest/_models_intel_vehicle_attributes_recognition_barrier_0039_description_vehicle_attributes_recognition_barrier_0039.html#inputs) of the `text-detection-0004` model to make sure what is input expectation.

The summary is:

| name | B (batch size) | C (number of color channels) | H (image height) | W (image width) | color order |
|-------|----------------|------------------------|------------------|-----------------|-------------|
| input | 1 | 3 | 72 | 72 | BGR |

Again, the only difference from what we did before is image height and width.

Copy and paste the code from `pose_estimation` function, and replace 456 to 72 and 256 to 72.

The function looks like:

```
def text_detection(input_image):
    # omitted
    preprocessed_image = np.copy(input_image)

    preprocessed_image = cv2.resize(preprocessed_image, (72, 72))
    preprocessed_image = preprocessed_image.transpose((2,0,1))
    preprocessed_image=preprocessed_image.reshape(1, 3, 72, 72)

    return preprocessed_image
```

Then run `python test.py`

<details>
<summary>log</summary>

<pre>
root@5b564e118360:/home/workspace# python test.py
Passed Pose Estimation test.
Passed Text Detection test.
Passed Car Meta test.
You passed 3 of 3 tests.
Congratulations!
root@5b564e118360:/home/workspace#
</pre>
</details>

It passed all tests and is done pre-processing for all three models, `human-pose-estimation-0001`, `text-detection-0004`, and `vehicle-attributes-recognition-barrier-0039`.

### Solution: Pre-processing Inputs

 For each model, we ended up noticing they needed essentially the same preprocessing, outside of the height and width of the input to the network.

 Add a helper function called `preprocessing` which can be passed in input_image, height, width.

 In the function, make sure to use height and width local veriables.

 ```
 def preprocessing(input_image, height, width):
    '''
    Given an input image, height and width:
    - Resize to height and width
    - Transpose the final "channel" dimension to be first
    - Reshape the image to add a "batch" of 1 at the start
    '''
    image = cv2.resize(input_image, (width, height))
    image = image.transpose((2,0,1))
    image = image.reshape(1, 3, height, width)

    return image
 ```

Now you can replace the dupricated three-line codes on each preprocessing functions

<details>
<summary>The Solution code</summary>

<pre>
import cv2
import numpy as np

def preprocessing(input_image, height, width):
   '''
   Given an input image, height and width:
   - Resize to height and width
   - Transpose the final "channel" dimension to be first
   - Reshape the image to add a "batch" of 1 at the start
   '''
   image = cv2.resize(input_image, (width, height))
   image = image.transpose((2,0,1))
   image = image.reshape(1, 3, height, width)

   return image

def pose_estimation(input_image):
    '''
    Given some input image, preprocess the image so that
    it can be used with the related pose estimation model
    you downloaded previously. You can use cv2.resize()
    to resize the image.
    '''
    preprocessed_image = np.copy(input_image)

    preprocessed_image = preprocessing(preprocessed_image, 256, 456)

    return preprocessed_image


def text_detection(input_image):
    '''
    Given some input image, preprocess the image so that
    it can be used with the related text detection model
    you downloaded previously. You can use cv2.resize()
    to resize the image.
    '''
    preprocessed_image = np.copy(input_image)

    preprocessed_image = preprocessing(preprocessed_image, 768, 1280)

    return preprocessed_image


def car_meta(input_image):
    '''
    Given some input image, preprocess the image so that
    it can be used with the related car metadata model
    you downloaded previously. You can use cv2.resize()
    to resize the image.
    '''
    preprocessed_image = np.copy(input_image)

    preprocessed_image = preprocessing(preprocessed_image, 72, 72)

    return preprocessed_image
</pre>
</details>

To test this implementation, you can just run `python test.py` again.

<details>
<summary>log</summary>

<pre>
(venv) root@0bc31b756b55:/home/workspace# python test.py
Passed Pose Estimation test.
Passed Text Detection test.
Passed Car Meta test.
You passed 3 of 3 tests.
Congratulations!
</pre>
</details>

It is still working with nicer way.

## Deploy Your First Edge App

Make sure to click the button, `SOURCE ENV` before you get started to source the correct environment.

<details>
<summary>log</summary>

<pre>
root@d1a6654df463:/home/workspace# source /opt/intel/openvino/bin/setupvars.sh -pyver 3.5
python_version = 3.5
[setupvars.sh] OpenVINO environment initialized
(venv) root@d1a6654df463:/home/workspace#
</pre>
</details>

Here you will just need to call your functions to handle the input and output of the model within the app.

We don't touch the code about the Model Optimizer now.

You will work out of the `handle_models.py` file, as well as adding functions calls within the edge app in `app.py`.

### TODOs

You will implement the handling of the outputs of our three models on `handle_models.py`.

Notice that there are two TODOs for each handle function to determine the each output on the first three functions.

The 4th function, named `handle_output` is the helper function returns one of the above three functions to handle an output, based on the `model_type`.

The last one is `preprocessing` function you wrote on the previous exercise.

```
import cv2
import numpy as np


def handle_pose(output, input_shape):
    '''
    Handles the output of the Pose Estimation model.
    Returns ONLY the keypoint heatmaps, and not the Part Affinity Fields.
    '''
    # TODO 1: Extract only the second blob
    # TODO 2: Resize the heatmap back to the size of the input

    return None


def handle_text(output, input_shape):
    '''
    Handles the output of the Text Detection model.
    Returns ONLY the text/no text classification of each pixel,
        and not the linkage between pixels and their neighbors.
    '''
    # TODO 1: Extract only the first blob output (text/no text classification)
    # TODO 2: Resize this output back to the size of the input

    return None


def handle_car(output, input_shape):
    '''
    Handles the output of the Car Metadata model.
    Returns two integers: the argmax of each softmax output.
    The first is for color, and the second for type.
    '''
    # TODO 1: Get the argmax of the "color" output
    # TODO 2: Get the argmax of the "type" output

    return None


def handle_output(model_type):
    '''
    Returns the related function to handle an output,
        based on the model_type being used.
    '''
    if model_type == "POSE":
        return handle_pose
    elif model_type == "TEXT":
        return handle_text
    elif model_type == "CAR_META":
        return handle_car
    else:
        return None


'''
The below function is carried over from the previous exercise.
You just need to call it appropriately in `app.py` to preprocess
the input image.
'''
def preprocessing(input_image, height, width):
    '''
    Given an input image, height and width:
    - Resize to width and height
    - Transpose the final "channel" dimension to be first
    - Reshape the image to add a "batch" of 1 at the start
    '''
    image = np.copy(input_image)
    image = cv2.resize(image, (width, height))
    image = image.transpose((2,0,1))
    image = image.reshape(1, 3, height, width)

    return image
```

Here is two TODOs on the `handle_pose` function. For `TODO 1: Extract only the second blob`, refer the output information on [outputs section](https://docs.openvinotoolkit.org/latest/_models_intel_human_pose_estimation_0001_description_human_pose_estimation_0001.html#outputs) of the `human_pose_estimation_0001` page.

```
def handle_pose(output, input_shape):
    '''
    Handles the output of the Pose Estimation model.
    Returns ONLY the keypoint heatmaps, and not the Part Affinity Fields.
    '''
    # TODO 1: Extract only the second blob
    # TODO 2: Resize the heatmap back to the size of the input

    return None
```

We want to check what is exactly the output type to extract the second blob which contains keypoint heatmaps.

For checking the data type, implement `app.py` first, because the `handle_pose` function calling from `app.py` is much more easier for debugging.

### app.py

Let's have a closer look at the the first part of the `app.py` to understand the basic structure of the code and how do we implement it.

```
import argparse
import cv2
import numpy as np

from handle_models import handle_output, preprocessing
from inference import Network


CAR_COLORS = ["white", "gray", "yellow", "red", "green", "blue", "black"]
CAR_TYPES = ["car", "bus", "truck", "van"]
```

> `import argparse` - import the argparse module to write user-friendly command-line interfaces more easily.
>
> `import cv2` - import statement to use the OpenCV package in code  
> [OpenCV Tutorial: A Guide to Learn OpenCV](https://www.pyimagesearch.com/2018/07/19/opencv-tutorial-a-guide-to-learn-opencv/)
>
> `import numpy as np` - this imports the numpy package in code and as np statement make it accessible using np in your code
>
> `from handle_models import handle_output, preprocessing` - this imports handle_output and preprocessing functions from handle_models.py file.
>
> `from inference import Network` - this imports Network class from inference.py file.
>
> `CAR_COLORS = ["white", "gray", "yellow", "red", "green", "blue", "black"]`  
> `CAR_TYPES = ["car", "bus", "truck", "van"]` - defines these arrays for labeling car colors and car types of output on vehicle-attributes-recognition-barrier-0039 pre-trained model

There are two parts having a defined starting point for the execution of a program called main function.

```
def main():
    args = get_args()
    perform_inference(args)


if __name__ == "__main__":
    main()
```

> `def main():` - this defined the function called main() and inside this there are args = get_args() and perform_inference(args)
>
> `args = get_args()` - this statement calls get_args() function and assign return value to args variable ()
>
> `perform_inference(args)` - This code executes perform_inference function with the args parameter which is assigned on args = get_args()
>
> `if __name__ == "__main__":` - this is the best practice for Python main functions. if statement checks the special \__name__ variable and compare it to the string "\__main__". If it is True, the Python interpreter executes main() function.
>
> The special \__name__ variable is defined by Python when it executed.  
> When you execute the Python file as a script using the command line like `python app.py`, \__name__ variable will have the string value "\__main__".  
> As the second way, the Python interpreter will execute your code: imports using like `import cv2`, \__name__ variable will have the string value "cv2" in this case.  
> Reference: [Defining Main Functions in Python](https://realpython.com/python-main-function/)

Here `get_args()` is called from the starting point, main function. The function retrieves the arguments when the code executed.

The arguments come from when the `app.py` is executed on the command line.

For example, here is `-i`, `-t`, `-m` and `-c` arguments which is handled by `get_args` function and passed to the further functions.

```
# python app.py -i "images/blue-car.jpg" -t "CAR_META" -m "/home/workspace/models/vehicle-attributes-recognition-barrier-0039.xml" -c "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"
```

> `-i "images/blue-car.jpg"` - The location of the input image
>
> `-t "CAR_META"` - The model type, which should be one of "POSE", "TEXT", or "CAR_META"
>
> `-m "/home/workspace/models/vehicle-attributes-recognition-barrier-0039.xml"` - The location of the model .xml file
>
> `-c "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"` - A CPU extension file (this is optional). You can ignore now.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">More Detail for get_args Function</summary>

This is the first step in using the argparse is creating an ArgumentParser object.

```
def get_args():
    '''
    Gets the arguments from the command line.
    '''

    parser = argparse.ArgumentParser("Basic Edge App with Inference Engine")

# omitted ...
```

> `parser = argparse.ArgumentParser("Basic Edge App with Inference Engine")` - The `argparse.ArgumentParser` creates the object of ArgumentParser class on Lib/argparse.py which you imported. The ArgumentParser object will hold all the information necessary to parse the command line into Python data types.  
> "Basic Edge App with Inference Engine" string value is passed in for description to display before the argument help. It shows like this:  
> Reference: [Create object from class in separate file](https://stackoverflow.com/a/23238374)

log
```
(venv) root@044969e5b664:/home/workspace# python app.py -h
usage: Basic Edge App with Inference Engine [-h] -i I -m M -t T [-c C] [-d D]

# omitted ...
(venv) root@044969e5b664:/home/workspace#
```

For preparation of the descriptions for the each arguments, it creates string vlues wich is used later.

```
# -- Create the descriptions for the commands

c_desc = "CPU extension file location, if applicable"
d_desc = "Device, if not CPU (GPU, FPGA, MYRIAD)"
i_desc = "The location of the input image"
m_desc = "The location of the model XML file"
t_desc = "The type of model: POSE, TEXT or CAR_META"
```

The next few lines are configuring the argument groups for showing the help messages when running with `-h` or `--help` argument.

```
# -- Add required and optional groups
parser._action_groups.pop()
required = parser.add_argument_group('required arguments')
optional = parser.add_argument_group('optional arguments')
```

> `parser._action_groups.pop()` -  By default, ArgumentParser groups command-line arguments into “positional arguments” and “optional arguments” which is stored in `_action_groups` internally when displaying help messages. To show the argument groups more sophisticated way, it can be removed last argument group from the list, “optional arguments”. Without popping (removing) the “optional arguments”, optional argument group shows up first by default.  
> Reference: [Argparse: Required arguments listed under “optional arguments”?](https://stackoverflow.com/questions/24180527/argparse-required-arguments-listed-under-optional-arguments)
>
> `required = parser.add_argument_group('required arguments')` - New argument group called 'required arguments' is created for a better conceptual grouping of arguments than this default one. the returned argument group object assignes the variable, required.
>
> `optional = parser.add_argument_group('optional arguments')` - The same concept is applied here. It re-creates the 'optional arguments' group because the the default 'optional arguments' group is deleted and to shows the optional group under the 'required arguments' group

Check the data type of the `parser._action_groups` and comment out the `parser._action_groups.pop()` line to understand how it works in `app.py` code.

```
# -- Add required and optional groups
print('Type: {}'.format(type(parser._action_groups)))
# parser._action_groups.pop()
required = parser.add_argument_group('required arguments')
optional = parser.add_argument_group('optional arguments')
```

Then run on the command line to show help messages.

```
python app.py -h
```

> `-h` - which is a default option to show help messages.

As you can see that `_action_groups` is list class accroding to `Type: <class 'list'>` and `optional arguments:` part is shown here because it is not deleted using pop function.

log

```
(venv) root@125f05bfb32a:/home/workspace# python app.py -h
Type: <class 'list'>
usage: Basic Edge App with Inference Engine [-h] -i I -m M -t T [-c C] [-d D]

optional arguments:
  -h, --help  show this help message and exit

required arguments:
  -i I        The location of the input image
  -m M        The location of the model XML file
  -t T        The type of model: POSE, TEXT or CAR_META

optional arguments:
  -c C        CPU extension file location, if applicable
  -d D        Device, if not CPU (GPU, FPGA, MYRIAD)
```

Those arguments such as "-i" and "-m" is defined with some parameters and assigned to the each required and optional argument groups created at the above part.

```
# -- Create the arguments
required.add_argument("-i", help=i_desc, required=True)
required.add_argument("-m", help=m_desc, required=True)
required.add_argument("-t", help=t_desc, required=True)
optional.add_argument("-c", help=c_desc, default=None)
optional.add_argument("-d", help=d_desc, default="CPU")
args = parser.parse_args()

return args
```

> `required.add_argument("-i", help=i_desc, required=True)` - For the "-i" argument, adding `i_desc` variable as a brief description of what the argument does in `help=i_desc`. Also it is flaged as a required argument when you use `app.py`.  
> `required.add_argument("-m", help=m_desc, required=True)`  
> `required.add_argument("-t", help=t_desc, required=True)` - Those "-m" and "-t" is also added the required argument group.
>
> `optional.add_argument("-c", help=c_desc, default=None)` - Almost same one as you did above, the "-c" argument is added in optional argument group you created above and the value parameter produced as None here if the argument is absent from the command line which means optional argument, in other words.
>
> `optional.add_argument("-d", help=d_desc, default="CPU")` - If "-d" is not passed in on the command line, the value, "CPU" is filled in by default.
>
> `args = parser.parse_args()` - It parses arguments (like "-h" on `python app.py -h`) through the parse_args() method. This will inspect the command line, convert each argument to the appropriate type and then invoke the appropriate action.  
> Reference: [Parsing a Command Line](https://pymotw.com/2/argparse/#parsing-a-command-line)

</details>

{::options parse_block_html="false" /}
<br>

After executing `get_args()` function, it executes `perform_inference(args)` for preprocessing and handling the output image created by the pre-trained model.

```
def perform_inference(args):
    '''
    Performs inference on an input image, given a model.
    '''
    # Create a Network for using the Inference Engine
    inference_network = Network()
    # Load the model in the network, and obtain its input shape
    n, c, h, w = inference_network.load_model(args.m, args.d, args.c)

    # Read the input image
    image = cv2.imread(args.i)

    ### TODO: Preprocess the input image

    # Perform synchronous inference on the image
    inference_network.sync_inference(preprocessed_image)

    # Obtain the output of the inference request
    output = inference_network.extract_output()

    ### TODO: Handle the output of the network, based on args.t
    ### Note: This will require using `handle_output` to get the correct
    ###       function, and then feeding the output to that function.

    # Create an output image based on network
    output_image = create_output_image(args.t, image, processed_output)

    # Save down the resulting image
    cv2.imwrite("outputs/{}-output.png".format(args.t), output_image)

```

> `inference_network = Network()` - `Network()` function comes from inference.py file which imported the first section of codes. The inference.py contains code for working with the Inference Engine. You'll learn how to implement this code and more in the related lesson on the topic.
>
> `n, c, h, w = inference_network.load_model(args.m, args.d, args.c)` - (explanis later lessons) it feeds in args.m (The location of the model .xml file), args.d (Device, default value is CPU), args.c (CPU extension file location).  
> It returns the model's input shape information, n (batch size), c (number of color channels), h (image height) and w (image width)
>
> `image = cv2.imread(args.i)` - the `imread` method loads an image from the specified file, args.i (the location of the input image)
>
> `### TODO: Preprocess the input image` - TODO to preprocess the input image (Tacles later)
>
> `inference_network.sync_inference(preprocessed_image)` - (explanis later lessons) it feeds in the above preprocessed_image.  
>
> `output = inference_network.extract_output()` - (explanis later lessons) returning object is the output of the inference request
>
> `### TODO: Handle the output of the network, based on args.t` - Here is the second TODO. (Tacles later)
>
> `output_image = create_output_image(args.t, image, processed_output)` - create_output_image method creates an output image showing the result of inference using args.t (the model type), image (input image), and processed_output (processed output).

For the first TODO, the output of `preprocessing` function assignes the variable `preprocessed_image`.

```
  ### TODO: Preprocess the input image
  preprocessed_image = preprocessing(image, h, w)
```

> `preprocessed_image = preprocessing(image, h, w)` - The `preprocessed_image` variable name comes from the next code  `inference_network.sync_inference(preprocessed_image)`. The `preprocessing` function is defined `handle_models.py`.  
> The` preprocessing` function takes `image` as a input image (from the privious line `image = cv2.imread(args.i)`) with image hight and width, `h` and `w` (`n, c, h, w = inference_network.load_model(args.m, args.d, args.c)` function actually returned).

The next TODO is about processing the output of the pre-trained model. Accroding to the Note suggestion, it uses handle_output function which returns the correct output handling function by feeding in the model type, `args.t`. The second line sends the output of inference and image shape to `output_function`.

```
  ### TODO: Handle the output of the network, based on args.t
  ### Note: This will require using `handle_output` to get the correct
  ###       function, and then feeding the output to that function.
  output_function = handle_output(args.t)
  processed_output = output_function(output, image.shape)
```

> `output_function = handle_output(args.t)` - `handle_output(args.t)` function with `args.t` (the model type) and assignes the return to `output_function`. handle_output function will be implemented later.
>
> `processed_output = output_function(output, image.shape)` - Using `output_function` function with the raw output and shape properties, `image.shape`, it process the output. Your processed_output image will be used on the next line `output_image = create_output_image(args.t, image, processed_output)`.

Now you implemented the `app.py`, it is time to back `handle_models.py` TODOs.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Try and Except from Solution</summary>

For handling exceptions, you can use `try` and `except` statements.

The main part in this exercise is creating `processed_output` value using `handle_output` and each model output handle functions on `handle_models.py`.

If you mistake anywhere in the `handle_models.py`, the next line, `output_image = create_output_image(args.t, image, processed_output)` will fail. So the line is the best place to handle exceptions and return feedback to you.

```
    ### TODO: Handle the output of the network, based on args.t
    ### Note: This will require using `handle_output` to get the correct
    ###       function, and then feeding the output to that function.
    output_function = handle_output(args.t)
    processed_output = output_function(output, image.shape)
```

Add try and except clause

```
    # Create an output image based on network
    try:
        output_image = create_output_image(args.t, image, processed_output)
        print('Success!')
    except:
        output_image = image
        print('Error!')
```

> `try:` -  this block is executed first. If no exception occurs, the except clause is skipped and execution of the try statement is finished. (print "Error!")
>
> `except:` - If an exception occurs during execution of the try clause, the rest of the clause is skipped. Then this except clause is executed. (print "Success!")
> Reference: [8. Errors and Exceptions](https://docs.python.org/3/tutorial/errors.html)

</details>

{::options parse_block_html="false" /}

### handle_models.py

#### handle_pose function

To check the data type of output, add print function on `handle_pose` function.

```
def handle_pose(output, input_shape):
    '''
    Handles the output of the Pose Estimation model.
    Returns ONLY the keypoint heatmaps, and not the Part Affinity Fields.
    '''
    # TODO 1: Extract only the second blob
    print(type(output))
    exit(1)
    # TODO 2: Resize the heatmap back to the size of the input

    return None
```

> `print(type(output))` - prints what type that outputs on the console
>
> `exit(1)` - This causes the program to exit with some issue / error / problem and that is why the program is exiting (here, for debugging purpose)  
> Reference: [Difference between exit(0) and exit(1) in Python](https://stackoverflow.com/questions/9426045/difference-between-exit0-and-exit1-in-python)

Run

```
# python app.py -i "images/sitting-on-car.jpg" -t "POSE" -m "/home/workspace/models/human-pose-estimation-0001.xml" -c "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"
```

<details>
<summary>log</summary>

<pre>
python app.py -i "images/sitting-on-car.jpg" -t "POSE" -m "/home/workspace/models/human-pose-estimation-0001.xml" -c "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"
<class 'dict'>
(venv) root@d35e24cf5494:/home/workspace#
</pre>
</details>

The output is dictionary which has `Mconv7_stage2_L1` and `Mconv7_stage2_L2` keys (`print(output.keys())` prints only keys on the dictionary)

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Check keys on dictionary</summary>

code
```
def handle_pose(output, input_shape):
    '''
    Handles the output of the Pose Estimation model.
    Returns ONLY the keypoint heatmaps, and not the Part Affinity Fields.
    '''
    # TODO 1: Extract only the second blob
    print(output.keys())
    exit(1)
    # TODO 2: Resize the heatmap back to the size of the input

    return None
```

Run
```
# python app.py -i "images/sitting-on-car.jpg" -t "POSE" -m "/home/workspace/models/human-pose-estimation-0001.xml" -c "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"
```

log
```
(venv) root@332ffbba3402:/home/workspace# python app.py -i "images/sitting-on-car.jpg" -t "POSE" -m "/home/workspace/models/human-pose-estimation-0001.xml" -c "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"
dict_keys(['Mconv7_stage2_L2', 'Mconv7_stage2_L1'])
(venv) root@332ffbba3402:/home/workspace#
```

</details>

{::options parse_block_html="false" /}

To Extract only the second blob, `Mconv7_stage2_L2`, add

```
def handle_pose(output, input_shape):
    '''
    Handles the output of the Pose Estimation model.
    Returns ONLY the keypoint heatmaps, and not the Part Affinity Fields.
    '''
    # TODO 1: Extract only the second blob
    heatmaps = output['Mconv7_stage2_L2']
    # TODO 2: Resize the heatmap back to the size of the input

    return None
```

To start off TODO 2, print heatmaps' shape to check what contains in it.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">code and log</summary>

code

```
def handle_pose(output, input_shape):
    '''
    Handles the output of the Pose Estimation model.
    Returns ONLY the keypoint heatmaps, and not the Part Affinity Fields.
    '''
    # TODO 1: Extract only the second blob
    heatmaps = output['Mconv7_stage2_L2']
    # TODO 2: Resize the heatmap back to the size of the input
    print(heatmaps.shape)
    exit(1)

    return None
```

log

```
(venv) root@4685af7bd898:/home/workspace# python app.py -i "images/sitting-on-car.jpg" -t "POSE" -m "/home/workspace/models/human-pose-estimation-0001.xml" -c "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"
(1, 19, 32, 57)
```
</details>

{::options parse_block_html="false" /}

The heatmaps ndarray has 4 dimensions, (1, 19, 32, 57) which represents keypoint heatmaps.

You can assume that there are 19 keypoint heatmaps for human pose detection. On the second dimension, 32 and 57 is image height and width, and 1 is batch size that means they return 1 output at a time.

It has a matrix of matrices. 1 is the number of rows of matrices, 19 is the number of columns of matrices, and (32, 57) is the number of rows and columns in the matrix at array[1][19].

{% include helpers/image.html name="keypoint_heatmaps_ndarray.png" %}

Resize it with input image height and width. `input_shape` is from `image.shape` and `image = cv2.imread(args.i)` on app.py. Input image is read as a 3D ndarray of row (height) x column (width) x depth (color).

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Check input_shape</summary>

code

```
def handle_pose(output, input_shape):
    '''
    Handles the output of the Pose Estimation model.
    Returns ONLY the keypoint heatmaps, and not the Part Affinity Fields.
    '''
    # TODO 1: Extract only the second blob output (keypoint heatmaps)
    heatmaps = output['Mconv7_stage2_L2']
    # TODO 2: Resize the heatmap back to the size of the input
    print(input_shape)
    exit(1)

    return None
```

log

```
(venv) root@e58ff8e15d0f:/home/workspace# python app.py -i "images/sitting-on-car.jpg" -t "POSE" -m "/home/workspace/models/human-pose-estimation-0001.xml" -c "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"
(750, 1000, 3)
(venv) root@e58ff8e15d0f:/home/workspace#
```
> (750, 1000, 3) - this is a input shape, 750 pixels height, 1000 pixels width, and 3 represents color picture.

</details>

{::options parse_block_html="false" /}
<br>

And the return value `processed_output` will be used on `get_mask(processed_output)` and `create_output_image(model_type, image, output)`. You can find that `mask = np.dstack((empty, processed_output, empty))` means 3 dimensional ndarray is needed because `dstack` function makes most sense for arrays with up to 3 dimensions. `output = output[:-1]` and `# Remove final part of output not used for heatmaps` can be infered that the first dimension will be the heatmaps, height and width in order.

> `output = output[:-1]` - extract all elements of the sequence but the last.
> Reference: [What does [:-1] mean/do in python?](https://stackoverflow.com/questions/15535205/what-does-1-mean-do-in-python)

{::options parse_block_html="true" /}

<details>
<summary markdown="span">create_output_image And get_mask</summary>

get_mask(processed_output)

```
def get_mask(processed_output):
    '''
    Given an input image size and processed output for a semantic mask,
    returns a masks able to be combined with the original image.
    '''
    # Create an empty array for other color channels of mask
    empty = np.zeros(processed_output.shape)
    # Stack to make a Green mask where text detected
    mask = np.dstack((empty, processed_output, empty))

    return mask
```

create_output_image(model_type, image, output)

```
def create_output_image(model_type, image, output):
    '''
    Using the model type, input image, and processed output,
    creates an output image showing the result of inference.
    '''
    if model_type == "POSE":
        # Remove final part of output not used for heatmaps
        output = output[:-1]
        # Get only pose detections above 0.5 confidence, set to 255
        for c in range(len(output)):
            output[c] = np.where(output[c]>0.5, 255, 0)
        # Sum along the "class" axis
        output = np.sum(output, axis=0)
        # Get semantic mask
        pose_mask = get_mask(output)
        # Combine with original image
        image = image + pose_mask
        return image
# omitted ...
```

Here [Futher Reading about Human Pose Estimation](http://docs.openvinotoolkit.org/latest/_demos_human_pose_estimation_demo_README.html) explains the output for pose may contains up to 18 keypoints. So, shouldn't it be 18 instead of 19? That is the reason why it removes final part of output not used for heatmaps.

```
# Remove final part of output not used for heatmaps
output = output[:-1]
```

{::options parse_block_html="false" /}

The final part of output is about background.

{% include helpers/image.html name="POSE-output-background.png" %}

{::options parse_block_html="true" /}

code

```
# Change output[:-1] to output[-1:] to extract only the last element
output = output[-1:]
```

</details>

{::options parse_block_html="false" /}
<br>

Create new ndarray for output using input shape and keypoint heatmaps.

```
  # TODO 2: Resize the heatmap back to the size of the input
  # Create an array of zeros
  processed_output = np.zeros([heatmaps.shape[1], input_shape[0], input_shape[1]])
```

Resize each ndarray using for loop. `cv2.resize` function only takes dimensions of 1 or 3 for the channels which is usually color or grayscale image. In our case, there is 19 of these layers.

```
  # TODO 2: Resize the heatmap back to the size of the input
  # Create an array of zeros
  processed_output = np.zeros([heatmaps.shape[1], input_shape[0], input_shape[1]])
  # Iterate through and re-size each heatmap
  for h in range(len(heatmaps[0])):
     processed_output[h] = cv2.resize(heatmaps[0][h], input_shape[0:2][::-1])

  return processed_output
```

> `out_heatmap = np.zeros([heatmaps.shape[1], input_shape[0], input_shape[1]])` - numpy function `zeros` returns a new array of given shape and type, filled with zeros. The first parameter, `[heatmaps.shape[1], input_shape[0], input_shape[1]]` list explains shape of the new 3 dimensional ndarray.
>
> `for h in range(len(heatmaps[0])):` - This `for` loop is used for iterating over a sequence of numbers (0~18).  The `range()` function returns a sequence of numbers, starting from 0 by default, and increments by 1 (by default), and ends at a specified number (In this case, `len(heatmaps[0])`)
>
> `processed_output[h] = cv2.resize(heatmaps[0][h], input_shape[0:2][::-1])` - `cv2.resize` resize each keypoint heatmap (`heatmaps[0][h]`) to specific width and height (`input_shape[0:2][::-1]`). the `input_shape[0:2][::-1]` line is taking the original image shape of HxWxC, taking just the first two (HxW), and reversing them to be WxH.
> `[::-1]` reverses `input_shape[0:2]` (750, 1000). It starts from the end, towards the first, taking each element.
>
> `return processed_output` - It returns `processed_output` which is trimed and resized.

Now, it's time to run `app.py` for Human Pose Estimation.

```
# python app.py -i "images/sitting-on-car.jpg" -t "POSE" -m "/home/workspace/models/human-pose-estimation-0001.xml" -c "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"
```

<details>
<summary>log</summary>

<pre>
(venv) root@2416e0f303d3:/home/workspace# python app.py -i "images/sitting-on-car.jpg" -t "POSE" -m "/home/workspace/models/human-pose-estimation-0001.xml" -c "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"
(venv) root@2416e0f303d3:/home/workspace#
</pre>
</details>

It will not show anything but the image should already be available in the outputs folder. You can find a folder icon at the top left corner below the taskbar, and browse the `POSE-output.png` file on the output directory. You can double click or download by right click.

{% include helpers/image.html name="Screen Shot 2020-01-07 at 19.29.41.png" %}

The output of Human Pose Estimation will be:

{% include helpers/image.html name="POSE-output.png" %}

#### handle_text

Here is two TODOs on the `handle_text` function. For `TODO 1: Extract only the first blob output`, refer the output information on [outputs section](https://docs.openvinotoolkit.org/latest/_models_intel_text_detection_0004_description_text_detection_0004.html#outputs) of the `text-detection-0004` page.

It is a similar approch, first, check type of output.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">check Type of output</summary>

code

```
def handle_text(output, input_shape):
    '''
    Handles the output of the Text Detection model.
    Returns ONLY the text/no text classification of each pixel,
        and not the linkage between pixels and their neighbors.
    '''
    # TODO 1: Extract only the first blob output (text/no text classification)
    print(type(output))
    exit(1)
    # TODO 2: Resize this output back to the size of the input

    return None
```

Run

```
# python app.py -i "images/sign.jpg" -t "TEXT" -m "/home/workspace/models/text-detection-0004.xml" -c "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"
```

log

```
(venv) root@dfaa228ce41f:/home/workspace# python app.py -i "images/sign.jpg" -t "TEXT" -m "/home/workspace/models/text-detection-0004.xml" -c "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"
<class 'dict'>
(venv) root@dfaa228ce41f:/home/workspace#
```

</details>

{::options parse_block_html="false" /}

The class of output is dictionary. Add code for extracting it using the first key, `'model/segm_logits/add'` to variable `first_blob`.

```
# TODO 1: Extract only the first blob output (text/no text classification)
first_blob = output['model/segm_logits/add']
```

For TODO 2, check the `first_blob` shape to determine resizing.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Check the first_blob shape</summary>

```
def handle_text(output, input_shape):
    '''
    Handles the output of the Text Detection model.
    Returns ONLY the text/no text classification of each pixel,
        and not the linkage between pixels and their neighbors.
    '''
    # TODO 1: Extract only the first blob output (text/no text classification)
    first_blob = output['model/segm_logits/add']
    # TODO 2: Resize this output back to the size of the input
    print(first_blob.shape)
    exit(1)

    return None
```

Run
```
# python app.py -i "images/sign.jpg" -t "TEXT" -m "/home/workspace/models/text-detection-0004.xml" -c "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"
```

log
```
(venv) root@de1e9a55d8cd:/home/workspace# python app.py -i "images/sign.jpg" -t "TEXT" -m "/home/workspace/models/text-detection-0004.xml" -c "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"
(1, 2, 192, 320)
```

> `(1, 2, 192, 320)` - It supposes 1 (batch size), 2 (text/no-text classification), 192 (output width), 320 (output height)

</details>

{::options parse_block_html="false" /}

For both text/no-text classification, it resizes from (192, 320) output size to the input size.

In the `app.py`, again they use the first dimension of output.

```
# omitted ...
    # Get only text detections above 0.5 confidence, set to 255
    output = np.where(output[1]>0.5, 255, 0)
# omitted ...
```

TODO 2's code is the almost same with human-pose-estimation-0001.

```
    # TODO 2: Resize this output back to the size of the input
    # Create an array of zeros
    processed_output = np.zeros([first_blob.shape[1], input_shape[0], input_shape[1]])
    # Iterate through and re-size each heatmap
    for h in range(len(first_blob[0])):
        processed_output[h] = cv2.resize(first_blob[0][h], input_shape[0:2][::-1])

    return processed_output
```

Now you can run `app.py` for `text-detection-0004`.

```
# python app.py -i "images/sign.jpg" -t "TEXT" -m "/home/workspace/models/text-detection-0004.xml" -c "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"
```

> `-i "images/sign.jpg"` - test image which already provided
>
> `-t "TEXT"` - model type for test detection
>
> `-m "/home/workspace/models/text-detection-0004.xml"` - model xml file for text-detection-0004
>
> `-c "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"` - A CPU extension file (optional). You can ignore now.

Check output image on `outputs` directory.

{% include helpers/image.html name="Screen Shot 2020-01-09 at 12.20.37.png" %}

This is full output image.

{% include helpers/image.html name="TEXT-output.png" %}

#### handle_car

Here is two TODOs on the `handle_car` function. Refer the output information on [outputs section](https://docs.openvinotoolkit.org/latest/_models_intel_vehicle_attributes_recognition_barrier_0039_description_vehicle_attributes_recognition_barrier_0039.html#outputs) of the `vehicle-attributes-recognition-barrier-0039` page.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Check class type of output.</summary>

code
```
def handle_car(output, input_shape):
    '''
    Handles the output of the Car Metadata model.
    Returns two integers: the argmax of each softmax output.
    The first is for color, and the second for type.
    '''
    # TODO 1: Get the argmax of the "color" output
    print(type(output))
    exit(1)
    # TODO 2: Get the argmax of the "type" output

    return None
```

Run
```
# python app.py -i "images/blue-car.jpg" -t "CAR_META" -m "/home/workspace/models/vehicle-attributes-recognition-barrier-0039.xml" -c "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"
```

log
```
(venv) root@de1e9a55d8cd:/home/workspace# python app.py -i "images/blue-car.jpg" -t "CAR_META" -m "/home/workspace/models/vehicle-attributes-recognition-barrier-0039.xml" -c "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"
<class 'dict'>
(venv) root@de1e9a55d8cd:/home/workspace#
```

You can check keys of this dictionary with `print(output.keys())` and each shape using `print(output['color'])` and `print(output['type'])`. That should match what we saw on the [documentation](https://docs.openvinotoolkit.org/latest/_models_intel_vehicle_attributes_recognition_barrier_0039_description_vehicle_attributes_recognition_barrier_0039.html#outputs).

```
dict_keys(['color', 'type'])
(1, 7, 1, 1)
(1, 4, 1, 1)
```

</details>

{::options parse_block_html="false" /}

To make well-processed output, check how the processed output is used on the application.

In the `create_output_image` function, it uses only the first dimension.

```
# omitted ...
    # Get the color and car type from their lists
        color = CAR_COLORS[output[0]]
        car_type = CAR_TYPES[output[1]]
# omitted ...
```

So it is reasonable to get rid of unnecessary dimensions. The argmax suggests to use argmax function to get the indices of the maximum values.

```
def handle_car(output, input_shape):
    '''
    Handles the output of the Car Metadata model.
    Returns two integers: the argmax of each softmax output.
    The first is for color, and the second for type.
    '''
    # TODO 1: Get the argmax of the "color" output
    # Get rid of unnecessary dimensions
    output_color = output['color'].flatten()

    argmax_color = np.argmax(output_color)

    # TODO 2: Get the argmax of the "type" output
    # Get rid of unnecessary dimensions
    output_type = output['type'].flatten()

    argmax_type = np.argmax(output_type)

    return argmax_color, argmax_type
```

> `output_color = output['color'].flatten()` -  flatten function flattens `output['color']` to one dimension and assignes it to `output_color` variable.
>
> `argmax_color = np.argmax(output_color)` - `argmax` function returns the index where the highest probability on `output_color` array.
>
> `output_type = output['type'].flatten()` - almost same above but for car type.
>
> `argmax_type = np.argmax(output_type)` - same but output_type array.

Now it is time to run

```
# python app.py -i "images/blue-car.jpg" -t "CAR_META" -m "/home/workspace/models/vehicle-attributes-recognition-barrier-0039.xml" -c "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"
```

> `-i "images/blue-car.jpg"` - example image for testing
>
> `-t "CAR_META"` - model type for vehicle-attributes-recognition-barrier-0039
>
> `-m "/home/workspace/models/vehicle-attributes-recognition-barrier-0039.xml"` - pre-trained model data
>
> `-c "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"` - you can ignore for now.

<details>
<summary>log</summary>

<pre>
(venv) root@8ae83e78eaaf:/home/workspace# python app.py -i "images/blue-car.jpg" -t "CAR_META" -m "/home/workspace/models/vehicle-attributes-recognition-barrier-0039.xml" -c "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"
(venv) root@8ae83e78eaaf:/home/workspace#
</pre>
</details>

On `outputs` folder on your workspace, there should be `CAR_META-output.png`.

{% include helpers/image.html name="CAR_META-output.png" %}

# Lesson 3: The Model Optimizer

You will do the following things:

- Converting from models in those frameworks to Intermediate Representations
- And a bit on Custom Layers

## Exercise: Convert a TensorFlow Model

Make sure to click the `SOURCE ENV` button before you get started to source the correct environment.

<details>
<summary>log</summary>

<pre>
root@4a89951ac85e:/home/workspace# source /opt/intel/openvino/bin/setupvars.sh -pyver 3.5
python_version = 3.5
[setupvars.sh] OpenVINO environment initialized
(venv) root@4a89951ac85e:/home/workspace#
</pre>
</details>

### SSD MobileNet V2 COCO model

You'll convert a TensorFlow Model from the Object Detection Model Zoo into an Intermediate Representation using the Model Optimizer.

First, you need to download the SSD MobileNet V2 COCO model which is a TensorFlow Model.

```
# wget http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_coco_2018_03_29.tar.gz
```

> `wget http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_coco_2018_03_29.tar.gz` - wget is one of the most common a Linux and UNIX command for downloading files from the Internet. In this case, you will download the `ssd_mobilenet_v2_coco_2018_03_29.tar.gz` which is a tar file, a collection of files wrapped up in one single file for easy storage from the url, http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_coco_2018_03_29.tar.gz.

<details>
<summary>log</summary>

<pre>
(venv) root@4a89951ac85e:/home/workspace# wget http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_coco_2018_03_29.tar.gz
--2020-01-10 12:33:35--  http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_coco_2018_03_29.tar.gz
Resolving download.tensorflow.org (download.tensorflow.org)... 173.194.193.128, 2607:f8b0:4001:c0f::80
Connecting to download.tensorflow.org (download.tensorflow.org)|173.194.193.128|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 187925923 (179M) [application/x-tar]
Saving to: ‘ssd_mobilenet_v2_coco_2018_03_29.tar.gz’

ssd_mobilenet_v2_c 100%[===============>] 179.22M   167MB/s    in 1.1s    

2020-01-10 12:33:37 (167 MB/s) - ‘ssd_mobilenet_v2_coco_2018_03_29.tar.gz’ saved [187925923/187925923]

(venv) root@4a89951ac85e:/home/workspace#
</pre>
</details>

You can check the `ssd_mobilenet_v2_coco_2018_03_29.tar.gz` file under `/home/workspace` using `ls` command.

```
# ls -l
```

> `ls -l` - `ls` command to lists files and directories within the current directory. With the `-l` option, `ls` will list out files and directories in long list format.

<details>
<summary>log</summary>

<pre>
(venv) root@4a89951ac85e:/home/workspace# ls -l
total 183788
-rw-r--r-- 1 root root     68036 Jan 10 11:32 Guide.ipynb
-rw-r--r-- 1 root root      2135 Dec 12 23:48 README.md
drwxr-xr-x 2 root root      4096 Dec 12 23:48 solution
-rw-r--r-- 1 root root 187925923 Apr  2  2018 ssd_mobilenet_v2_coco_2018_03_29.tar.gz
(venv) root@4a89951ac85e:/home/workspace#
</pre>
</details>

Now you can extract the compressed file.

```
# tar -xvf ssd_mobilenet_v2_coco_2018_03_29.tar.gz
```

> `tar -xvf ssd_mobilenet_v2_coco_2018_03_29.tar.gz` - `tar` command for handling `**.tar.gz` file.  
> `x`: Extract a tar file.  
> `v`: Verbose output or show progress while extracting files.  
> `f`: Specify an archive or a tar filename. (ssd_mobilenet_v2_coco_2018_03_29.tar.gz)

<details>
<summary>log</summary>

<pre>
(venv) root@4a89951ac85e:/home/workspace# tar -xvf ssd_mobilenet_v2_coco_2018_03_29.tar.gz
ssd_mobilenet_v2_coco_2018_03_29/checkpoint
ssd_mobilenet_v2_coco_2018_03_29/model.ckpt.meta
ssd_mobilenet_v2_coco_2018_03_29/pipeline.config
ssd_mobilenet_v2_coco_2018_03_29/saved_model/saved_model.pb
ssd_mobilenet_v2_coco_2018_03_29/frozen_inference_graph.pb
ssd_mobilenet_v2_coco_2018_03_29/saved_model/
ssd_mobilenet_v2_coco_2018_03_29/saved_model/variables/
ssd_mobilenet_v2_coco_2018_03_29/model.ckpt.index
ssd_mobilenet_v2_coco_2018_03_29/
ssd_mobilenet_v2_coco_2018_03_29/model.ckpt.data-00000-of-00001
(venv) root@4a89951ac85e:/home/workspace# ls -l
total 183792
-rw-r--r-- 1 root   root      68036 Jan 10 11:32 Guide.ipynb
-rw-r--r-- 1 root   root       2135 Dec 12 23:48 README.md
drwxr-xr-x 2 root   root       4096 Dec 12 23:48 solution
drwxr-xr-x 3 345018 89939      4096 Mar 30  2018 ssd_mobilenet_v2_coco_2018_03_29
-rw-r--r-- 1 root   root  187925923 Apr  2  2018 ssd_mobilenet_v2_coco_2018_03_29.tar.gz
(venv) root@4a89951ac85e:/home/workspace#
</pre>
</details>

There is an extracted folder, `ssd_mobilenet_v2_coco_2018_03_29`.

```
# cd ssd_mobilenet_v2_coco_2018_03_29
```

> `cd` - command changes directories

<details>
<summary>log</summary>

<pre>
(venv) root@7fca492ef91a:/home/workspace# cd ssd_mobilenet_v2_coco_2018_03_29
(venv) root@7fca492ef91a:/home/workspace/ssd_mobilenet_v2_coco_2018_03_29# ls -l
total 137576
-rw-r--r-- 1 345018 89939       77 Mar 30  2018 checkpoint
-rw-r--r-- 1 345018 89939 69688296 Mar 30  2018 frozen_inference_graph.pb
-rw-r--r-- 1 345018 89939 67505156 Mar 30  2018 model.ckpt.data-00000-of-00001
-rw-r--r-- 1 345018 89939    15069 Mar 30  2018 model.ckpt.index
-rw-r--r-- 1 345018 89939  3496023 Mar 30  2018 model.ckpt.meta
-rw-r--r-- 1 345018 89939     4204 Mar 30  2018 pipeline.config
drwxr-xr-x 3 345018 89939     4096 Mar 30  2018 saved_model
(venv) root@7fca492ef91a:/home/workspace/ssd_mobilenet_v2_coco_2018_03_29#
</pre>
</details>

In TensorFlow, the `.pb` file contains the graph definition as well as the weights of the model. Thus, a pb file is all you need to be able to run a given trained model.

It's time to convert the TensorFlow model to produce an optimized Intermediate Representation (IR) of the model based on the trained network topology, weights, and biases values.

Use the `mo_tf.py` script to simply convert a model with the path to the input model `.pb` file. Also there is a little note about `--reverse_input_channels` in [Converting a TensorFlow* Model](https://docs.openvinotoolkit.org/latest/_docs_MO_DG_prepare_model_convert_model_Convert_Model_From_TensorFlow.html#Convert_From_TF).

> NOTE: The Model Optimizer does not revert input channels from RGB to BGR by default. Manually specify the command-line parameter to perform this reversion: --reverse_input_channels.

Check [Converting TensorFlow* Object Detection API Models](https://docs.openvinotoolkit.org/latest/_docs_MO_DG_prepare_model_convert_model_tf_specific_Convert_Object_Detection_API_Models.html#how_to_convert_a_model) because you downloaded an Object Detection API models from the Object Detection Model Zoo.

There are the three required parameters using `mo_tf.py` script for TensorFlow* Object Detection API Models.

* --input_model <path_to_frozen.pb>
* --tensorflow_use_custom_operations_config <path_to_subgraph_replacement_configuration_file.json>
* --tensorflow_object_detection_api_pipeline_config <path_to_pipeline.config>

Finally, we will convert this model with:

```
# python /opt/intel/openvino/deployment_tools/model_optimizer/mo.py \
  --input_model /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/frozen_inference_graph.pb \
  --tensorflow_object_detection_api_pipeline_config /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/pipeline.config \
  --reverse_input_channels \
  --tensorflow_use_custom_operations_config /opt/intel/openvino/deployment_tools/model_optimizer/extensions/front/tf/ssd_v2_support.json
```

> `python` - `python` is specified when invoking Python
>
> `/opt/intel/openvino/deployment_tools/model_optimizer/mo_tf.py` - the path of the model converter script
>
> `--input_model /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/frozen_inference_graph.pb` - option treats the input model file as a text protobuf format (in this case, frozen_inference_graph.pb within `/home/workspace/ssd_mobilenet_v2_coco_2018_03_29`)
>
> `--tensorflow_object_detection_api_pipeline_config /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/pipeline.config` - path to the pipeline configuration file used to generate model created with help of Object Detection API. (which is also located in `/home/workspace/ssd_mobilenet_v2_coco_2018_03_29`) (maybe igonre now)
>
> `--reverse_input_channels` - revert input channels from RGB to BGR due to the TensorFlow models being trained on RGB images, but the Inference Engine otherwise defaulting to BGR.
>
> `--tensorflow_use_custom_operations_config /opt/intel/openvino/deployment_tools/model_optimizer/extensions/front/tf/ssd_v2_support.json` - use the configuration file with custom operation description. (which is also located in `/opt/intel/openvino/deployment_tools/model_optimizer/extensions/front/tf`) (maybe igonre now)

[Intel - OpenVINO Toolkit - Converting TensorFlow* Object Detection API Models](https://docs.openvinotoolkit.org/latest/_docs_MO_DG_prepare_model_convert_model_tf_specific_Convert_Object_Detection_API_Models.html#how_to_convert_a_model)

> `\` backslash effectively allows the a command to span multiple lines to make it easier to read a long command.
>
> Reference: [What does this command with a backslash at the end do?](https://unix.stackexchange.com/questions/368753/what-does-this-command-with-a-backslash-at-the-end-do)

{::options parse_block_html="true" /}

<details>
<summary markdown="span">log</summary>

```
(venv) root@873a2f7d04af:/home/workspace/ssd_mobilenet_v2_coco_2018_03_29# python /opt/intel/openvino/deployment_tools/model_optimizer/mo.py \
>   --input_model /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/frozen_inference_graph.pb \
>   --tensorflow_object_detection_api_pipeline_config /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/pipeline.config \
>   --reverse_input_channels \
>   --tensorflow_use_custom_operations_config /opt/intel/openvino/deployment_tools/model_optimizer/extensions/front/tf/ssd_v2_support.json
Model Optimizer arguments:
Common parameters:
        - Path to the Input Model:      /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/frozen_inference_graph.pb
        - Path for generated IR:        /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/.
        - IR output name:       frozen_inference_graph
        - Log level:    ERROR
        - Batch:        Not specified, inherited from the model
        - Input layers:         Not specified, inherited from the model
        - Output layers:        Not specified, inherited from the model
        - Input shapes:         Not specified, inherited from the model
        - Mean values:  Not specified
        - Scale values:         Not specified
        - Scale factor:         Not specified
        - Precision of IR:      FP32
        - Enable fusing:        True
        - Enable grouped convolutions fusing:   True
        - Move mean values to preprocess section:       False
        - Reverse input channels:       True
TensorFlow specific parameters:
        - Input model in text protobuf format:  False
        - Path to model dump for TensorBoard:   None
        - List of shared libraries with TensorFlow custom layers implementation:    None
        - Update the configuration file with input/output node names:   None
        - Use configuration file used to generate the model with Object Detection API:      /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/pipeline.config
        - Operations to offload:        None
        - Patterns to offload:  None
        - Use the config file:  /opt/intel/openvino/deployment_tools/model_optimizer/extensions/front/tf/ssd_v2_support.json
Model Optimizer version:        2019.3.0-408-gac8584cb7
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorflow/python/framework/dtypes.py:516: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint8 = np.dtype([("qint8", np.int8, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorflow/python/framework/dtypes.py:517: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint8 = np.dtype([("quint8", np.uint8, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorflow/python/framework/dtypes.py:518: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint16 = np.dtype([("qint16", np.int16, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorflow/python/framework/dtypes.py:519: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint16 = np.dtype([("quint16", np.uint16, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorflow/python/framework/dtypes.py:520: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint32 = np.dtype([("qint32", np.int32, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorflow/python/framework/dtypes.py:525: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  np_resource = np.dtype([("resource", np.ubyte, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:541: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint8 = np.dtype([("qint8", np.int8, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:542: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint8 = np.dtype([("quint8", np.uint8, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:543: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint16 = np.dtype([("qint16", np.int16, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:544: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint16 = np.dtype([("quint16", np.uint16, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:545: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint32 = np.dtype([("qint32", np.int32, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:550: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  np_resource = np.dtype([("resource", np.ubyte, 1)])
The Preprocessor block has been removed. Only nodes performing mean value subtraction and scaling (if applicable) are kept.

[ SUCCESS ] Generated IR model.
[ SUCCESS ] XML file: /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/./frozen_inference_graph.xml
[ SUCCESS ] BIN file: /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/./frozen_inference_graph.bin
[ SUCCESS ] Total execution time: 89.62 seconds.
```
</details>

{::options parse_block_html="false" /}

As you see at the end of the log, the TensorFlow Model, the SSD MobileNet V2 COCO model sucessfully converts the Intermediate Representation (IR) model for OpenVINO Toolkit.

```
# omitted ...
[ SUCCESS ] Generated IR model.
[ SUCCESS ] XML file: /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/./frozen_inference_graph.xml
[ SUCCESS ] BIN file: /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/./frozen_inference_graph.bin
[ SUCCESS ] Total execution time: 89.62 seconds.
```

Check `.xml` and `.bin` files for the converted IR model at `/home/workspace/ssd_mobilenet_v2_coco_2018_03_29/./`.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">log</summary>

Run for checking
```
# ls -l
```

log

```
(venv) root@befe18074801:/home/workspace/ssd_mobilenet_v2_coco_2018_03_29# ls -l
total 203520
-rw-r--r-- 1 345018 89939       77 Mar 30  2018 checkpoint
-rw-r--r-- 1 root   root  67272876 Jan 18 06:53 frozen_inference_graph.bin
-rw-r--r-- 1 root   root     49370 Jan 18 06:53 frozen_inference_graph.mapping
-rw-r--r-- 1 345018 89939 69688296 Mar 30  2018 frozen_inference_graph.pb
-rw-r--r-- 1 root   root    112028 Jan 18 06:53 frozen_inference_graph.xml
-rw-r--r-- 1 345018 89939 67505156 Mar 30  2018 model.ckpt.data-00000-of-00001
-rw-r--r-- 1 345018 89939    15069 Mar 30  2018 model.ckpt.index
-rw-r--r-- 1 345018 89939  3496023 Mar 30  2018 model.ckpt.meta
-rw-r--r-- 1 345018 89939     4204 Mar 30  2018 pipeline.config
drwxr-xr-x 3 345018 89939     4096 Mar 30  2018 saved_model
(venv) root@befe18074801:/home/workspace/ssd_mobilenet_v2_coco_2018_03_29#
```

</details>

{::options parse_block_html="false" /}

### Solution: Convert a TF Model

To work more efficiently the long execution command, we can set up path environment variables as you run three export commands:

```
# export MOD_OPT=/opt/intel/openvino/deployment_tools/model_optimizer
# export OPT_TF_CONF=/opt/intel/openvino/deployment_tools/model_optimizer/extensions/front/tf
# export TF_MOD=/home/workspace/ssd_mobilenet_v2_coco_2018_03_29
```

> `export MOD_OPT=/opt/intel/openvino/deployment_tools/model_optimizer` - Creates the "MOD_OPT" environment variable and assign the value "/opt/intel/openvino/deployment_tools/model_optimizer" to it on your current console.  
> below two export commands are almost same. You can choose variable name and value you want. (In this case, I chose `OPT_TF_CONF` and `TF_MOD` as the variable name)
>
> Reference: [path environment variable](https://help.ubuntu.com/community/EnvironmentVariables)

<details>
<summary>log</summary>

<pre>
(venv) root@873a2f7d04af:/home/workspace/ssd_mobilenet_v2_coco_2018_03_29# export MOD_OPT=/opt/intel/openvino/deployment_tools/model_optimizer
(venv) root@873a2f7d04af:/home/workspace/ssd_mobilenet_v2_coco_2018_03_29# export OPT_TF_CONF=opt/intel/openvino/deployment_tools/model_optimizer/extensions/front/tf
(venv) root@873a2f7d04af:/home/workspace/ssd_mobilenet_v2_coco_2018_03_29# export TF_MOD=/home/workspace/ssd_mobilenet_v2_coco_2018_03_29
(venv) root@873a2f7d04af:/home/workspace/ssd_mobilenet_v2_coco_2018_03_29#
</pre>
</details>

Now you can run more cleaner commands for converting.

```
# python $MOD_OPT/mo.py \
  --input_model $TF_MOD/frozen_inference_graph.pb \
  --tensorflow_object_detection_api_pipeline_config $TF_MOD/pipeline.config \
  --reverse_input_channels \
  --tensorflow_use_custom_operations_config $OPT_TF_CONF/ssd_v2_support.json
```

## Exercise: Convert a Caffe Model

Make sure to click the `SOURCE ENV` button before you get started to source the correct environment.

<details>
<summary>log</summary>

<pre>
root@d8a038f20a83:/home/workspace# source /opt/intel/openvino/bin/setupvars.sh -pyver 3.5
python_version = 3.5
[setupvars.sh] OpenVINO environment initialized
(venv) root@d8a038f20a83:/home/workspace#
</pre>
</details>

### SqueezeNet V1.1 model

Instead of `wget` downloading a model, this time you download the SqueezeNet V1.1 model by cloning [this repository](https://github.com/forresti/SqueezeNet).

```
# git clone https://github.com/DeepScale/SqueezeNet
```

> `git clone https://github.com/DeepScale/SqueezeNet` - `git clone` obtain a local copy of a Github repository at the location, https://github.com/DeepScale/SqueezeNet  
> Reference: [git clone tutorial](https://www.atlassian.com/git/tutorials/setting-up-a-repository/git-clone)

{::options parse_block_html="true" /}

<details>
<summary markdown="span">git clone log</summary>

log

```
(venv) root@d8a038f20a83:/home/workspace# git clone https://github.com/DeepScale/SqueezeNet
Cloning into 'SqueezeNet'...
remote: Enumerating objects: 107, done.
remote: Total 107 (delta 0), reused 0 (delta 0), pack-reused 107
Receiving objects: 100% (107/107), 8.83 MiB | 0 bytes/s, done.
Resolving deltas: 100% (49/49), done.
Checking connectivity... done.
(venv) root@d8a038f20a83:/home/workspace#
```

Check the local copy, SqueezeNet with `ls -l`

```
(venv) root@d8a038f20a83:/home/workspace# ls -l
total 84
-rw-r--r-- 1 root root 68002 Jan 18 08:16 Guide.ipynb
-rw-r--r-- 1 root root  1251 Dec 12 23:48 README.md
drwxr-xr-x 2 root root  4096 Dec 12 23:48 solution
drwxr-xr-x 5 root root  4096 Jan 18 09:59 SqueezeNet
(venv) root@d8a038f20a83:/home/workspace#
```

</details>

{::options parse_block_html="false" /}

Now let's find SqueezeNet V1.1 model's `.caffemodel` file and a `.prototxt` file which need to feed into the Model Optimizer.

Move `SqueezeNet` directory with `cd SqueezeNet` and check with `ls -l` command.

<details>
<summary>log</summary>

<pre>
(venv) root@d8a038f20a83:/home/workspace# cd SqueezeNet
(venv) root@d8a038f20a83:/home/workspace/SqueezeNet# ls -l
total 20
-rw-r--r-- 1 root root 1250 Jan 18 09:59 LICENSE
-rw-r--r-- 1 root root 4293 Jan 18 09:59 README.md
drwxr-xr-x 2 root root 4096 Jan 18 09:59 SqueezeNet_v1.0
drwxr-xr-x 2 root root 4096 Jan 18 09:59 SqueezeNet_v1.1
(venv) root@d8a038f20a83:/home/workspace/SqueezeNet#
</pre>
</details>

Here you can see `SqueezeNet_v1.1` and move into it again with `cd SqueezeNet_v1.1`

<details>
<summary>log</summary>

<pre>
(venv) root@d8a038f20a83:/home/workspace/SqueezeNet# cd SqueezeNet_v1.1
(venv) root@d8a038f20a83:/home/workspace/SqueezeNet/SqueezeNet_v1.1# ls -l
total 4880
-rw-r--r-- 1 root root    9678 Jan 18 09:59 deploy.prototxt
-rw-r--r-- 1 root root     640 Jan 18 09:59 README.md
-rw-r--r-- 1 root root     781 Jan 18 09:59 solver.prototxt
-rw-r--r-- 1 root root 4950080 Jan 18 09:59 squeezenet_v1.1.caffemodel
-rw-r--r-- 1 root root   11839 Jan 18 09:59 train_val.prototxt
(venv) root@d8a038f20a83:/home/workspace/SqueezeNet/SqueezeNet_v1.1#
</pre>
</details>

There are a few files:

> `deploy.prototxt` - please take a look this file using `cat`, you see about a hundred of layers which is considered as a deploy-ready prototxt file that contains a topology structure and layer attributes  
> Reference: [Converting a Caffe* Model](https://docs.openvinotoolkit.org/2018_R5/_docs_MO_DG_prepare_model_convert_model_Convert_Model_From_Caffe.html#caffe_specific_conversion_params)
>
> `solver.prototxt` - additional training details (we don't need it here)
>
> `README.md` - A README.md is a reference for other users visiting a repository and documents steps for them to get a model up and running.  
> Reference: [What is README.MD file and why do I need it?](https://www.quora.com/What-is-README-MD-file-and-why-do-I-need-it)
>
> `solver.prototxt` - additional training details (learning rate schedule, etc.) (we don't need it here)
>
> `squeezenet_v1.1.caffemodel` - pretrained model parameters
>
> `train_val.prototxt` - model architecture (we don't need it here)
>
> Reference: [SqueezeNet](https://github.com/forresti/SqueezeNet)

To convert a Caffe Model, we use `mo.py` file as we did in TensorFlow model convertion and specify `--input_proto` because the `.prototxt` file is not named the same as the model.

```
# python /opt/intel/openvino/deployment_tools/model_optimizer/mo.py \
  --input_model squeezenet_v1.1.caffemodel \
  --input_proto deploy.prototxt
```

> `python /opt/intel/openvino/deployment_tools/model_optimizer/mo.py` - the `mo.py` script to simply convert a model
>
> `--input_model squeezenet_v1.1.caffemodel` - the path to the input model `.caffemodel` file
>
> `--input_proto deploy.prototxt` - it specifies deploy-ready prototxt file

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Convert a Caffe Model log</summary>

```
(venv) root@d8a038f20a83:/home/workspace/SqueezeNet/SqueezeNet_v1.1# python /opt/intel/openvino/deployment_tools/model_optimizer/mo.py \
>   --input_model squeezenet_v1.1.caffemodel \
>   --input_proto deploy.prototxt
Model Optimizer arguments:
Common parameters:
        - Path to the Input Model:      /home/workspace/SqueezeNet/SqueezeNet_v1.1/squeezenet_v1.1.caffemodel
        - Path for generated IR:        /home/workspace/SqueezeNet/SqueezeNet_v1.1/.
        - IR output name:       squeezenet_v1.1
        - Log level:    ERROR
        - Batch:        Not specified, inherited from the model
        - Input layers:         Not specified, inherited from the model
        - Output layers:        Not specified, inherited from the model
        - Input shapes:         Not specified, inherited from the model
        - Mean values:  Not specified
        - Scale values:         Not specified
        - Scale factor:         Not specified
        - Precision of IR:      FP32
        - Enable fusing:        True
        - Enable grouped convolutions fusing:   True
        - Move mean values to preprocess section:       False
        - Reverse input channels:       False
Caffe specific parameters:
        - Path to Python Caffe* parser generated from caffe.proto:       /opt/intel/openvino/deployment_tools/model_optimizer/mo/front/caffe/proto
        - Enable resnet optimization:   True
        - Path to the Input prototxt:   /home/workspace/SqueezeNet/SqueezeNet_v1.1/deploy.prototxt
        - Path to CustomLayersMapping.xml:      Default
        - Path to a mean file:  Not specified
        - Offsets for a mean file:      Not specified
Model Optimizer version:        2019.3.0-408-gac8584cb7

[ SUCCESS ] Generated IR model.
[ SUCCESS ] XML file: /home/workspace/SqueezeNet/SqueezeNet_v1.1/./squeezenet_v1.1.xml
[ SUCCESS ] BIN file: /home/workspace/SqueezeNet/SqueezeNet_v1.1/./squeezenet_v1.1.bin
[ SUCCESS ] Total execution time: 5.88 seconds.
```

</details>

{::options parse_block_html="false" /}

You see the converting sucess.

```
# omitted ...
[ SUCCESS ] Generated IR model.
[ SUCCESS ] XML file: /home/workspace/SqueezeNet/SqueezeNet_v1.1/./squeezenet_v1.1.xml
[ SUCCESS ] BIN file: /home/workspace/SqueezeNet/SqueezeNet_v1.1/./squeezenet_v1.1.bin
[ SUCCESS ] Total execution time: 5.88 seconds.
```

and check the output `.xml` file and `.bin` file for inference engine with `ls -l`

<details>
<summary>log</summary>

<pre>
(venv) root@d8a038f20a83:/home/workspace/SqueezeNet/SqueezeNet_v1.1# ls -l
total 9768
-rw-r--r-- 1 root root    9678 Jan 18 09:59 deploy.prototxt
-rw-r--r-- 1 root root     640 Jan 18 09:59 README.md
-rw-r--r-- 1 root root     781 Jan 18 09:59 solver.prototxt
-rw-r--r-- 1 root root 4941984 Jan 18 11:00 squeezenet_v1.1.bin
-rw-r--r-- 1 root root 4950080 Jan 18 09:59 squeezenet_v1.1.caffemodel
-rw-r--r-- 1 root root    9200 Jan 18 11:00 squeezenet_v1.1.mapping
-rw-r--r-- 1 root root   36766 Jan 18 11:00 squeezenet_v1.1.xml
-rw-r--r-- 1 root root   11839 Jan 18 09:59 train_val.prototxt
(venv) root@d8a038f20a83:/home/workspace/SqueezeNet/SqueezeNet_v1.1#
</pre>
</details>

## Exercise: Convert an ONNX Model

Make sure to click the `SOURCE ENV` button before you get started to source the correct environment.

<details>
<summary>log</summary>

<pre>
root@0390971149ca:/home/workspace# source /opt/intel/openvino/bin/setupvars.sh -pyver 3.5
python_version = 3.5
[setupvars.sh] OpenVINO environment initialized
(venv) root@0390971149ca:/home/workspace#
</pre>
</details>

### AlexNet model

First, you will download the bvlc_alexnet model from provided URL, [https://s3.amazonaws.com/download.onnx/models/opset_8/bvlc_alexnet.tar.gz](https://s3.amazonaws.com/download.onnx/models/opset_8/bvlc_alexnet.tar.gz) with `wget`.

```
# wget https://s3.amazonaws.com/download.onnx/models/opset_8/bvlc_alexnet.tar.gz
```

> `wget http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_coco_2018_03_29.tar.gz` - wget is UNIX command for downloading files from the Internet. In this case, you will download the `opset_8/bvlc_alexnet.tar.gz`.

<details>
<summary>log</summary>

<pre>
(venv) root@0390971149ca:/home/workspace# wget https://s3.amazonaws.com/download.onnx/models/opset_8/bvlc_alexnet.tar.gz
--2020-01-19 07:55:10--  https://s3.amazonaws.com/download.onnx/models/opset_8/bvlc_alexnet.tar.gz
Resolving s3.amazonaws.com (s3.amazonaws.com)... 52.216.129.13
Connecting to s3.amazonaws.com (s3.amazonaws.com)|52.216.129.13|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 231241418 (221M) [binary/octet-stream]
Saving to: ‘bvlc_alexnet.tar.gz’

bvlc_alexnet.tar.gz   100%[======================>] 220.53M  70.0MB/s    in 3.2s    

2020-01-19 07:55:13 (70.0 MB/s) - ‘bvlc_alexnet.tar.gz’ saved [231241418/231241418]

(venv) root@0390971149ca:/home/workspace#
</pre>
</details>

You can check the `bvlc_alexnet.tar.gz` file under your current folder (in my case, `/home/workspace`) using `ls` command.

<details>
<summary>log</summary>

<pre>
(venv) root@0390971149ca:/home/workspace# ls -l
total 226132
-rw-r--r-- 1 root root 231241418 Jun 29  2018 bvlc_alexnet.tar.gz
-rw-r--r-- 1 root root     68036 Jan 19 07:16 Guide.ipynb
-rw-r--r-- 1 root root      1202 Dec 12 23:48 README.md
drwxr-xr-x 2 root root      4096 Dec 12 23:48 solution
(venv) root@0390971149ca:/home/workspace#
</pre>
</details>

Now extract the compressed file.

```
# tar -xvf bvlc_alexnet.tar.gz
```

> `tar -xvf bvlc_alexnet.tar.gz` - `tar` command for handling `**.tar.gz` file.  
> `x`: Extract a tar file.  
> `v`: Verbose output or show progress while extracting files.  
> `f`: Specify an archive or a tar filename. (bvlc_alexnet.tar.gz)

<details>
<summary>log</summary>

<pre>
(venv) root@0390971149ca:/home/workspace# tar -xvf bvlc_alexnet.tar.gz
bvlc_alexnet/
bvlc_alexnet/test_data_0.npz
bvlc_alexnet/test_data_2.npz
bvlc_alexnet/test_data_1.npz
bvlc_alexnet/test_data_set_0/
bvlc_alexnet/test_data_set_0/input_0.pb
bvlc_alexnet/test_data_set_0/output_0.pb
bvlc_alexnet/test_data_set_1/
bvlc_alexnet/test_data_set_1/input_0.pb
bvlc_alexnet/test_data_set_1/output_0.pb
bvlc_alexnet/test_data_set_2/
bvlc_alexnet/test_data_set_2/input_0.pb
bvlc_alexnet/test_data_set_2/output_0.pb
bvlc_alexnet/test_data_set_3/
bvlc_alexnet/test_data_set_3/input_0.pb
bvlc_alexnet/test_data_set_3/output_0.pb
bvlc_alexnet/test_data_set_4/
bvlc_alexnet/test_data_set_4/input_0.pb
bvlc_alexnet/test_data_set_4/output_0.pb
bvlc_alexnet/test_data_set_5/
bvlc_alexnet/test_data_set_5/input_0.pb
bvlc_alexnet/test_data_set_5/output_0.pb
bvlc_alexnet/model.onnx
(venv) root@0390971149ca:/home/workspace#
</pre>
</details>

Change a directory to an extracted folder, `bvlc_alexnet` and check inside with `ls -l` command.

```
# cd bvlc_alexnet
```

<details>
<summary>log</summary>

<pre>
(venv) root@0390971149ca:/home/workspace# cd bvlc_alexnet
(venv) root@0390971149ca:/home/workspace/bvlc_alexnet# ls -l
total 240212
-rw-r--r-- 1 135397 users 243863542 Jun 28  2018 model.onnx
-rw-r--r-- 1 135397 users    606504 Sep 20  2017 test_data_0.npz
-rw-r--r-- 1 135397 users    606504 Sep 20  2017 test_data_1.npz
-rw-r--r-- 1 135397 users    606504 Sep 20  2017 test_data_2.npz
drwxr-xr-x 2 135397 users      4096 Mar  2  2018 test_data_set_0
drwxr-xr-x 2 135397 users      4096 Mar  2  2018 test_data_set_1
drwxr-xr-x 2 135397 users      4096 Mar  2  2018 test_data_set_2
drwxr-xr-x 2 135397 users      4096 Jun 22  2018 test_data_set_3
drwxr-xr-x 2 135397 users      4096 Jun 22  2018 test_data_set_4
drwxr-xr-x 2 135397 users      4096 Jun 22  2018 test_data_set_5
(venv) root@0390971149ca:/home/workspace/bvlc_alexnet#
</pre>
</details>

Using the `mo_tf.py` script, convert AlexNet model to an IR model.

```
# python /opt/intel/openvino/deployment_tools/model_optimizer/mo.py \
  --input_model /home/workspace/bvlc_alexnet/model.onnx
```

> `python /opt/intel/openvino/deployment_tools/model_optimizer/mo.py` - Run `mo.py` python script of Model Optimizer
>
> `--input_model /home/workspace/bvlc_alexnet/model.onnx` - Feed in the ONNX model to the Model Optimizer using `--input_model` option.
>
> Reference: [Convert an ONNX* Model](https://docs.openvinotoolkit.org/latest/_docs_MO_DG_prepare_model_convert_model_Convert_Model_From_ONNX.html#Convert_From_ONNX)

{::options parse_block_html="true" /}

<details>
<summary markdown="span">log</summary>

```
(venv) root@0390971149ca:/home/workspace/bvlc_alexnet# python /opt/intel/openvino/deployment_tools/model_optimizer/mo.py \
>   --input_model /home/workspace/bvlc_alexnet/model.onnx
Model Optimizer arguments:
Common parameters:
        - Path to the Input Model:      /home/workspace/bvlc_alexnet/model.onnx
        - Path for generated IR:        /home/workspace/bvlc_alexnet/.
        - IR output name:       model
        - Log level:    ERROR
        - Batch:        Not specified, inherited from the model
        - Input layers:         Not specified, inherited from the model
        - Output layers:        Not specified, inherited from the model
        - Input shapes:         Not specified, inherited from the model
        - Mean values:  Not specified
        - Scale values:         Not specified
        - Scale factor:         Not specified
        - Precision of IR:      FP32
        - Enable fusing:        True
        - Enable grouped convolutions fusing:   True
        - Move mean values to preprocess section:       False
        - Reverse input channels:       False
ONNX specific parameters:
Model Optimizer version:        2019.3.0-408-gac8584cb7

[ SUCCESS ] Generated IR model.
[ SUCCESS ] XML file: /home/workspace/bvlc_alexnet/./model.xml
[ SUCCESS ] BIN file: /home/workspace/bvlc_alexnet/./model.bin
[ SUCCESS ] Total execution time: 4.99 seconds.
(venv) root@0390971149ca:/home/workspace/bvlc_alexnet#
```
</details>

{::options parse_block_html="false" /}

Converting suceeded.

```
# omitted ...
[ SUCCESS ] Generated IR model.
[ SUCCESS ] XML file: /home/workspace/bvlc_alexnet/./model.xml
[ SUCCESS ] BIN file: /home/workspace/bvlc_alexnet/./model.bin
# omitted ...
```

and check the output `model.xml` and `model.bin` file for inference engine with `ls -l`

<details>
<summary>log</summary>

<pre>
(venv) root@0390971149ca:/home/workspace/bvlc_alexnet# ls -l
total 478620
-rw-r--r-- 1 root   root  243860904 Jan 19 08:06 model.bin
-rw-r--r-- 1 root   root       2990 Jan 19 08:06 model.mapping
-rw-r--r-- 1 135397 users 243863542 Jun 28  2018 model.onnx
-rw-r--r-- 1 root   root      13033 Jan 19 08:06 model.xml
-rw-r--r-- 1 135397 users    606504 Sep 20  2017 test_data_0.npz
-rw-r--r-- 1 135397 users    606504 Sep 20  2017 test_data_1.npz
-rw-r--r-- 1 135397 users    606504 Sep 20  2017 test_data_2.npz
drwxr-xr-x 2 135397 users      4096 Mar  2  2018 test_data_set_0
drwxr-xr-x 2 135397 users      4096 Mar  2  2018 test_data_set_1
drwxr-xr-x 2 135397 users      4096 Mar  2  2018 test_data_set_2
drwxr-xr-x 2 135397 users      4096 Jun 22  2018 test_data_set_3
drwxr-xr-x 2 135397 users      4096 Jun 22  2018 test_data_set_4
drwxr-xr-x 2 135397 users      4096 Jun 22  2018 test_data_set_5
(venv) root@0390971149ca:/home/workspace/bvlc_alexnet#
</pre>
</details>

## Exercise: Custom Layers
### Custom Layers

You will walk you through the full walkthrough of creating a custom layer.

Make sure to click the `SOURCE ENV` button before you get started to source the correct environment.

<details>
<summary>log</summary>

<pre>
root@2659676823e2:/home/workspace# source /opt/intel/openvino/bin/setupvars.sh -pyver 3.5
python_version = 3.5
[setupvars.sh] OpenVINO environment initialized
(venv) root@2659676823e2:/home/workspace#
</pre>
</details>

### Build the Model

To shorten the long execution command, we can set up path environment variables with export command:

```
# export CLWS=/home/workspace/cl_tutorial
# export CLT=$CLWS/OpenVINO-Custom-Layers
```

> `export CLWS=/home/workspace/cl_tutorial` - Defines the "CLWS" environment variable and assign the value "/home/workspace/cl_tutorial" to it on your current console.  
>
> `export CLT=$CLWS/OpenVINO-Custom-Layers` - Same rule is applied here. The environment variable, `CLT` has the path, `$CLWS/OpenVINO-Custom-Layers`. The dollar sign can be used for defined environment variables. It combines the values of environment variables `/OpenVINO-Custom-Layers` here.  
> So `$CLWS/OpenVINO-Custom-Layers` means `/home/workspace/cl_tutorial/OpenVINO-Custom-Layers`
>
> Reference: [path environment variable](https://help.ubuntu.com/community/EnvironmentVariables)

<details>
<summary>log</summary>

<pre>
(venv) root@baaf3f5b8f13:/home/workspace# export CLWS=/home/workspace/cl_tutorial
(venv) root@baaf3f5b8f13:/home/workspace# export CLT=$CLWS/OpenVINO-Custom-Layers
(venv) root@baaf3f5b8f13:/home/workspace#
</pre>
</details>

For TensorFlow models, create new directory on `$CLWS`.

```
# mkdir $CLWS/tf_model
```

{::options parse_block_html="true" /}

<details>
<summary markdown="span">log</summary>

```
(venv) root@baaf3f5b8f13:/home/workspace# mkdir $CLWS/tf_model
(venv) root@baaf3f5b8f13:/home/workspace#
```

Check
```
(venv) root@baaf3f5b8f13:/home/workspace# ls -l $CLWS
total 32
drwxr-xr-x 4 root root  4096 Dec 12 23:48 OpenVINO-Custom-Layers
-rw-r--r-- 1 root root 23337 Dec 12 23:48 README.md
drwxr-xr-x 2 root root  4096 Jan 19 23:18 tf_model
```
</details>

{::options parse_block_html="false" /}

Now you have `tf_model` directory under `$CLWS`.

Using already prepared `build_cosh_model.py` scipt, create the TensorFlow model including the cosh layer.

```
# python $CLT/create_tf_model/build_cosh_model.py $CLWS/tf_model
```

> `python $CLT/create_tf_model/build_cosh_model.py $CLWS/tf_model` - create the TensorFlow model including the cosh layer. The second argument is assumed output folder, `$CLWS/tf_model`.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">log</summary>

```
(venv) root@baaf3f5b8f13:/home/workspace# python $CLT/create_tf_model/build_cosh_model.py $CLWS/tf_model
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorflow/python/framework/dtypes.py:516: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint8 = np.dtype([("qint8", np.int8, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorflow/python/framework/dtypes.py:517: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint8 = np.dtype([("quint8", np.uint8, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorflow/python/framework/dtypes.py:518: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint16 = np.dtype([("qint16", np.int16, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorflow/python/framework/dtypes.py:519: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint16 = np.dtype([("quint16", np.uint16, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorflow/python/framework/dtypes.py:520: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint32 = np.dtype([("qint32", np.int32, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorflow/python/framework/dtypes.py:525: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  np_resource = np.dtype([("resource", np.ubyte, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:541: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint8 = np.dtype([("qint8", np.int8, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:542: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint8 = np.dtype([("quint8", np.uint8, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:543: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint16 = np.dtype([("qint16", np.int16, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:544: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint16 = np.dtype([("quint16", np.uint16, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:545: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint32 = np.dtype([("qint32", np.int32, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:550: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  np_resource = np.dtype([("resource", np.ubyte, 1)])
WARNING:tensorflow:From /home/workspace/cl_tutorial/OpenVINO-Custom-Layers/create_tf_model/build_cosh_model.py:16: The name tf.get_default_graph is deprecated. Please use tf.compat.v1.get_default_graph instead.

WARNING:tensorflow:From /home/workspace/cl_tutorial/OpenVINO-Custom-Layers/create_tf_model/build_cosh_model.py:24: The name tf.placeholder is deprecated. Please use tf.compat.v1.placeholder instead.

WARNING:tensorflow:From /home/workspace/cl_tutorial/OpenVINO-Custom-Layers/create_tf_model/NetworkBuilder.py:16: The name tf.random_normal is deprecated. Please use tf.random.normal instead.

WARNING:tensorflow:From /home/workspace/cl_tutorial/OpenVINO-Custom-Layers/create_tf_model/NetworkBuilder.py:18: The name tf.summary.histogram is deprecated. Please use tf.compat.v1.summary.histogram instead.

WARNING:tensorflow:From /home/workspace/cl_tutorial/OpenVINO-Custom-Layers/create_tf_model/NetworkBuilder.py:25: The name tf.nn.max_pool is deprecated. Please use tf.nn.max_pool2d instead.

WARNING:tensorflow:From /home/workspace/cl_tutorial/OpenVINO-Custom-Layers/create_tf_model/build_cosh_model.py:66: The name tf.summary.scalar is deprecated. Please use tf.compat.v1.summary.scalar instead.

WARNING:tensorflow:From /home/workspace/cl_tutorial/OpenVINO-Custom-Layers/create_tf_model/build_cosh_model.py:68: The name tf.train.AdamOptimizer is deprecated. Please use tf.compat.v1.train.AdamOptimizer instead.

WARNING:tensorflow:From /home/workspace/cl_tutorial/OpenVINO-Custom-Layers/create_tf_model/build_cosh_model.py:89: The name tf.Session is deprecated. Please use tf.compat.v1.Session instead.

2020-01-19 23:26:34.545893: I tensorflow/core/platform/cpu_feature_guard.cc:142] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2 FMA
2020-01-19 23:26:34.591003: I tensorflow/core/platform/profile_utils/cpu_utils.cc:94] CPU Frequency: 2300000000 Hz
2020-01-19 23:26:34.591692: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x3d79f60 executing computations on platform Host. Devices:
2020-01-19 23:26:34.591735: I tensorflow/compiler/xla/service/service.cc:175]   StreamExecutor device (0): <undefined>, <undefined>
WARNING:tensorflow:From /home/workspace/cl_tutorial/OpenVINO-Custom-Layers/create_tf_model/build_cosh_model.py:94: The name tf.train.Saver is deprecated. Please use tf.compat.v1.train.Saver instead.

WARNING:tensorflow:From /home/workspace/cl_tutorial/OpenVINO-Custom-Layers/create_tf_model/build_cosh_model.py:95: The name tf.summary.merge_all is deprecated. Please use tf.compat.v1.summary.merge_all instead.

WARNING:tensorflow:From /home/workspace/cl_tutorial/OpenVINO-Custom-Layers/create_tf_model/build_cosh_model.py:97: The name tf.summary.FileWriter is deprecated. Please use tf.compat.v1.summary.FileWriter instead.

WARNING:tensorflow:From /home/workspace/cl_tutorial/OpenVINO-Custom-Layers/create_tf_model/build_cosh_model.py:99: The name tf.global_variables_initializer is deprecated. Please use tf.compat.v1.global_variables_initializer instead.

2020-01-19 23:26:35.099356: W tensorflow/compiler/jit/mark_for_compilation_pass.cc:1412] (One-time warning): Not using XLA:CPU for cluster because envvar TF_XLA_FLAGS=--tf_xla_cpu_global_jit was not set.  If you want XLA:CPU, either set that envvar, or use experimental_jit_scope to enable XLA:CPU.  To confirm that XLA is active, pass --vmodule=xla_compilation_cache=1 (as a proper command-line flag, not via TF_XLA_FLAGS) or set the envvar XLA_FLAGS=--xla_hlo_profile.
WARNING:tensorflow:From /home/workspace/cl_tutorial/OpenVINO-Custom-Layers/create_tf_model/build_cosh_model.py:102: The name tf.train.write_graph is deprecated. Please use tf.io.write_graph instead.

WARNING:tensorflow:From /home/workspace/cl_tutorial/OpenVINO-Custom-Layers/create_tf_model/build_cosh_model.py:106: convert_variables_to_constants (from tensorflow.python.framework.graph_util_impl) is deprecated and will be removed in a future version.
Instructions for updating:
Use `tf.compat.v1.graph_util.convert_variables_to_constants`
WARNING:tensorflow:From /opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorflow/python/framework/graph_util_impl.py:270: extract_sub_graph (from tensorflow.python.framework.graph_util_impl) is deprecated and will be removed in a future version.
Instructions for updating:
Use `tf.compat.v1.graph_util.extract_sub_graph`

Model saved in path: /home/workspace/cl_tutorial/tf_model/model.ckpt

(venv) root@baaf3f5b8f13:/home/workspace#
```
</details>

{::options parse_block_html="false" /}

As we intended, there is the model under `$CLWS/tf_model`

```
# omitted ...
Model saved in path: /home/workspace/cl_tutorial/tf_model/model.ckpt
```

### Creating the cosh Custom Layer

To store the output from the Model Extension Generator, create `cl_cosh` folder in the `$CLWS` directory.

```
# mkdir $CLWS/cl_cosh
```

<details>
<summary>log</summary>

<pre>
(venv) root@baaf3f5b8f13:/home/workspace# mkdir $CLWS/cl_cosh
(venv) root@baaf3f5b8f13:/home/workspace# ls -l $CLWS
total 36
drwxr-xr-x 2 root root  4096 Jan 19 23:48 cl_cosh
drwxr-xr-x 4 root root  4096 Dec 12 23:48 OpenVINO-Custom-Layers
-rw-r--r-- 1 root root 23337 Dec 12 23:48 README.md
drwxr-xr-x 2 root root  4096 Jan 19 23:26 tf_model
(venv) root@baaf3f5b8f13:/home/workspace#
</pre>
</details>

To automatically create templates for all the extensions needed, we use the Model Extension Generator tool, `extgen.py` python script.  
Reference: [Custom Layers Guide](https://docs.openvinotoolkit.org/latest/_docs_HOWTO_Custom_Layers_Guide.html)

To understand the `extgen.py` python script, you can use `--help` option.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">log</summary>

```
(venv) root@aa4ccc137c4f:/home/workspace# python /opt/intel/openvino/deployment_tools/tools/extension_generator/extgen.py -h
usage: Extensions generator has two modes
    * Interactive mode - the tool prompts you to input information
      extgen command [<args>]

    * Silent mode - the tool reads the input information from a configuration file.
      extgen config.json

You can run it with the following commands:
    * to generate Model Optimizer extension (both extractor and operation) for unsupported TensorFlow* layer
        extgen new --mo-tf-ext --mo-op --output_dir=<output path>
    * to generate Model Optimizer extension for TensorFlow* layer and Inference Engine CPU extension
        extgen new --mo-tf-ext --mo-op --ie-cpu-ext --output_dir=<output path>
    * to generate Model Optimizer extension for Caffe* layer and Inference Engine CPU extension
        extgen new --mo-caffe-ext --mo-op --ie-cpu-ext --output_dir=<output path>
    * to generate Model Optimizer extension for MXNet* layer
        extgen new --mo-mxnet-ext --mo-op --output_dir=<output path>

To get more information about arguments for interactive mode, run:
  extgen new --help

Generates extension source files with stubs for the core functions

positional arguments:
  command     The only supported command is new, which generates Model
              Optimizer and Inference Engine extensions
  {}

optional arguments:
  -h, --help  show this help message and exit
(venv) root@aa4ccc137c4f:/home/workspace#
```
</details>

{::options parse_block_html="false" /}

As you can see, Extensions generator has two modes. Here, we will use Interactive mode.

```
Extensions generator has two modes
    * Interactive mode - the tool prompts you to input information
      extgen command [<args>]

    * Silent mode - the tool reads the input information from a configuration file.
      extgen config.json
```

For the Interactive mode, we use `new`, which is the only supported command and generates Model Optimizer and Inference Engine extensions.

Now, create the four extensions for the cosh custom layer using the Model Extension Generator.

```
# python /opt/intel/openvino/deployment_tools/tools/extension_generator/extgen.py \
  new \
  --mo-tf-ext \
  --mo-op \
  --ie-cpu-ext \
  --ie-gpu-ext \
  --output_dir=$CLWS/cl_cosh
```

> `python /opt/intel/openvino/deployment_tools/tools/extension_generator/extgen.py` - the Model Extension Generator tool to automatically create templates for all the extensions needed by the Model Optimizer to convert and the Inference Engine to execute the custom layer.
>
> `new` - keyword for the Interactive mode
>
> `--mo-tf-ext` - Generate a template for a Model Optimizer TensorFlow extractor
>
> `--mo-op` - Generate a template for a Model Optimizer custom layer operation
>
> `--ie-cpu-ext` - Generate a template for an Inference Engine CPU extension
>
> `--ie-gpu-ext` - Generate a template for an Inference Engine GPU extension
>
> `--output_dir=$CLWS/cl_cosh` - Set the output directory. Here we are using `$CLWS/cl_cosh` as the target directory which means `/home/workspace/cl_tutorial/cl_cosh`

{::options parse_block_html="true" /}

<details>
<summary markdown="span">log</summary>

```
(venv) root@aa4ccc137c4f:/home/workspace# python /opt/intel/openvino/deployment_tools/tools/extension_generator/extgen.py new --mo-tf-ext --mo-op --ie-cpu-ext --ie-gpu-ext --output_dir=$CLWS/cl_cosh
Generating:
  Model Optimizer:
    Extractor for Caffe Custom Layer: No
      Extractor for MxNet Custom Layer: No
    Extractor for TensorFlow Custom Layer: Yes
      Framework-agnostic operation extension: Yes
    Inference Engine:
      CPU extension: Yes
      GPU extension: Yes

Enter layer name:   cosh

Do you want to automatically parse all parameters from the model file? (y/n)
  Yes means layer parameters will be automatically parsed during Model Optimizer work as is.
  No means you will be prompted for layer parameters in the following section    n

Enter all parameters in the following format:
  <param1> <new name1> <type1>
  <param2> <new name2> <type2>
  ...
Where type is one of the following types:

  batch - Get batch from dataFormat,      spatial - Get spatial from dataFormat,  shape - TensorShapeProto,               
  list.b - List of bools,                 list.s - List of strings,               list.shape - List of TensorShapeProto,  
  channel - Get channel from dataFormat,  list.i - List of ints,                  list.type - List of DataType,           
  i - Int,                                type - DataType,                        b - Bool,                               
  padding - Padding type,                 s - String,                             f - Float,                              
  list.f - List of floats,                
Example:
  length attr_length i

If your attribute type is not shown in the list above, or you want to implement your own attribute parsing,
omit the <type> parameter.
Enter 'q' when finished:    q


**********************************************************************************************
Check your answers for TensorFlow* extractor generation:

1.  Layer name:                                                            cosh
2.  Automatically parse all parameters from model file:                    No
3.  Parameters entered:  <param1> <new name1> <type1>                      []

**********************************************************************************************

Do you want to change any answer (y/n) ? Default 'no'
n

Do you want to use the layer name as the operation name? (y/n)    y

Does your operation change shape? (y/n)    n


**********************************************************************************************
Check your answers for the Model Optimizer operation generation:

4.  Use layer name as operation name? (y/n)                                Yes
5.  Operation changes shape? (y/n)                                         No

**********************************************************************************************

Do you want to change any answer (y/n) ? Default 'no'
n

The following folders and files were created:

Stub file for TensorFlow Model Optimizer extractor is in /home/workspace/cl_tutorial/cl_cosh/user_mo_extensions/front/tf folder
Stub file for the Model Optimizer operation is in /home/workspace/cl_tutorial/cl_cosh/user_mo_extensions/ops folder
Stub files for the Inference Engine CPU extension are in /home/workspace/cl_tutorial/cl_cosh/user_ie_extensions/cpu folder
Stub files for the Inference Engine GPU extension are in /home/workspace/cl_tutorial/cl_cosh/user_ie_extensions/gpu folder
```
</details>

{::options parse_block_html="false" /}

It is interactive mode, so you are asked some questions.

For example, type `cosh` and hit the Enter.

```
Enter layer name:
[cosh]

Do you want to automatically parse all parameters from the model file? (y/n)
...
[n]

Enter all parameters in the following format:
...
Enter 'q' when finished:
[q]

Do you want to change any answer (y/n) ? Default 'no'
[n]

Do you want to use the layer name as the operation name? (y/n)
[y]

Does your operation change shape? (y/n)  
[n]

Do you want to change any answer (y/n) ? Default 'no'
[n]
```

After executing, the final part of log shows us about folders and files were created.

```
# omitted ...
Stub file for TensorFlow Model Optimizer extractor is in /home/workspace/cl_tutorial/cl_cosh/user_mo_extensions/front/tf folder
Stub file for the Model Optimizer operation is in /home/workspace/cl_tutorial/cl_cosh/user_mo_extensions/ops folder
Stub files for the Inference Engine CPU extension are in /home/workspace/cl_tutorial/cl_cosh/user_ie_extensions/cpu folder
Stub files for the Inference Engine GPU extension are in /home/workspace/cl_tutorial/cl_cosh/user_ie_extensions/gpu folder
```

Check at once with:

```
# ls -l $CLWS/cl_cosh/user_mo_extensions/front/tf/ $CLWS/cl_cosh/user_mo_extensions/ops $CLWS/cl_cosh/user_ie_extensions/cpu $CLWS/cl_cosh/user_ie_extensions/gpu
```

> `ls -l $CLWS/cl_cosh/user_mo_extensions/front/tf/ $CLWS/cl_cosh/user_mo_extensions/ops $CLWS/cl_cosh/user_ie_extensions/cpu $CLWS/cl_cosh/user_ie_extensions/gpu` - `ls` accepts more than one file/directory arguments.

<details>
<summary>log</summary>

<pre>
(venv) root@2c847fc30220:/home/workspace# ls -l $CLWS/cl_cosh/user_mo_extensions/front/tf/ $CLWS/cl_cosh/user_mo_extensions/ops $CLWS/cl_cosh/user_ie_extensions/cpu $CLWS/cl_cosh/user_ie_extensions/gpu
/home/workspace/cl_tutorial/cl_cosh/user_ie_extensions/cpu:
total 36
-rw-r--r-- 1 root root  1855 Jan 21 06:39 CMakeLists.txt
-rw-r--r-- 1 root root  4426 Jan 21 06:39 ext_base.cpp
-rw-r--r-- 1 root root 11548 Jan 21 06:39 ext_base.hpp
-rw-r--r-- 1 root root  3215 Jan 21 06:39 ext_cosh.cpp
-rw-r--r-- 1 root root  3797 Jan 21 06:39 ext_list.cpp
-rw-r--r-- 1 root root  2224 Jan 21 06:39 ext_list.hpp

/home/workspace/cl_tutorial/cl_cosh/user_ie_extensions/gpu:
total 8
-rw-r--r-- 1 root root  951 Jan 21 06:39 cosh_kernel.cl
-rw-r--r-- 1 root root 2170 Jan 21 06:39 cosh_kernel.xml

/home/workspace/cl_tutorial/cl_cosh/user_mo_extensions/front/tf/:
total 4
-rw-r--r-- 1 root root 1450 Jan 21 06:39 cosh_ext.py
-rw-r--r-- 1 root root    0 Jan 21 06:37 __init__.py

/home/workspace/cl_tutorial/cl_cosh/user_mo_extensions/ops:
total 4
-rw-r--r-- 1 root root 1923 Jan 21 06:39 cosh.py
-rw-r--r-- 1 root root    0 Jan 21 06:37 __init__.py
(venv) root@2c847fc30220:/home/workspace#
</pre>
</details>

### Using Model Optimizer to Generate IR Files Containing the Custom Layer

Before generating the model IR files needed by the Inference Engine, we will check the generated extractor and operation extensions for the Model Optimizer.

The extractor extension is responsible for identifying the custom layer operation (operation extension) and extracting the parameters for each custom layer.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Edit the Extractor Extension Template File</summary>

First open the file, `$CLWS/cl_cosh/user_mo_extensions/front/tf/cosh_ext.py` from File Browser on the left side on workspace.

{::options parse_block_html="false" /}

{% include helpers/image.html name="Screen Shot 2020-01-22 at 8.58.25.png" %}

{::options parse_block_html="true" /}

There are some import statements for creating Extractor Extension Template File. (no need to understnad too much)

```
# omitted ...
import numpy as np

from mo.front.extractor import FrontExtractorOp
from mo.ops.op import Op
from mo.front.tf.extractors.utils import *
from mo.front.common.partial_infer.utils import convert_tf_padding_to_str
# omitted ...
```

> `from mo.front.extractor import FrontExtractorOp` - import `FrontExtractorOp` class from `mo.front.extractor`. `FrontExtractorOp` provides basic methods for TensorFlow Model Optimizer extractor.  
> FYI, `mo.front.extractor` comes from `/opt/intel/openvino/deployment_tools/model_optimizer/mo/front/extractor.py`
>
> `from mo.ops.op import Op` - Same above. `Op` class has the base operations for Extractor Extension.
>
> `from mo.front.tf.extractors.utils import *` - Same above. importing from utils, so there is some helper methods.
>
> `from mo.front.common.partial_infer.utils import convert_tf_padding_to_str` - Same above. Also some helper methods are imported.

It starts `coshFrontExtractor` class.

```
# omitted ...
class coshFrontExtractor(FrontExtractorOp):
     op = 'cosh'
     enabled = True
# omitted ...
```

> `class coshFrontExtractor(FrontExtractorOp):` - Create a class named coshFrontExtractor, which will inherit the properties and methods from the FrontExtractorOp class. You can use common methods on Extractor Extension.  
> Reference: [Python Inheritance](https://www.w3schools.com/python/python_inheritance.asp)
>
> `op = 'cosh'` - The variable `op` has `'cosh'` string.
>
> `enabled = True` - The variable `enabled` has `True` boolean value.


```
# omitted ...
@staticmethod
def extract(node):
# omitted ...
```

> `@staticmethod` - With `@staticmethod`, neither self (the object instance) nor  cls (the class) is implicitly passed as the first argument. The usual way an object instance calls a method. The object instance is implicitly passed as the first argument.
> don't worry about this if you don't understand well.
> Refrence: [https://stackoverflow.com/questions/136097/difference-between-staticmethod-and-classmethod](https://stackoverflow.com/questions/136097/difference-between-staticmethod-and-classmethod)
>
> `def extract(node):` - In Python a function is defined using the def keyword. And The `extract` function is overridden. Overriding means you can change the implementation of a method provided by one of its base classes. (in this case, `extract`).  
> Refrence: [Method overriding in Python](https://www.thedigitalcatonline.com/blog/2014/05/19/method-overriding-in-python/)  
> Also `node` means the input model as the first argument.

There is codes inside `extract` method.

```
 proto_layer = node.pb
 param = proto_layer.attr
 # extracting parameters from TensorFlow layer and prepare them for IR
 attrs = {
     'op': __class__.op
 }
```

> `proto_layer = node.pb` - The layer (`proto_layer`) are extracted from the input model, `node`.
>
> `param = proto_layer.attr` - The layer parameters, `proto_layer.attr` is assigned to `param` variable.
>
> ` attrs = { # omitted ... }` - defines a dictionary (data type) called `attrs` is a collection of data. In Python dictionaries are written with curly brackets, and they have keys and values.  
> Reference: [Python Dictionaries](https://www.w3schools.com/python/python_dictionaries.asp)  
>
> `'op': __class__.op` - The key is `op` and its value is `cosh` as we difined `op = 'cosh'` above.  
> Those defined values are used for updating node (input model)

There is the final part of the code.

```
 # update the attributes of the node
 Op.get_op_class_by_name(__class__.op).update_node_stat(node, attrs)

 return __class__.enabled
```

> `Op.get_op_class_by_name(__class__.op).update_node_stat(node, attrs)` - `Op` comes from import `from mo.ops.op import Op`. Usinf its functions like `get_op_class_by_name`. It updates the attributes of the node.
>
> `return __class__.enabled` - Finally, the enabled class variable is returned.

</details>

{::options parse_block_html="false" /}

The operation extension is responsible for specifying the attributes that are supported by the custom layer and computing the output shape for each instance of the custom layer from its parameters.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Edit the Operation Extension Template File</summary>

Open the file, `$CLWS/cl_cosh/user_mo_extensions/ops/cosh.py` from File Browser on the left side on workspace.

There are some import statements. (please don't worry)

```
# omitted ...
from mo.ops.op import Op
from mo.front.common.partial_infer.elemental import copy_shape_infer
from mo.graph.graph import Node
# omitted ...
```

> `from mo.ops.op import Op` - Import `Op` class from `from mo.ops.op`. `Op` class has the base operations for Extractor Extension.  
> FYI, `mo.ops.op` comes from `/opt/intel/openvino/deployment_tools/model_optimizer/mo/ops.op.py`
>
> `from mo.front.common.partial_infer.elemental import copy_shape_infer` - Same above. `copy_shape_infer` helper function for returning the shape of the layer for each node.
>
> `from mo.graph.graph import Node` - Same above. A node is just a place where computation happens in neural network. The layers are made of nodes.

It starts with `coshOp` class inherites `Op`, the base operation class.

```
class coshOp(Op):
    op = 'cosh'
```

> `class coshOp(Op):` - You can assume that `Op` class provides the base operation needs for Operation Extension Template File.
>
> `op = 'cosh'` - The variable `op` has `'cosh'` string.

The next function is initializer `__init__` function. This initializer `__init__` function will be called for each layer created.

```
def __init__(self, graph, attrs):
    mandatory_props = dict(
        type=__class__.op,
        op=__class__.op,

        infer=coshOp.infer            
    )
    super().__init__(graph, mandatory_props, attrs)
```

> `def __init__(self, graph, attrs):` - `__init__` is a special Python method that is automatically called when a new object is created.  
> Reference: [Explicit return in __init__](https://docs.quantifiedcode.com/python-anti-patterns/correctness/explicit_return_in_init.html)
> The three arguments, `self`, `graph` and `attrs` are passed in. `self` variable represents the instance of the object itself.  
> Reference: [What __init__ and self do on Python?](https://stackoverflow.com/questions/625083/what-init-and-self-do-on-python)
>
> `mandatory_props = dict( # omitted ... )` - It defines a dictionary data type called `mandatory_props`.
>
> `type=__class__.op,` - The variable `op` which has `'cosh'` string is assigned to `type` variable.
>
> `op=__class__.op,` - The variable `op` which has `'cosh'` string is assigned to `op` variable on `mandatory_props` dictionary.
>
> `infer=coshOp.infer` - For `infer` variable, `infer` function of `coshOp` class is assigned.
>
> `super().__init__(graph, mandatory_props, attrs)` - This initializer initializes the super class `Op` by passing the `graph` and `attrs` arguments along with a dictionary of the mandatory properties for the cosh operation layer.

The final part is about `infer` function.

```
@staticmethod
def infer(node: Node):
    # ==========================================================
    # You should add your shape calculation implementation here
    # If a layer input shape is different to the output one
    # it means that it changes shape and you need to implement
    # it on your own. Otherwise, use copy_shape_infer(node).
    # ==========================================================
    return copy_shape_infer(node)
```

> `@staticmethod` - With `@staticmethod`, self (the object instance) is implicitly passed as the first argument. So explicitly it means `def infer(self, node: Node):`.
>
> `def infer(node: Node):` - It defines `infer` function. `:` inside parentheses means the `node` variable is intended as Node type.  
> Reference: [Function parameter with colon](https://stackoverflow.com/questions/54962869/function-parameter-with-colon)
>
> `return copy_shape_infer(node)` - returning the shape of the layer output for each node. `copy_shape_infer` function is a helper function for returning the shape.

</details>

{::options parse_block_html="false" /}

Now it is time to use the Model Optimizer to convert and optimize the example TensorFlow model into IR files.

Move to the location of the TensorFlow model, `# cd $CLWS/tf_model` and Run

```
# python /opt/intel/openvino/deployment_tools/model_optimizer/mo.py \
  --input_meta_graph model.ckpt.meta \
  --batch 1 \
  --output "ModCosh/Activation_8/softmax_output" \
  --extensions $CLWS/cl_cosh/user_mo_extensions \
  --output_dir $CLWS/cl_ext_cosh
```

> `python /opt/intel/openvino/deployment_tools/model_optimizer/mo.py` - we uses `mo.py` as the Model Optimizer. The `mo.py` script is the universal entry point that can deduce the framework that has produced the input model by a standard extension of the model file. You can also use the `mo_tf.py` to do that as well, just that `mo_tf.py` is only specific to tensorflow models.
>
> `--input_meta_graph model.ckpt.meta` - Specifies the model input file, a file with a meta-graph of the model before freezing.
>
> `--batch 1` - Explicitly sets the batch size to 1 because this example model has "-1" as an input dimension. So "-1" will cause an error for the Model Optimizer. In TensorFlow allows "-1" as a variable indicating "to be filled in later", however the Model Optimizer requires explicit information for the optimization process.
>
> `--output "ModCosh/Activation_8/softmax_output"` - The full name of the final output layer of the model.
>
> `--extensions $CLWS/cl_cosh/user_mo_extensions` - Location of the extractor and operation extensions for the custom layer which we created just now.
>
> `--output_dir $CLWS/cl_ext_cosh` - Directory that stores the generated IR.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">log</summary>

```
root@102dcf238d4a:/home/workspace/cl_tutorial/tf_model# python /opt/intel/openvino/deployment_tools/model_optimizer/mo.py \
>   --input_meta_graph model.ckpt.meta \
>   --batch 1 \
>   --output "ModCosh/Activation_8/softmax_output" \
>   --extensions $CLWS/cl_cosh/user_mo_extensions \
>   --output_dir $CLWS/cl_ext_cosh
Model Optimizer arguments:
Common parameters:
        - Path to the Input Model:      None
        - Path for generated IR:        /home/workspace/cl_tutorial/cl_ext_cosh
        - IR output name:       model.ckpt
        - Log level:    ERROR
        - Batch:        1
        - Input layers:         Not specified, inherited from the model
        - Output layers:        ModCosh/Activation_8/softmax_output
        - Input shapes:         Not specified, inherited from the model
        - Mean values:  Not specified
        - Scale values:         Not specified
        - Scale factor:         Not specified
        - Precision of IR:      FP32
        - Enable fusing:        True
        - Enable grouped convolutions fusing:   True
        - Move mean values to preprocess section:       False
        - Reverse input channels:       False
TensorFlow specific parameters:
        - Input model in text protobuf format:  False
        - Path to model dump for TensorBoard:   None
        - List of shared libraries with TensorFlow custom layers implementation:None
        - Update the configuration file with input/output node names:   None
        - Use configuration file used to generate the model with Object Detection API:   None
        - Operations to offload:        None
        - Patterns to offload:  None
        - Use the config file:  None
Model Optimizer version:        2019.3.0-408-gac8584cb7
Converted 18 variables to const ops.

[ SUCCESS ] Generated IR model.
[ SUCCESS ] XML file: /home/workspace/cl_tutorial/cl_ext_cosh/model.ckpt.xml
[ SUCCESS ] BIN file: /home/workspace/cl_tutorial/cl_ext_cosh/model.ckpt.bin
[ SUCCESS ] Total execution time: 17.78 seconds.
root@102dcf238d4a:/home/workspace/cl_tutorial/tf_model#
```
</details>

{::options parse_block_html="false" /}

### Inference Engine Custom Layer Implementation for the Intel® CPU

First, edit the generated CPU Extension Template Files, `ext_cosh.cpp` and `CMakeLists.txt`.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Edit ext_cosh.cpp</summary>

Let's walk through the code and making the necessary changes for the cosh custom layer along the way.

Open the CPU extension source file `$CLWS/cl_cosh/user_ie_extensions/cpu/ext_cosh.cpp` on the workspace.

{::options parse_block_html="false" /}

{% include helpers/image.html name="Screen Shot 2020-01-25 at 15.18.51.png" %}

{::options parse_block_html="true" /}

You may notice it is written by C++ rather than Python.

You won't write any code on your own, just simple edit of few lines as per the instructions and please don't worry if you understand well.

```
#include "ext_list.hpp"
#include "ext_base.hpp"
#include <cmath>
#include <vector>
#include <string>
#include <algorithm>
```

> There are some include statements to includes other source file into current source file. `""` surrounded include files are at the directory where the current file resides. `<>` surrounded ones comes from comes from the standard C++ library and the standard C library.  
> Reference: [Source file inclusion](https://en.cppreference.com/w/cpp/preprocessor/include)

Add `#include "ie_parallel.hpp"` under the `#include "ext_base.hpp"` to efficiently execute in parallel, the code will use the parallel processing supported by the Inference Engine through the use of the Intel® Threading Building Blocks library.

```
#include "ext_list.hpp"
#include "ext_base.hpp"
#include "ie_parallel.hpp"
#include <cmath>
#include <vector>
#include <string>
#include <algorithm>
```

You can igonre the next namespace sections.
Namespaces provide a method for preventing name conflicts in large projects.

Reference: [Namespaces](https://en.cppreference.com/w/cpp/language/namespace)

```
namespace InferenceEngine {
namespace Extensions {
namespace Cpu {
```

The class `coshImpl` implements the cosh custom layer.

```
class coshImpl: public ExtLayerBase {
public:
```

> `class coshImpl: public ExtLayerBase {` - It inherits from the extension layer base class `ExtLayerBase`.  
> Reference: [Inheritance in C++](https://www.geeksforgeeks.org/inheritance-in-c/)
>
> `public:` - public access specifier. public members are accessible from anywhere where the object is visible.  
> Reference: [Classes (I)](http://www.cplusplus.com/doc/tutorial/classes/)

The `coshImpl` constructor is passed the layer object that it is associated with to provide access to any layer parameters.

```
explicit coshImpl(const CNNLayer* layer) {
  try {
```

> `explicit coshImpl(const CNNLayer* layer) { # omitted ... }` - This defines constructor for `coshImpl` class. Prefixing the `explicit` keyword to the constructor prevents the compiler from using that constructor for implicit conversions.  
> Reference: [What does the explicit keyword mean?](https://stackoverflow.com/questions/121162/what-does-the-explicit-keyword-mean)  
> The `const` keyword allows you to specify whether or not a variable is modifiable. You can use const to prevent modifications to variables. Here `layer` variable cannot be changable.  
> Reference: [Const Correctness](https://www.cprogramming.com/tutorial/const_correctness.html)  
> `CNNLayer* layer` declare a pointer points to `CNNLayer` data type.  
> Reference: [Pointers](http://www.cplusplus.com/doc/tutorial/pointers/)
>
> `try {` - To catch exceptions, a portion of code is placed under exception inspection. This is done by enclosing that portion of code in a try-block.  
> Reference: [Exceptions](http://www.cplusplus.com/doc/tutorial/exceptions/)

Add `addConfig` function inside try block for the custom layer to indicate that layer uses `DataConfigurator(ConfLayout::PLN)` data for both input and output.

```
# omitted ...
// addConfig({DataConfigurator(ConfLayout::PLN), DataConfigurator(ConfLayout::PLN)}, {DataConfigurator(ConfLayout::PLN)});
addConfig(layer, { DataConfigurator(ConfLayout::PLN) }, { DataConfigurator(ConfLayout::PLN) });
```

> `addConfig(layer, { DataConfigurator(ConfLayout::PLN) }, { DataConfigurator(ConfLayout::PLN) });` - You can assume that `addConfig` is a provided function for configuring the input and output data layout for the custom layer. The `::` operator is to help to resolve `PLN` is inside `ConfLayout`.
> Reference: [What is the meaning of prepended double colon “::”?](https://stackoverflow.com/questions/4269034/what-is-the-meaning-of-prepended-double-colon)

Here, catch block for catching and reporting certain exceptions if an exception is occured inside `try` block.

```
    } catch (InferenceEngine::details::InferenceEngineException &ex) {
            errorMsg = ex.what();
        }
    }
```

> `} catch (InferenceEngine::details::InferenceEngineException &ex) {` - The keyword `catch` starts catch block to handle exception. Again `::` shows this `InferenceEngineException` comes from `details` of `InferenceEngine`. The line `InferenceEngine::details::InferenceEngineException &ex` indeicates the exception which we intend to catch.  
> Reference: [Exceptions](http://www.cplusplus.com/doc/tutorial/exceptions/)  
> The `InferenceEngine::details::InferenceEngineException &ex` declare `ex` which reference to data type, `InferenceEngine::details::InferenceEngineException`.  
> Reference: [Reference (C++)](https://en.wikipedia.org/wiki/Reference_(C%2B%2B))  
> It doesn't matter space style between data type and indetifer.  
> Reference: [What's the semantically accurate position for the ampersand in C++ references](https://stackoverflow.com/questions/22766907/whats-the-semantically-accurate-position-for-the-ampersand-in-c-references)

To implement the functionality of the cosh custom layer, we will replace the execute method with the code needed to calculate the cosh function in parallel using the parallel_for3d function.

```
StatusCode execute(std::vector<Blob::Ptr>& inputs, std::vector<Blob::Ptr>& outputs,
 ResponseDesc *resp) noexcept override {
    // Add implementation for layer inference here
    // Examples of implementations are in OpenVINO samples/extensions folder

    // Get pointers to source and destination buffers
    float* src_data = inputs[0]->buffer();
    float* dst_data = outputs[0]->buffer();

    // Get the dimensions from the input (output dimensions are the same)
    SizeVector dims = inputs[0]->getTensorDesc().getDims();

    // Get dimensions:N=Batch size, C=Number of Channels, H=Height, W=Width
    int N = static_cast<int>((dims.size() > 0) ? dims[0] : 1);
    int C = static_cast<int>((dims.size() > 1) ? dims[1] : 1);
    int H = static_cast<int>((dims.size() > 2) ? dims[2] : 1);
    int W = static_cast<int>((dims.size() > 3) ? dims[3] : 1);

    // Perform (in parallel) the hyperbolic cosine given by:
    //    cosh(x) = (e^x + e^-x)/2
    parallel_for3d(N, C, H, [&](int b, int c, int h) {
        // Fill output_sequences with -1
        for (size_t ii = 0; ii < b*c; ii++) {
          dst_data[ii] = (exp(src_data[ii]) + exp(-src_data[ii]))/2;
        }
    });
    return OK;
}
```

> `StatusCode execute(std::vector<Blob::Ptr>& inputs, std::vector<Blob::Ptr>& outputs,
 ResponseDesc *resp) noexcept override` - `StatusCode` is the return type. Here, `std::vector<Blob::Ptr>` is the data type for the first argument. The `vector` template from `std`, `<Blob::Ptr>` is data type which is stored on this `vector`. In `std::vector<Blob::Ptr>& inputs`, `inputs` has reference to data type, `std::vector<Blob::Ptr>`. The same applied on `outputs` as well.
> Reference: [Functions](http://www.cplusplus.com/doc/tutorial/functions/)  
> The final parameter, `ResponseDesc *resp` declare a pointer, `resp` points to `ResponseDesc` type object.  
> Reference: [Type Declaration - Pointer Asterisk Position](https://stackoverflow.com/questions/2704167/type-declaration-pointer-asterisk-position)
>
> `float* src_data = inputs[0]->buffer();` - Declaring a pointor, `src_data` which points to float data type, `buffer()` inside the class which is pointed by `inputs[0]` pointer (address).
> Reference: [C++: difference between ampersand “&” and asterisk “*” in function/method declaration?](https://stackoverflow.com/questions/596636/c-difference-between-ampersand-and-asterisk-in-function-method-declar)  
> `inputs[0]->buffer()` accesses `buffer()` function inside an object of `inputs[0]` pointer. `float* dst_data = outputs[0]->buffer();` is the same for outputs.
>
> `SizeVector dims = inputs[0]->getTensorDesc().getDims();` - The variable name, `dims` has `inputs[0]->getTensorDesc().getDims()` value. Inside `inputs[0]->getTensorDesc().getDims()`, it uses `getTensorDesc()` function inside the class pointed by `inputs[0]` pointor. For the value (a class) of `getTensorDesc()` function, it is calling `getDims()` of the class.
>
> `int N = static_cast<int>((dims.size() > 0) ? dims[0] : 1);` - `static_cast<int>( # omitted ... );` is a function which returns int data type. Its argument is equivalent to "if `dims.size()` is greater than 0, return `dims[0]` otherwise return 1". The same principals goes the rest of three statements.  
> Reference: [Conditional Operator](https://mathbits.com/MathBits/CompSci/looping/operator2.htm)
>
> `parallel_for3d(N, C, H, [&](int b, int c, int h) { # omitted ... });` - This is an one function which `N, C, H, [&](int b, int c, int h) { # omitted ... }` is passed as parameters. The `[&]` introduces a lambda expression. The contents of the square brackets indicate what is to be captured inside the lambda. Having only a `&` in there means that everything that is mentioned inside the lambda and can be found outside of its scope is captured by reference.  
> Reference: [c++ \[&\] operator](https://stackoverflow.com/questions/12262019/c-operator)  
> Those `(int b, int c, int h)` which comes from local variables of the function, `N, C, H` are parameters for the lambda expression. `{ # omitted ... }` is the function body.  
> Reference: [Lambda expressions (since C++11)](https://en.cppreference.com/w/cpp/language/lambda)  
> the function body is about for-loop to fill output_sequences with -1.
>
> `return OK;` - finally it returns `OK` as StatusCode.

You can igonre the rest of the code.

</details>

{::options parse_block_html="false" /}

For the implementation of the `cosh` custom layer, we need to add the Intel® Threading Building Blocks dependency to CMakeLists.txt to use the parallel processing supported by the Inference Engine.

Here, a CMake build script is a plain text file that you must name CMakeLists.txt and includes commands CMake uses to build your C/C++ libraries.  
Reference: [Configure CMake](https://developer.android.com/studio/projects/configure-cmake)

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Edit CMakeLists.txt</summary>

Open the CPU extension CMake file `$CLWS/cl_cosh/user_ie_extensions/cpu/CMakeLists.txt`.

Rename the `TARGET_NAME` so that the compiled library is named `libcosh_cpu_extension.so`.

```
set(TARGET_NAME "cosh_cpu_extension")
```

Modify the include_directories to add the header include path for the Intel® Threading Building Blocks library located in `/opt/intel/openvino/deployment_tools/inference_engine/external/tbb/include`:

```
include_directories (PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/common
    ${InferenceEngine_INCLUDE_DIRS}
    "/opt/intel/openvino/deployment_tools/inference_engine/external/tbb/include"
)
```

Add the link_directories with the path to the Intel® Threading Building Blocks library binaries at `/opt/intel/openvino/deployment_tools/inference_engine/external/tbb/lib`:

```
link_directories(
    "/opt/intel/openvino/deployment_tools/inference_engine/external/tbb/lib"
)
#enable_omp()
```

Finally, add the Intel® Threading Building Blocks library tbb to the list of link libraries in target_link_libraries:

```
target_link_libraries(${TARGET_NAME} ${InferenceEngine_LIBRARIES} ${intel_omp_lib} tbb)
```

</details>

{::options parse_block_html="false" /}

Now it is time to compile the Extension Library to run the custom layer on the CPU during inference, the edited extension C++ source code must be compiled to create a .so shared library used by the Inference Engine.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Compile the Extension Library</summary>

Run the following commands to use CMake to setup for compiling:

```
# cd $CLWS/cl_cosh/user_ie_extensions/cpu
# mkdir -p build
# cd build
# cmake ..
```

> `cd $CLWS/cl_cosh/user_ie_extensions/cpu` - change directory to `$CLWS/cl_cosh/user_ie_extensions/cpu`
>
> `mkdir -p build` - make a directory called `build`. `-p` option create a directory without error here. (For example, mkdir -p a/b will create directory a if it doesn't exist, then will create directory b inside directory a .)
>
> `cd build` - move to `build` folder.
>
> `cmake ..` - `..` means shorthand for the parent folder (`cd $CLWS/cl_cosh/user_ie_extensions/cpu`). It generates a Makefile in the current directory, `build` following instructions given in `$CLWS/cl_cosh/user_ie_extensions/cpu/CMakeLists.txt`.

Log
```
root@36830e842745:/home/workspace# cd $CLWS/cl_cosh/user_ie_extensions/cpu
root@36830e842745:/home/workspace/cl_tutorial/cl_cosh/user_ie_extensions/cpu# mkdir -p build
root@36830e842745:/home/workspace/cl_tutorial/cl_cosh/user_ie_extensions/cpu# ls -l
total 44
drwxr-xr-x 2 root root  4096 Jan 26 07:35 build
-rw-r--r-- 1 root root  2038 Jan 26 07:22 CMakeLists.txt
-rw-r--r-- 1 root root  4426 Jan 21 06:39 ext_base.cpp
-rw-r--r-- 1 root root 11548 Jan 21 06:39 ext_base.hpp
-rw-r--r-- 1 root root  4304 Jan 26 06:25 ext_cosh.cpp
-rw-r--r-- 1 root root  3797 Jan 21 06:39 ext_list.cpp
-rw-r--r-- 1 root root  2224 Jan 21 06:39 ext_list.hpp
root@36830e842745:/home/workspace/cl_tutorial/cl_cosh/user_ie_extensions/cpu# cd build
root@36830e842745:/home/workspace/cl_tutorial/cl_cosh/user_ie_extensions/cpu/build#
(venv) root@36830e842745:/home/workspace/cl_tutorial/cl_cosh/user_ie_extensions/cpu/build# cmake ..
-- Looking for inference engine configuration file at: /home/workspace/cl_tutorial/cl_cosh/user_ie_extensions/cpu/InferenceEngine_DIR-NOTFOUND
-- Found InferenceEngine: /opt/intel/openvino_2019.3.376/deployment_tools/inference_engine/lib/intel64/libinference_engine.so (Required is at least version "1.0")
-- Performing Test HAVE_CPUID_INFO
-- Performing Test HAVE_CPUID_INFO - Success
-- Host CPU features:
--   3DNOW not supported
--   3DNOWEXT not supported
--   ABM not supported
--   ADX not supported
--   AES supported
--   AVX supported
--   AVX2 supported
--   AVX512CD not supported
--   AVX512F not supported
--   AVX512ER not supported
--   AVX512PF not supported
--   BMI1 supported
--   BMI2 supported
--   CLFSH supported
--   CMPXCHG16B supported
--   CX8 supported
--   ERMS supported
--   F16C supported
--   FMA supported
--   FSGSBASE supported
--   FXSR supported
--   HLE not supported
--   INVPCID supported
--   LAHF supported
--   LZCNT supported
--   MMX supported
--   MMXEXT not supported
--   MONITOR not supported
--   MOVBE supported
--   MSR supported
--   OSXSAVE supported
--   PCLMULQDQ supported
--   POPCNT supported
--   PREFETCHWT1 not supported
--   RDRAND supported
--   RDSEED not supported
--   RDTSCP supported
--   RTM not supported
--   SEP supported
--   SHA not supported
--   SSE supported
--   SSE2 supported
--   SSE3 supported
--   SSE4.1 supported
--   SSE4.2 supported
--   SSE4a not supported
--   SSSE3 supported
--   SYSCALL supported
--   TBM not supported
--   XOP not supported
--   XSAVE supported
-- TBB include: /opt/intel/openvino_2019.3.376/deployment_tools/inference_engine/external/tbb/include
-- TBB Release lib: /opt/intel/openvino_2019.3.376/deployment_tools/inference_engine/external/tbb/lib/libtbb.so
-- TBB Debug lib: /opt/intel/openvino_2019.3.376/deployment_tools/inference_engine/external/tbb/lib/libtbb_debug.so
-- Looking for pthread.h
-- Looking for pthread.h - found
-- Looking for pthread_create
-- Looking for pthread_create - not found
-- Looking for pthread_create in pthreads
-- Looking for pthread_create in pthreads - not found
-- Looking for pthread_create in pthread
-- Looking for pthread_create in pthread - found
-- Found Threads: TRUE  
CMake Warning (dev) in CMakeLists.txt:
  No cmake_minimum_required command is present.  A line of code such as

    cmake_minimum_required(VERSION 3.5)

  should be added at the top of the file.  The version specified may be lower
  if you wish to support older CMake versions for this project.  For more
  information run "cmake --help-policy CMP0000".
This warning is for project developers.  Use -Wno-dev to suppress it.

-- Configuring done
CMake Warning (dev) at CMakeLists.txt:56 (add_library):
  Policy CMP0003 should be set before this line.  Add code such as

    if(COMMAND cmake_policy)
      cmake_policy(SET CMP0003 NEW)
    endif(COMMAND cmake_policy)

  as early as possible but after the most recent call to
  cmake_minimum_required or cmake_policy(VERSION).  This warning appears
  because target "cosh_cpu_extension" links to some libraries for which the
  linker must search:

    tbb, dl

  and other libraries with known full path:

    /opt/intel/openvino_2019.3.376/deployment_tools/inference_engine/lib/intel64/libinference_engine.so

  CMake is adding directories in the second list to the linker search path in
  case they are needed to find libraries from the first list (for backwards
  compatibility with CMake 2.4).  Set policy CMP0003 to OLD or NEW to enable
  or disable this behavior explicitly.  Run "cmake --help-policy CMP0003" for
  more information.
This warning is for project developers.  Use -Wno-dev to suppress it.

-- Generating done
-- Build files have been written to: /home/workspace/cl_tutorial/cl_cosh/user_ie_extensions/cpu/build
(venv) root@36830e842745:/home/workspace/cl_tutorial/cl_cosh/user_ie_extensions/cpu/build#
```

Now you finished setup for compiling.

```
# omitted ...
-- Generating done
-- Build files have been written to: /home/workspace/cl_tutorial/cl_cosh/user_ie_extensions/cpu/build
```

The CPU extension library is now ready to be compiled. Compile the library using the command:

```
# make -j $(nproc)
```

> `make -j $(nproc)` - Specifies  the number of jobs (commands) to run simultaneously. The `$(nproc)` returns the number of CPU cores/threads available.  
> Reference: [make(1) - Linux man page](https://linux.die.net/man/1/make)

log

```
(venv) root@36830e842745:/home/workspace/cl_tutorial/cl_cosh/user_ie_extensions/cpu/build#
(venv) root@36830e842745:/home/workspace/cl_tutorial/cl_cosh/user_ie_extensions/cpu/build# make -j $(nproc)
Scanning dependencies of target cosh_cpu_extension
[ 16%] Building CXX object CMakeFiles/cosh_cpu_extension.dir/ext_base.o
[ 33%] Building CXX object CMakeFiles/cosh_cpu_extension.dir/.ipynb_checkpoints/ext_cosh-checkpoint.o
[ 50%] Building CXX object CMakeFiles/cosh_cpu_extension.dir/CMakeFiles/3.5.1/CompilerIdCXX/CMakeCXXCompilerId.o
[ 66%] Building CXX object CMakeFiles/cosh_cpu_extension.dir/ext_list.o
[ 83%] Building CXX object CMakeFiles/cosh_cpu_extension.dir/ext_cosh.o
[100%] Linking CXX shared library libcosh_cpu_extension.so
[100%] Built target cosh_cpu_extension
(venv) root@36830e842745:/home/workspace/cl_tutorial/cl_cosh/user_ie_extensions/cpu/build#
```

Now it is compiled.

</details>

{::options parse_block_html="false" /}

### Execute the Model with the Custom Layer

To start on a C++ sample, we first need to build the C++ samples for use with the Inference Engine:

```
# cd /opt/intel/openvino/deployment_tools/inference_engine/samples/
# ./build_samples.sh
```

> `cd /opt/intel/openvino/deployment_tools/inference_engine/samples/` ^ change directory to sample.
>
> `./build_samples.sh` - run shell script.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">log</summary>

```
(venv) root@36830e842745:/home/workspace/cl_tutorial/cl_cosh/user_ie_extensions/cpu/build# cd /opt/intel/openvino/deployment_tools/inference_engine/samples/
(venv) root@36830e842745:/opt/intel/openvino/deployment_tools/inference_engine/samples# ./build_samples.sh

Setting environment variables for building samples...
[setupvars.sh] OpenVINO environment initialized
-- The C compiler identification is GNU 7.4.0
-- The CXX compiler identification is GNU 7.4.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Looking for C++ include unistd.h
-- Looking for C++ include unistd.h - found
-- Looking for C++ include stdint.h
-- Looking for C++ include stdint.h - found
-- Looking for C++ include sys/types.h
-- Looking for C++ include sys/types.h - found
-- Looking for C++ include fnmatch.h
-- Looking for C++ include fnmatch.h - found
-- Looking for C++ include stddef.h
-- Looking for C++ include stddef.h - found
-- Check size of uint32_t
-- Check size of uint32_t - done
-- Looking for strtoll
-- Looking for strtoll - found
-- Found InferenceEngine: /opt/intel/openvino_2019.3.376/deployment_tools/inference_engine/lib/intel64/libinference_engine.so (Required is at least version "2.1")
-- Performing Test HAVE_CPUID_INFO
-- Performing Test HAVE_CPUID_INFO - Success
-- Host CPU features:
--   3DNOW not supported
--   3DNOWEXT not supported
--   ABM not supported
--   ADX not supported
--   AES supported
--   AVX supported
--   AVX2 supported
--   AVX512CD not supported
--   AVX512F not supported
--   AVX512ER not supported
--   AVX512PF not supported
--   BMI1 supported
--   BMI2 supported
--   CLFSH supported
--   CMPXCHG16B supported
--   CX8 supported
--   ERMS supported
--   F16C supported
--   FMA supported
--   FSGSBASE supported
--   FXSR supported
--   HLE not supported
--   INVPCID supported
--   LAHF supported
--   LZCNT supported
--   MMX supported
--   MMXEXT not supported
--   MONITOR not supported
--   MOVBE supported
--   MSR supported
--   OSXSAVE supported
--   PCLMULQDQ supported
--   POPCNT supported
--   PREFETCHWT1 not supported
--   RDRAND supported
--   RDSEED not supported
--   RDTSCP supported
--   RTM not supported
--   SEP supported
--   SHA not supported
--   SSE supported
--   SSE2 supported
--   SSE3 supported
--   SSE4.1 supported
--   SSE4.2 supported
--   SSE4a not supported
--   SSSE3 supported
--   SYSCALL supported
--   TBM not supported
--   XOP not supported
--   XSAVE supported
-- TBB include: /opt/intel/openvino_2019.3.376/deployment_tools/inference_engine/external/tbb/include
-- TBB Release lib: /opt/intel/openvino_2019.3.376/deployment_tools/inference_engine/external/tbb/lib/libtbb.so
-- TBB Debug lib: /opt/intel/openvino_2019.3.376/deployment_tools/inference_engine/external/tbb/lib/libtbb_debug.so
-- Looking for pthread.h
-- Looking for pthread.h - found
-- Looking for pthread_create
-- Looking for pthread_create - not found
-- Looking for pthread_create in pthreads
-- Looking for pthread_create in pthreads - not found
-- Looking for pthread_create in pthread
-- Looking for pthread_create in pthread - found
-- Found Threads: TRUE  
-- Configuring done
-- Generating done
-- Build files have been written to: /root/inference_engine_samples_build
Scanning dependencies of target format_reader
Scanning dependencies of target ie_cpu_extension
Scanning dependencies of target gflags_nothreads_static
[  1%] Building CXX object thirdparty/gflags/CMakeFiles/gflags_nothreads_static.dir/src/gflags.cc.o
[  2%] Building CXX object thirdparty/gflags/CMakeFiles/gflags_nothreads_static.dir/src/gflags_completions.cc.o
[  3%] Building CXX object thirdparty/gflags/CMakeFiles/gflags_nothreads_static.dir/src/gflags_reporting.cc.o
[  5%] Building CXX object common/format_reader/CMakeFiles/format_reader.dir/bmp.cpp.o
[  6%] Building CXX object common/format_reader/CMakeFiles/format_reader.dir/opencv_wraper.cpp.o
[  8%] Building CXX object common/format_reader/CMakeFiles/format_reader.dir/format_reader.cpp.o
[  7%] Building CXX object common/format_reader/CMakeFiles/format_reader.dir/MnistUbyte.cpp.o
[ 10%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_grn.cpp.o
[ 11%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_select.cpp.o
[ 12%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_priorbox_clustered.cpp.o
[ 14%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/common/simple_copy.cpp.o
[ 15%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_reverse_sequence.cpp.o
[ 16%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_gather_tree.cpp.o
[ 17%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_simplernms.cpp.o
[ 19%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_math.cpp.o
[ 20%] Linking CXX static library ../../intel64/Release/lib/libgflags_nothreads.a
[ 20%] Built target gflags_nothreads_static
[ 21%] Linking CXX shared library ../../intel64/Release/lib/libformat_reader.so
[ 23%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_detectionoutput_onnx.cpp.o
[ 23%] Built target format_reader
[ 24%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_pad.cpp.o
[ 25%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_fill.cpp.o
[ 26%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_proposal_onnx.cpp.o
[ 28%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_unsqueeze.cpp.o
[ 29%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_squeeze.cpp.o
[ 30%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_space_to_depth.cpp.o
[ 32%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_psroi.cpp.o
[ 33%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_resample.cpp.o
[ 34%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_scatter.cpp.o
[ 35%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_one_hot.cpp.o
[ 37%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_base.cpp.o
[ 38%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_sparse_fill_empty_rows.cpp.o
[ 39%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_roifeatureextractor_onnx.cpp.o
[ 41%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_proposal.cpp.o
[ 42%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_reduce.cpp.o
[ 43%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_list.cpp.o
[ 44%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_mvn.cpp.o
[ 46%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_shuffle_channels.cpp.o
[ 47%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_normalize.cpp.o
[ 48%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_argmax.cpp.o
[ 50%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_priorgridgenerator_onnx.cpp.o
[ 51%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_powerfile.cpp.o
[ 52%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_reorg_yolo.cpp.o
[ 53%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_detectionoutput.cpp.o
[ 55%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_log_softmax.cpp.o
[ 56%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_ctc_greedy.cpp.o
[ 57%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_interp.cpp.o
[ 58%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_topkrois_onnx.cpp.o
[ 60%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_unique.cpp.o
[ 61%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_range.cpp.o
[ 62%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_depth_to_space.cpp.o
[ 64%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_non_max_suppression.cpp.o
[ 65%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_strided_slice.cpp.o
[ 66%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_topk.cpp.o
[ 67%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_priorbox.cpp.o
[ 69%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_region_yolo.cpp.o
[ 70%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_gather.cpp.o
[ 71%] Building CXX object ie_cpu_extension/CMakeFiles/ie_cpu_extension.dir/ext_broadcast.cpp.o
[ 73%] Linking CXX shared library ../intel64/Release/lib/libcpu_extension.so
[ 73%] Built target ie_cpu_extension
Scanning dependencies of target hello_classification
Scanning dependencies of target benchmark_app
Scanning dependencies of target hello_reshape_ssd
Scanning dependencies of target hello_nv12_input_classification
Scanning dependencies of target object_detection_sample_ssd
Scanning dependencies of target classification_sample_async
Scanning dependencies of target style_transfer_sample
Scanning dependencies of target speech_sample
[ 74%] Building CXX object speech_sample/CMakeFiles/speech_sample.dir/main.cpp.o
[ 75%] Building CXX object hello_nv12_input_classification/CMakeFiles/hello_nv12_input_classification.dir/main.cpp.o
[ 76%] Building CXX object classification_sample_async/CMakeFiles/classification_sample_async.dir/main.cpp.o
[ 78%] Building CXX object object_detection_sample_ssd/CMakeFiles/object_detection_sample_ssd.dir/main.cpp.o
[ 79%] Building CXX object style_transfer_sample/CMakeFiles/style_transfer_sample.dir/main.cpp.o
[ 80%] Building CXX object benchmark_app/CMakeFiles/benchmark_app.dir/statistics_report.cpp.o
[ 82%] Building CXX object hello_reshape_ssd/CMakeFiles/hello_reshape_ssd.dir/main.cpp.o
[ 83%] Building CXX object hello_classification/CMakeFiles/hello_classification.dir/main.cpp.o
[ 84%] Building CXX object benchmark_app/CMakeFiles/benchmark_app.dir/inputs_filling.cpp.o
[ 85%] Linking CXX executable ../intel64/Release/style_transfer_sample
[ 85%] Built target style_transfer_sample
Scanning dependencies of target hello_query_device
[ 87%] Building CXX object hello_query_device/CMakeFiles/hello_query_device.dir/main.cpp.o
[ 88%] Linking CXX executable ../intel64/Release/hello_nv12_input_classification
[ 89%] Linking CXX executable ../intel64/Release/object_detection_sample_ssd
[ 89%] Built target hello_nv12_input_classification
[ 91%] Building CXX object benchmark_app/CMakeFiles/benchmark_app.dir/main.cpp.o
[ 91%] Built target object_detection_sample_ssd
[ 92%] Building CXX object benchmark_app/CMakeFiles/benchmark_app.dir/utils.cpp.o
[ 93%] Linking CXX executable ../intel64/Release/classification_sample_async
[ 93%] Built target classification_sample_async
[ 94%] Linking CXX executable ../intel64/Release/speech_sample
[ 94%] Built target speech_sample
[ 96%] Linking CXX executable ../intel64/Release/hello_reshape_ssd
[ 97%] Linking CXX executable ../intel64/Release/hello_classification
[ 97%] Built target hello_reshape_ssd
[ 97%] Built target hello_classification
[ 98%] Linking CXX executable ../intel64/Release/hello_query_device
[ 98%] Built target hello_query_device
[100%] Linking CXX executable ../intel64/Release/benchmark_app
[100%] Built target benchmark_app
Scanning dependencies of target ie_samples
[100%] Built target ie_samples

Build completed, you can find binaries for all samples in the /root/inference_engine_samples_build/intel64/Release subfolder.

(venv) root@36830e842745:/opt/intel/openvino/deployment_tools/inference_engine/samples#
```

</details>

{::options parse_block_html="false" /}

Next, we will try running the C++ sample without including the cosh extension library to see the error describing the unsupported cosh operation using the command:

```
# ~/inference_engine_samples_build/intel64/Release/classification_sample_async \
  -i $CLT/pics/dog.bmp \
  -m $CLWS/cl_ext_cosh/model.ckpt.xml \
  -d CPU
```

> `~/inference_engine_samples_build/intel64/Release/classification_sample_async` - Run sample inference engine.
>
> `-i $CLT/pics/dog.bmp` - The path to a folder with images or path to an image files
>
> `-m $CLWS/cl_ext_cosh/model.ckpt.xml` - The path to an .xml file with a trained model.
>
> `-d CPU` - Specify the target device to infer on (the list of available devices is shown below).

{::options parse_block_html="true" /}

<details>
<summary markdown="span">log</summary>

```
(venv) root@36830e842745:/opt/intel/openvino/deployment_tools/inference_engine/samples# ~/inference_engine_samples_build/intel64/Release/classification_sample_async \
>   -i $CLT/pics/dog.bmp \
>   -m $CLWS/cl_ext_cosh/model.ckpt.xml \
>   -d CPU
[ INFO ] InferenceEngine:
        API version ............ 2.1
        Build .................. custom_releases/2019/R3_ac8584cb714a697a12f1f30b7a3b78a5b9ac5e05
        Description ....... API
[ INFO ] Parsing input parameters
[ INFO ] Parsing input parameters
[ INFO ] Files were added: 1
[ INFO ]     /home/workspace/cl_tutorial/OpenVINO-Custom-Layers/pics/dog.bmp
[ INFO ] Creating Inference Engine
        CPU
        MKLDNNPlugin version ......... 2.1
        Build ........... 32974

[ INFO ] Loading network files
[ INFO ] Preparing input blobs
[ WARNING ] Image is resized from (500, 355) to (128, 128)
[ INFO ] Batch size is 1
[ INFO ] Loading model to the device
[ ERROR ] Unsupported primitive of type: cosh name: ModCosh/cosh/Cosh
(venv) root@36830e842745:/opt/intel/openvino/deployment_tools/inference_engine/samples#
```

</details>

{::options parse_block_html="false" /}

You see the expected error.

```
# omitted ...
[ ERROR ] Unsupported primitive of type: cosh name: ModCosh/cosh/Cosh
```

We will now run the command again, this time with the cosh extension library specified using the `-l $CLWS/cl_cosh/user_ie_extensions/cpu/build/libcosh_cpu_extension.so` option.

```
# ~/inference_engine_samples_build/intel64/Release/classification_sample_async \
  -i $CLT/pics/dog.bmp \
  -m $CLWS/cl_ext_cosh/model.ckpt.xml \
  -d CPU \
  -l $CLWS/cl_cosh/user_ie_extensions/cpu/build/libcosh_cpu_extension.so
```

{::options parse_block_html="true" /}

<details>
<summary markdown="span">log</summary>

```
(venv) root@36830e842745:/opt/intel/openvino/deployment_tools/inference_engine/samples# ~/inference_engine_samples_build/intel64/Release/classification_sample_async \
>   -i $CLT/pics/dog.bmp \
>   -m $CLWS/cl_ext_cosh/model.ckpt.xml \
>   -d CPU \
>   -l $CLWS/cl_cosh/user_ie_extensions/cpu/build/libcosh_cpu_extension.so
[ INFO ] InferenceEngine:
        API version ............ 2.1
        Build .................. custom_releases/2019/R3_ac8584cb714a697a12f1f30b7a3b78a5b9ac5e05
        Description ....... API
[ INFO ] Parsing input parameters
[ INFO ] Parsing input parameters
[ INFO ] Files were added: 1
[ INFO ]     /home/workspace/cl_tutorial/OpenVINO-Custom-Layers/pics/dog.bmp
[ INFO ] Creating Inference Engine
[ INFO ] CPU Extension loaded: /home/workspace/cl_tutorial/cl_cosh/user_ie_extensions/cpu/build/libcosh_cpu_extension.so
        CPU
        MKLDNNPlugin version ......... 2.1
        Build ........... 32974

[ INFO ] Loading network files
[ INFO ] Preparing input blobs
[ WARNING ] Image is resized from (500, 355) to (128, 128)
[ INFO ] Batch size is 1
[ INFO ] Loading model to the device
[ INFO ] Create infer request
[ INFO ] Start inference (10 asynchronous executions)
[ INFO ] Completed 1 async request execution
[ INFO ] Completed 2 async request execution
[ INFO ] Completed 3 async request execution
[ INFO ] Completed 4 async request execution
[ INFO ] Completed 5 async request execution
[ INFO ] Completed 6 async request execution
[ INFO ] Completed 7 async request execution
[ INFO ] Completed 8 async request execution
[ INFO ] Completed 9 async request execution
[ INFO ] Completed 10 async request execution
[ INFO ] Processing output blobs
[ WARNING ] -nt 10 is not available for this network (-nt should be less than 3 and more than 0)
            will be used maximal value : 2

Top 2 results:

Image /home/workspace/cl_tutorial/OpenVINO-Custom-Layers/pics/dog.bmp

classid probability
------- -----------
0       0.8661612  
1       0.1338388  

[ INFO ] Execution successful

[ INFO ] This sample is an API example, for any performance measurements please use the dedicated benchmark_app tool
Segmentation fault (core dumped)
(venv) root@36830e842745:/opt/intel/openvino/deployment_tools/inference_engine/samples#
```

</details>

{::options parse_block_html="false" /}

For Python, we will try running the Python sample without including the cosh extension library to see the error describing the unsupported cosh operation using the command:

```
# python /opt/intel/openvino/deployment_tools/inference_engine/samples/python_samples/classification_sample_async/classification_sample_async.py \
-i $CLT/pics/dog.bmp \
-m $CLWS/cl_ext_cosh/model.ckpt.xml \
-d CPU
```

{::options parse_block_html="true" /}

<details>
<summary markdown="span">log</summary>

```
(venv) root@36830e842745:/opt/intel/openvino/deployment_tools/inference_engine/samples# python /opt/intel/openvino/deployment_tools/inference_engine/samples/python_samples/classification_sample_async/classification_sample_async.py \
> -i $CLT/pics/dog.bmp \
> -m $CLWS/cl_ext_cosh/model.ckpt.xml \
> -d CPU
[ INFO ] Creating Inference Engine
[ INFO ] Loading network files:
        /home/workspace/cl_tutorial/cl_ext_cosh/model.ckpt.xml
        /home/workspace/cl_tutorial/cl_ext_cosh/model.ckpt.bin
[ ERROR ] Following layers are not supported by the plugin for specified device CPU:
 ModCosh/cosh/Cosh, ModCosh/cosh_1/Cosh, ModCosh/cosh_2/Cosh
[ ERROR ] Please try to specify cpu extensions library path in sample's command line parameters using -l or --cpu_extension command line argument
(venv) root@36830e842745:/opt/intel/openvino/deployment_tools/inference_engine/samples#
```

</details>

{::options parse_block_html="false" /}

There is an error about un-supported layer, cosh.

```
# omitted ...
[ ERROR ] Following layers are not supported by the plugin for specified device CPU:
 ModCosh/cosh/Cosh, ModCosh/cosh_1/Cosh, ModCosh/cosh_2/Cosh
[ ERROR ] Please try to specify cpu extensions library path in sample's command line parameters using -l or --cpu_extension command line argument
```

We will now run the command again, this time with the cosh extension library specified using the -l $CLWS/cl_cosh/user_ie_extensions/cpu/build/libcosh_cpu_extension.so option in the command:

```
# python /opt/intel/openvino/deployment_tools/inference_engine/samples/python_samples/classification_sample_async/classification_sample_async.py \
-i $CLT/pics/dog.bmp \
-m $CLWS/cl_ext_cosh/model.ckpt.xml \
-l $CLWS/cl_cosh/user_ie_extensions/cpu/build/libcosh_cpu_extension.so \
-d CPU
```

{::options parse_block_html="true" /}

<details>
<summary markdown="span">log</summary>

```
(venv) root@36830e842745:/opt/intel/openvino/deployment_tools/inference_engine/samples# python /opt/intel/openvino/deployment_tools/inference_engine/samples/python_samples/classification_sample_async/classification_sample_async.py \
> -i $CLT/pics/dog.bmp \
> -m $CLWS/cl_ext_cosh/model.ckpt.xml \
> -l $CLWS/cl_cosh/user_ie_extensions/cpu/build/libcosh_cpu_extension.so \
> -d CPU
[ INFO ] Creating Inference Engine
[ INFO ] Loading network files:
        /home/workspace/cl_tutorial/cl_ext_cosh/model.ckpt.xml
        /home/workspace/cl_tutorial/cl_ext_cosh/model.ckpt.bin
[ INFO ] Preparing input blobs
[ WARNING ] Image /home/workspace/cl_tutorial/OpenVINO-Custom-Layers/pics/dog.bmp is resized from (355, 500) to (128, 128)
[ INFO ] Batch size is 1
[ INFO ] Loading model to the plugin
[ INFO ] Start inference (10 Synchronous executions)
[ INFO ] Completed 1 Sync request execution
[ INFO ] Completed 2 Sync request execution
[ INFO ] Completed 3 Sync request execution
[ INFO ] Completed 4 Sync request execution
[ INFO ] Completed 5 Sync request execution
[ INFO ] Completed 6 Sync request execution
[ INFO ] Completed 7 Sync request execution
[ INFO ] Completed 8 Sync request execution
[ INFO ] Completed 9 Sync request execution
[ INFO ] Completed 10 Sync request execution
[ INFO ] Processing output blob
[ INFO ] Top 10 results:
Image /home/workspace/cl_tutorial/OpenVINO-Custom-Layers/pics/dog.bmp

classid probability
------- -----------
   0      0.8661612
   1     0.1338388


[ INFO ] This sample is an API example, for any performance measurements please use the dedicated benchmark_app tool

(venv) root@36830e842745:/opt/intel/openvino/deployment_tools/inference_engine/samples#
```

</details>

{::options parse_block_html="false" /}

Congratulations! You have now implemented a custom layer with the Intel® Distribution of OpenVINO™ Toolkit.

# Lesson 4: The Inference Engine

You will do the following things:

- Feeding an Intermediate Representation to the Inference Engine
- Making Inference Requests
- Integrating the Inference Model into an App

## Exercise: Feed an IR to the Inference Engine

Make sure to click the `SOURCE ENV` button before you get started to source the correct environment.

<details>
<summary>log</summary>

<pre>
(venv) root@80fe8c3d1c8f:/home/workspace# source /opt/intel/openvino/bin/setupvars.sh -pyver 3.5
python_version = 3.5
[setupvars.sh] OpenVINO environment initialized
(venv) root@80fe8c3d1c8f:/home/workspace#
</pre>
</details>

Here, using the Python wrapper, practice to feed the different Intermediate Representation (IR) models to the Inference Engine.

The frist TODO is to import the Python wrapper for the Inference Engine (IE).

```
import argparse
### TODO: Load the necessary libraries
# omitted ...
```

> `import argparse` - import the `argparse` module to write user-friendly command-line interfaces more easily.  
> Reference: [argparse](https://docs.python.org/3/library/argparse.html)

You know that "To load an IR into the Inference Engine, you’ll mostly work with two classes in the `openvino.inference_engine` library (if using Python)" on the [4. Using the Inference Engine with an IR](https://classroom.udacity.com/nanodegrees/nd132/parts/3eafdf71-b35c-4525-9b2c-d46f7dc300aa/modules/cc8ef708-33e0-472b-a8d6-ed66b8e6f678/lessons/b2518992-e7c3-4c22-9790-f0c237fc14ce/concepts/50148649-f984-48f1-ab19-06dabb979e4b).

So import `IECore` and `IENetwork` from `openvino.inference_engine` library.

```
import argparse
from openvino.inference_engine import IENetwork, IECore

# omitted ...
```

There is a CPU extension location variable for the CPU on this workspace.

```
# omitted ...
CPU_EXTENSION = "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"
# omitted ...
```

> `CPU_EXTENSION = "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"` - Defines `CPU_EXTENSION` variable and assigned string `"/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"`.

The next few lines are about creating a command line interface using `argparse` library. You can igore the details but read comments.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">More Detail for get_args Function</summary>

This is the first step in using the argparse is creating an ArgumentParser object.

```
def get_args():
    '''
    Gets the arguments from the command line.
    '''
    parser = argparse.ArgumentParser("Load an IR into the Inference Engine")

# omitted ...
```

> `def get_args():` - Defines the function called `get_args`, which will call on main method and return an object with attributes for arguments.
>
> `parser = argparse.ArgumentParser("Load an IR into the Inference Engine")` - The `argparse.ArgumentParser` creates the object of ArgumentParser class. The ArgumentParser object will hold all the information necessary to parse the command line into Python data types.   
> "Load an IR into the Inference Engine" string value is passed in for description to display before the argument help. It shows like this:  
> Reference: [Create object from class in separate file](https://stackoverflow.com/a/23238374)

log
```
(venv) root@824c9f4fd61c:/home/workspace# python feed_network.py -h
usage: Load an IR into the Inference Engine [-h] [-m M]

optional arguments:
  -h, --help  show this help message and exit
  -m M        The location of the model XML file
(venv) root@824c9f4fd61c:/home/workspace#
```

Before creating each arguments, it prepare the descriptions with string values.

```
    # -- Create the descriptions for the commands
    m_desc = "The location of the model XML file"
```

> `m_desc = "The location of the model XML file"` - simply the variable, `m_desc` has `"The location of the model XML file"` string value.

The argument, "-m" is defined here with two parameters.

```
    # -- Create the arguments
    parser.add_argument("-m", help=m_desc)
    args = parser.parse_args()

    return args
```

> `parser.add_argument("-m", help=m_desc)` - For the "-m" argument, adding `m_desc` variable as a brief description of what the argument does in `help=i_desc`.
>
> `args = parser.parse_args()` - It parses arguments ("-h" when executing `python app.py -h`) through the `parse_args()` method. This will inspect the command line, convert each argument to the appropriate type and then invoke the appropriate action. And take the strings on the command line and turn them into objects.  
> Reference: [Parsing a Command Line](https://pymotw.com/2/argparse/#parsing-a-command-line)
>
> `return args` - return args object with parsed arguments.

</details>

{::options parse_block_html="false" /}

The next function, `load_to_IE` has one `model_xml` argument. The first TODO is to load the Inference Engine API, IECore here.

```
def load_to_IE(model_xml):
    ### TODO: Load the Inference Engine API
    ie = IECore()
```

> `def load_to_IE(model_xml):` - Defines load_to_IE function has model xml file.
>
> `ie = IECore()` - initialized the Python wrapper to work with the Inference Engine and assigned it to `ie` variable.
> Reference: [ie_api.IECore Class Reference](https://docs.openvinotoolkit.org/latest/classie__api_1_1IECore.html#aa367dbd9efe19543661bc96877a7d6c5)

To add an Intermediate Representation (IR) using IENetwork, we need to load arguments named `model` and `weights` to initialize - the XML and Binary files that make up the model’s IR. we need manipulate the path for xml and bin.

Reference: [ie_api.IENetwork Class Reference](https://docs.openvinotoolkit.org/latest/classie__api_1_1IENetwork.html)

```
    ### TODO: Load IR files into their related class
    model_bin = os.path.splitext(model_xml)[0] + ".bin"
    net = IENetwork(model_xml, model_bin)
```

> `model_bin = os.path.splitext(model_xml)[0] + ".bin"` - `os.path.splittext(model_xml)` will split the `model_xml` path into a tuple (root, ext) that represents root (e.g. `/home/workspace/models/human-pose-estimation-0001`) and ext (e.g. `.xml`) part of the path name, such that root + ext == path.  
> Reference: [os.path.splitext(path)](https://docs.python.org/3.5/library/os.path.html#os.path.splitext)  
> `os.path.splitext(model_xml)[0]` Selecting element at index 0 of the tuple is root part and concatenate `.bin` to it. (e.g. `/home/workspace/models/human-pose-estimation-0001.bin`) for feeding model file (.xml) and weights file (.bin) to `IENetwork`.
>
> `net = IENetwork(model_xml, model_bin)` - initialize `IENetwork` with `model_xml`, model file (.xml) and `model_bin`, weights file (.bin).

add one import statement for `os` module.

```
import argparse
from openvino.inference_engine import IENetwork, IECore
import os

# omitted ...
```

The next TODO is:

```
### TODO: Add a CPU extension, if applicable. It's suggested to check
###       your code for unsupported layers for practice before
###       implementing this. Not all of the models may need it.
```

For determining if applicable for adding a CPU extension or not, we need to check if there are unsupported layers on our model.

```
### TODO: Add a CPU extension, if applicable. It's suggested to check
###       your code for unsupported layers for practice before
###       implementing this. Not all of the models may need it.
for l in net.layers.keys():
    if l not in ie.query_network(net, "CPU"):
        if CPU_EXTENSION:
            ie.add_extension(CPU_EXTENSION, "CPU")
            break
```

> `for l in net.layers.keys():` - For loop is iterating over a sequence (in this case, `net.layers.keys()`). First, `net.layers` returns dictionary that maps network layer names which have IENetLayer objects containing layer properties.  
> Reference: [Class Attributes](https://docs.openvinotoolkit.org/latest/classie__api_1_1IENetwork.html#class_attributes)  
> the `keys()` function returns keys of the dictionary, `net.layers`.
> variable `l` has a network layer name (key) for each iterating.
>
> `if l not in ie.query_network(net, "CPU"):` - if that the `l` doesn't include in `ie.query_network(net, "CPU")`, execute the next indented line, `if CPU_EXTENSION:`. The `ie.query_network(net, "CPU")` returns network layers are supported in the current configuration.  
> Reference: [query_network()](https://docs.openvinotoolkit.org/latest/classie__api_1_1IECore.html#a968255ec7d65929bbc9ebd21ab5c1317)
>
> `if CPU_EXTENSION:` - It means if `CPU_EXTENSION` exists (not the variable, `CPU_EXTENSION` length 0) , executes the next indented line, `ie.add_extension(CPU_EXTENSION, "CPU")`.
>
> `ie.add_extension(CPU_EXTENSION, "CPU")` - It loads extension library, `CPU_EXTENSION` variable to the IECore with a device name, `"CPU"`.  
> Reference: [add_extension()](https://docs.openvinotoolkit.org/latest/classie__api_1_1IECore.html#adf1cf8c8d741ece2e18fad9dbc14a076)
>
> `break` - The break statement terminates the loop containing it.  
Reference: [Python break and continue](https://www.programiz.com/python-programming/break-continue)

The next TODO is straight forward. We can use `query_network` function as well.

```
### TODO: Get the supported layers of the network
supported_layers = ie.query_network(net, "CPU")
```

> `supported_layers = ie.query_network(net, "CPU")` - It assignes network layers are supported in the current IECore to `supported_layers`.  

Again, checking any unsupported layers, letting the user know if missing, and exitting the program, if so is accomplished by very similar way we did.

```
### TODO: Check for any unsupported layers, and let the user
###       know if anything is missing. Exit the program, if so.
for l in net.layers.keys():
    if l not in ie.query_network(net, "CPU"):
        print("Unsupported layers found: {}".format(l))
        exit(1)
```

> the difference is if we found an unsupported layer (`if l not in ie.query_network(net, "CPU"):`), print the layer name. Also this time we use `exit(1)` to exit program as a error.

```
### TODO: Load the network into the Inference Engine
ie.load_network(net, "CPU")
```

> `ie.load_network(net, "CPU")` - Loads a network that was read from the Intermediate Representation (IR) to the plugin with specified device name and creates an ExecutableNetwork object of the IENetwork class.
> Reference: [load_network()](https://docs.openvinotoolkit.org/latest/classie__api_1_1IECore.html#afe73d64ddd115a41f5acc0d31031f52b)
> It creates ExecutableNetwork object, but we don't catch here.

For Running Your Implementation, Run replcing {xml-file-location}.

```
# python feed_network.py -m {xml-file-location}
```

{::options parse_block_html="true" /}

<details>
<summary markdown="span">log</summary>

For human-pose-estimation-0001

```
(venv) root@5a72e434e548:/home/workspace# python feed_network.py -m models/human-pose-estimation-0001.xml
IR successfully loaded into Inference Engine.
(venv) root@5a72e434e548:/home/workspace#
```

For text-detection-0004

```
(venv) root@5a72e434e548:/home/workspace# python feed_network.py -m models/text-detection-0004.xml
IR successfully loaded into Inference Engine.
(venv) root@5a72e434e548:/home/workspace#
```

For vehicle-attributes-recognition-barrier-0039

```
(venv) root@5a72e434e548:/home/workspace# python feed_network.py -m models/vehicle-attributes-recognition-barrier-0039.xml
IR successfully loaded into Inference Engine.
(venv) root@5a72e434e548:/home/workspace#
```
</details>

{::options parse_block_html="false" /}

<br>

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Notes for Solution: Feed an IR to the Inference Engine</summary>

One of the difference is a way to write for loop and if statement. This uses the feature called List Comprehension.

```
# omitted ...
unsupported_layers = [l for l in net.layers.keys() if l not in supported_layers]
# omitted ...
```

```
L = [mapping-expression for element in source-list if filter-expression]
```

This above list comprehension is equivalent to,

```
result = []
for element in source-list:
    if filter-expression:
        result.append(mapping-expression)
```

So the solution's list comprehension equals

```
result = []
for l in net.layers.keys():
    if l not in supported_layers:
        result.append(l)
```

The `unsupported_layers` variable has `result` list.

</details>

{::options parse_block_html="false" /}

## Exercise: Inference Requests

Make sure to click the `SOURCE ENV` button before you get started to source the correct environment.

<details>
<summary>log</summary>

<pre>
root@cfe5ab65a194:/home/workspace# source /opt/intel/openvino/bin/setupvars.sh -pyver 3.5
python_version = 3.5
[setupvars.sh] OpenVINO environment initialized
(venv) root@cfe5ab65a194:/home/workspace#
</pre>
</details>

In this exercise, you practice with synchronous and asynchronous requests with the Inference Engine.

About exercise's progress, we can check using `test.py`. Run first `python test.py`. Now obviously will fail all tests.

```
(venv) root@cfe5ab65a194:/home/workspace# python test.py
Synchronous Inference failed for POSE Model.
Asynchronous Inference failed for POSE Model.
Synchronous Inference failed for TEXT Model.
Asynchronous Inference failed for TEXT Model.
Synchronous Inference failed for CAR META Model.
Asynchronous Inference failed for CAR META Model.
You passed 0 of 6 tests.
See above for additional feedback.
(venv) root@cfe5ab65a194:/home/workspace#
```

In the import section, there are helpers for loading the IR into the Inference Engine as we did privious and preprocessing the input images.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">More Detail for Export</summary>

```
import argparse
import cv2
from helpers import load_to_IE, preprocessing
# omitted ...
```

> `import argparse` - import the `argparse` module to write user-friendly command-line interfaces more easily.  
> Reference: [argparse](https://docs.python.org/3/library/argparse.html)
>
> `import cv2` - import statement to use the OpenCV package in code  
> [OpenCV Tutorial: A Guide to Learn OpenCV](https://www.pyimagesearch.com/2018/07/19/opencv-tutorial-a-guide-to-learn-opencv/)

the `helpers` comes from your current directory and import `load_to_IE` and `preprocessing` functions.
Check using `ls -l`

```
(venv) root@cfe5ab65a194:/home/workspace# ls -l
total 104
-rw-r--r-- 1 root root 68036 Feb  1 03:13 Guide.ipynb
-rw-r--r-- 1 root root  1836 Dec 12 23:48 helpers.py
drwxr-xr-x 2 root root  4096 Dec 12 23:48 images
-rw-r--r-- 1 root root  2271 Dec 12 23:48 inference.py
drwxr-xr-x 2 root root  4096 Dec 12 23:48 models
drwxr-xr-x 2 root root  4096 Feb  1 03:18 __pycache__
-rw-r--r-- 1 root root  1056 Dec 12 23:48 README.md
drwxr-xr-x 2 root root  4096 Dec 12 23:48 solution
-rw-r--r-- 1 root root  2843 Dec 12 23:48 test.py
(venv) root@cfe5ab65a194:/home/workspace#
```

</details>

{::options parse_block_html="false" /}

The global variable called `CPU_EXTENSION` is defined for unsupported layers on inference engine.  
Reference: [Global Variables](https://www.w3schools.com/python/python_variables.asp)

You may already know the `get_args()` function defined on the next few lines.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">More Detail for get_args Function</summary>

This is the first step in using the argparse is creating an ArgumentParser object.

```
def get_args():
    '''
    Gets the arguments from the command line.
    '''
    parser = argparse.ArgumentParser("Load an IR into the Inference Engine")

# omitted ...
```

> `def get_args():` - Defines the function called `get_args`, which will call on main method and return an object with attributes for arguments.
>
> `parser = argparse.ArgumentParser("Load an IR into the Inference Engine")` - The `argparse.ArgumentParser` creates the object of ArgumentParser class. The ArgumentParser object will hold all the information necessary to parse the command line into Python data types.   
> "Load an IR into the Inference Engine" string value is passed in for description to display before the argument help. It shows like this:  
> Reference: [Create object from class in separate file](https://stackoverflow.com/a/23238374)

log
```
(venv) root@cfe5ab65a194:/home/workspace# python inference.py -h
usage: Load an IR into the Inference Engine [-h] [-m M] [-i I] [-r R]

optional arguments:
  -h, --help  show this help message and exit
  -m M        The location of the model XML file
  -i I        The location of the image input
  -r R        The location of the image input
(venv) root@cfe5ab65a194:/home/workspace#
```

Before creating each arguments, it prepare the descriptions with string values.

```
    # -- Create the descriptions for the commands
    m_desc = "The location of the model XML file"
    i_desc = "The location of the image input"
    r_desc = "The type of inference request: Async ('A') or Sync ('S')"
```

> `m_desc = "The location of the model XML file"` - simply the variable, `m_desc` has `"The location of the model XML file"` string value and two other things are also almost same.

The argument, `-m`, `-i`, and `-r` is defined here with two parameters.

```
    # -- Create the arguments
    parser.add_argument("-m", help=m_desc)
    parser.add_argument("-i", help=i_desc)
    parser.add_argument("-r", help=i_desc)
    args = parser.parse_args()

    return args
```

> `parser.add_argument("-m", help=m_desc)` - For the "-m" argument, adding `m_desc` variable as a brief description of what the argument does in `help=i_desc`.
>
> `args = parser.parse_args()` - It parses arguments ("-h" when executing `python app.py -h`) through the `parse_args()` method. This will inspect the command line, convert each argument to the appropriate type and then invoke the appropriate action. And take the strings on the command line and turn them into objects.  
> Reference: [Parsing a Command Line](https://pymotw.com/2/argparse/#parsing-a-command-line)
>
> `return args` - return args object with parsed arguments.

</details>

{::options parse_block_html="false" /}

The first TODO is implementing `async_inference`. Before implementing functions, we need to know about the parameters, `exec_net`, `input_blob` and `image`.

```
def async_inference(exec_net, input_blob, image):
# omitted ...
```

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Where are the parameters comes from?</summary>

The argument is `exec_net` which we can assume an ExecutableNetwork. As you can see, the `exec_net` is the output of `load_to_IE` function.

```
# omitted ...
def main():
    args = get_args()
    exec_net, input_shape = load_to_IE(args.m, CPU_EXTENSION)
    perform_inference(exec_net, args.r, args.i, input_shape)
# omitted ...
```

On the `load_to_IE` function, eventually the `plugin.load_network` function returns `exec_net`, when it loads the network into the Inference Engine, `plugin` variable which initialized as `IECore`. Then this `load_network()` returns An `ExecutableNetwork` object.
Reference: [load_network()](https://docs.openvinotoolkit.org/latest/classie__api_1_1IECore.html#afe73d64ddd115a41f5acc0d31031f52b)

```
# omitted ...

# Load the Inference Engine API
plugin = IECore()

# omitted ...

# Load the network into the Inference Engine
exec_net = plugin.load_network(net, "CPU")

# omitted ...
```

The next argument is `input_blob`. It is a little bit tricky. This comes from inside `perform_inference` function.

```
# Get the input blob for the inference request
input_blob = next(iter(exec_net.inputs))
```

> `next(iter(exec_net.inputs))` - Get the first element of `exec_net.inputs`. `iter` function returns an object which can be iterated one element at a time.  
> Reference: [Python iter()](https://www.programiz.com/python-programming/methods/built-in/iter)  
> The `next` function is often used with iterater object to get the next element.  
> Reference: [next(iterator\[, default\])](https://docs.python.org/3/library/functions.html#next)

It extracts the input layer name. For example, you can check the name by printing.
Add on `perform_inference` function.

```
# omitted ...
# Get the input blob for the inference request
input_blob = next(iter(exec_net.inputs))
print(exec_net.inputs)
exit(1)
# omitted ...
```

Using test.py, you can test various model with `python test.py` which is for Inference request.

```
(venv) root@cfe5ab65a194:/home/workspace# python test.py
dict_keys(['data'])
Synchronous Inference failed for POSE Model.
dict_keys(['data'])
Asynchronous Inference failed for POSE Model.
dict_keys(['Placeholder'])
Synchronous Inference failed for TEXT Model.
dict_keys(['Placeholder'])
Asynchronous Inference failed for TEXT Model.
dict_keys(['input'])
Synchronous Inference failed for CAR META Model.
dict_keys(['input'])
Asynchronous Inference failed for CAR META Model.
You passed 0 of 6 tests.
See above for additional feedback.
(venv) root@cfe5ab65a194:/home/workspace#
```

You understand that `exec_net.inputs` is the keys of dictionary data type and each model has their own only one input layer name.

The final parameter is straight forward. The `image` is the output of `preprocessing` function.

```
# Preprocess it (applies for the IRs from the Pre-Trained Models lesson)
preprocessed_image = preprocessing(image, h, w)
```

we preprocess the input images to fit each requirements of the models.

</details>

{::options parse_block_html="false" /}

With an `ExecutableNetwork`, asynchronous requests begin with `start_async`, and then you can `wait` until the request is complete.

```
def async_inference(exec_net, input_blob, image):
    ### TODO: Add code to perform asynchronous inference
    ### Note: Return the exec_net
    infer_request = exec_net.start_async(0, {input_blob: image})

    infer_request.wait()

    responce = infer_request.outputs

    return exec_net
```

> `infer_request = exec_net.start_async(0, {input_blob: image})` - Using `exec_net` (ExecutableNetwork), start asynchronous inference request with `start_async` function. The first argument is hard-coded 0 which means an index of infer request to start inference because there is no more other request. As the input for the models, the dictionary, `{input_blob: image}` that maps input layer name, `input_blob` variable to `numpy.ndarray` object of proper shape with input data for the layer, `image`.  
> The return value, assigned `infer_request` variable is a handler of this asynchronous inference request, which is an instance of the `InferRequest` class.  
> Reference: [start_async()](https://docs.openvinotoolkit.org/latest/classie__api_1_1ExecutableNetwork.html#a314107a6b50f0ebf65751569973c760a)
>
> `infer_request.wait()` - The `wait` function literally waits until inference result becomes available by default.  
> Reference: [wait()](https://docs.openvinotoolkit.org/latest/classie__api_1_1InferRequest.html#a936fa50a7531e2f9a9e9c3d45afc9b43)
>
> `responce = infer_request.outputs` - After becoming available output, you can access them using `infer_request.outputs`.

Now run `python test.py` for our progress.

```
(venv) root@cfe5ab65a194:/home/workspace# python test.py
Synchronous Inference failed for POSE Model.
Synchronous Inference failed for TEXT Model.
Synchronous Inference failed for CAR META Model.
You passed 3 of 6 tests.
Congratulations!
(venv) root@cfe5ab65a194:/home/workspace#
```

Congrats! passed 3 parts about asynchronous inference of 6 tests.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Check Output of Inference Request</summary>

On implemented `async_inference` function, print the key value of the outputs.

```
# omitted ...
responce = infer_request.outputs
print(responce.keys())
# omitted ...
```

Then run `python test.py`.

```
(venv) root@cfe5ab65a194:/home/workspace# python test.py
Synchronous Inference failed for POSE Model.
dict_keys(['Mconv7_stage2_L1', 'Mconv7_stage2_L2'])
Synchronous Inference failed for TEXT Model.
dict_keys(['model/link_logits_/add', 'model/segm_logits/add'])
Synchronous Inference failed for CAR META Model.
dict_keys(['type', 'color'])
You passed 3 of 6 tests.
Congratulations!
(venv) root@cfe5ab65a194:/home/workspace#
```

Now you can see maybe familiar value you worked on Deploy Your First Edge App of the second lesson. In this exercise, it only returns `exec_net` because it is out of scope.

</details>

{::options parse_block_html="false" /}

The next TODO is creating synchronous inference request. All three parameters are the same, `exec_net`, `input_blob`, and `image`. With an `ExecutableNetwork`, synchronous requests just use the `infer` function.

```
def sync_inference(exec_net, input_blob, image):
    ### TODO: Add code to perform synchronous inference
    ### Note: Return the result of inference
    output = exec_net.infer({input_blob: image})

    return output
```

> `output = exec_net.infer({input_blob: image})` - The input parameter is the dictionary that maps input layer name, `input_blob` to the image input `numpy.ndarray` object. It returns the output dictionary that maps output layer names to numpy.ndarray objects with output data of the layer.  
> Reference: [infer()](https://docs.openvinotoolkit.org/latest/classie__api_1_1ExecutableNetwork.html#aea96e8e534c8e23d8b257bad11063519)
>
> `return output` - Return the result of inference request.

Now it is time to test again with `python test.py`.

```
(venv) root@cfe5ab65a194:/home/workspace# python test.py
You passed 6 of 6 tests.
See above for additional feedback.
(venv) root@cfe5ab65a194:/home/workspace#
```

You passed 6 of 6 tests!

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Check output</summary>

Again you can check the outputs.

```
(venv) root@cfe5ab65a194:/home/workspace# python test.py
dict_keys(['Mconv7_stage2_L1', 'Mconv7_stage2_L2'])
dict_keys(['model/link_logits_/add', 'model/segm_logits/add'])
dict_keys(['color', 'type'])
You passed 6 of 6 tests.
See above for additional feedback.
(venv) root@cfe5ab65a194:/home/workspace#
```

You can see the exact same output as we did asynchronous inference.

</details>

{::options parse_block_html="false" /}

<br>

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Notes for Solution: Feed an IR to the Inference Engine</summary>

On the Asynchronous Solution, only `exec_net.requests[0].wait(-1)` make much more sense as he suggested himself.

```
I don't actually need time.sleep() here - using the -1 with wait() is able to perform similar functionality.
```

```
while True:
    status = exec_net.requests[0].wait(-1)
    if status == 0:
        break
    else:
        time.sleep(1)
```

will replace just

```
status = exec_net.requests[0].wait(-1)
if status != 0:
    print('Something went wrong: {}'.format(status))
    exit(1)
```

For the Asynchronous Solution, we can check returned status is not error code.

Reference: [StatusCode](https://docs.openvinotoolkit.org/latest/namespaceInferenceEngine.html#a2ce897aa6a353c071958fe379f5d6421)


</details>

{::options parse_block_html="false" /}

## Exercise: Integrate into an App

Make sure to click the `SOURCE ENV` button before you get started to source the correct environment.

<details>
<summary>log</summary>

<pre>
root@30de5ec2308a:/home/workspace# source /opt/intel/openvino/bin/setupvars.sh -pyver 3.5
python_version = 3.5
[setupvars.sh] OpenVINO environment initialized
(venv) root@30de5ec2308a:/home/workspace#
</pre>
</details>

In this lesson, you will extract the results of the inference request, and then integrate the Inference Engine into an existing application with video and add extra option for various confidence thresholds with the model.

The first task is "Convert a bounding box model to an IR with the Model Optimizer.". For Object Detection, you can use the SSD MobileNet V2 COCO model from the [Object Detection Model Zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md#coco-trained-models) which we already experienced.

About the [SSD MobileNet V2 COCO model](https://github.com/opencv/open_model_zoo/blob/master/models/public/ssd_mobilenet_v2_coco/ssd_mobilenet_v2_coco.md)

```
# wget http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_coco_2018_03_29.tar.gz -P /home/workspace
```

> `wget http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_coco_2018_03_29.tar.gz -P /home/workspace` - wget is a command for downloading files from the Internet (In this case, from http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_coco_2018_03_29.tar.gz). The option `-P /home/workspace` specifies the location to store downloaded files.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">log</summary>

```
(venv) root@30de5ec2308a:/home/workspace# wget http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_coco_2018_03_29.tar.gz -P /home/workspace
--2020-02-02 04:06:47--  http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_coco_2018_03_29.tar.gz
Resolving download.tensorflow.org (download.tensorflow.org)... 74.125.129.128, 2607:f8b0:4001:c07::80
Connecting to download.tensorflow.org (download.tensorflow.org)|74.125.129.128|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 187925923 (179M) [application/x-tar]
Saving to: ‘/home/workspace/ssd_mobilenet_v2_coco_2018_03_29.tar.gz’

ssd_mobilenet_v2_c 100%[==============>] 179.22M  83.4MB/s    in 2.1s    

2020-02-02 04:06:50 (83.4 MB/s) - ‘/home/workspace/ssd_mobilenet_v2_coco_2018_03_29.tar.gz’ saved [187925923/187925923]

(venv) root@30de5ec2308a:/home/workspace#
```

you can check `ssd_mobilenet_v2_coco_2018_03_29.tar.gz` with `ls -l`.

```
(venv) root@30de5ec2308a:/home/workspace# ls -l
total 187036
-rw-r--r-- 1 root root      2579 Dec 12 23:48 app.py
-rw-r--r-- 1 root root     68036 Feb  2 03:29 Guide.ipynb
-rw-r--r-- 1 root root      2275 Dec 12 23:48 inference.py
drwxr-xr-x 2 root root      4096 Dec 12 23:48 models
-rw-r--r-- 1 root root      2422 Dec 12 23:48 README.md
drwxr-xr-x 2 root root      4096 Dec 12 23:48 solution
-rw-r--r-- 1 root root 187925923 Apr  2  2018 ssd_mobilenet_v2_coco_2018_03_29.tar.gz
-rw-r--r-- 1 root root   3306748 Dec 12 23:48 test_video.mp4
(venv) root@30de5ec2308a:/home/workspace#
```
</details>

{::options parse_block_html="false" /}

Extract the tar.gz file.

```
# tar -xvf /home/workspace/ssd_mobilenet_v2_coco_2018_03_29.tar.gz
```

> `tar -xvf ssd_mobilenet_v2_coco_2018_03_29.tar.gz` - `tar` command for handling `**.tar.gz` file.  
> `x`: Extract a tar file.  
> `v`: Verbose output or show progress while extracting files.  
> `f`: Specify an archive or a tar filename. (ssd_mobilenet_v2_coco_2018_03_29.tar.gz)

{::options parse_block_html="true" /}

<details>
<summary markdown="span">log</summary>

```
(venv) root@30de5ec2308a:/home/workspace# tar -xvf /home/workspace/ssd_mobilenet_v2_coco_2018_03_29.tar.gz
ssd_mobilenet_v2_coco_2018_03_29/checkpoint
ssd_mobilenet_v2_coco_2018_03_29/model.ckpt.meta
ssd_mobilenet_v2_coco_2018_03_29/pipeline.config
ssd_mobilenet_v2_coco_2018_03_29/saved_model/saved_model.pb
ssd_mobilenet_v2_coco_2018_03_29/frozen_inference_graph.pb
ssd_mobilenet_v2_coco_2018_03_29/saved_model/
ssd_mobilenet_v2_coco_2018_03_29/saved_model/variables/
ssd_mobilenet_v2_coco_2018_03_29/model.ckpt.index
ssd_mobilenet_v2_coco_2018_03_29/
ssd_mobilenet_v2_coco_2018_03_29/model.ckpt.data-00000-of-00001
(venv) root@30de5ec2308a:/home/workspace#
```

check one more `ssd_mobilenet_v2_coco_2018_03_29` folder created on `/home/workspace`.

```
(venv) root@30de5ec2308a:/home/workspace# ls -l
total 187040
-rw-r--r-- 1 root   root       2579 Dec 12 23:48 app.py
-rw-r--r-- 1 root   root      68036 Feb  2 03:29 Guide.ipynb
-rw-r--r-- 1 root   root       2275 Dec 12 23:48 inference.py
drwxr-xr-x 2 root   root       4096 Dec 12 23:48 models
-rw-r--r-- 1 root   root       2422 Dec 12 23:48 README.md
drwxr-xr-x 2 root   root       4096 Dec 12 23:48 solution
drwxr-xr-x 3 345018 89939      4096 Mar 30  2018 ssd_mobilenet_v2_coco_2018_03_29
-rw-r--r-- 1 root   root  187925923 Apr  2  2018 ssd_mobilenet_v2_coco_2018_03_29.tar.gz
-rw-r--r-- 1 root   root    3306748 Dec 12 23:48 test_video.mp4
(venv) root@30de5ec2308a:/home/workspace#
```

</details>

{::options parse_block_html="false" /}

Check inside of the `ssd_mobilenet_v2_coco_2018_03_29` folder using `ls -l /home/workspace/ssd_mobilenet_v2_coco_2018_03_29`.

```
(venv) root@30de5ec2308a:/home/workspace# ls -l /home/workspace/ssd_mobilenet_v2_coco_2018_03_29
total 137576
-rw-r--r-- 1 345018 89939       77 Mar 30  2018 checkpoint
-rw-r--r-- 1 345018 89939 69688296 Mar 30  2018 frozen_inference_graph.pb
-rw-r--r-- 1 345018 89939 67505156 Mar 30  2018 model.ckpt.data-00000-of-00001
-rw-r--r-- 1 345018 89939    15069 Mar 30  2018 model.ckpt.index
-rw-r--r-- 1 345018 89939  3496023 Mar 30  2018 model.ckpt.meta
-rw-r--r-- 1 345018 89939     4204 Mar 30  2018 pipeline.config
drwxr-xr-x 3 345018 89939     4096 Mar 30  2018 saved_model
(venv) root@30de5ec2308a:/home/workspace#
```

For converting this model into the Intermediate Representation (IR) for Inference Engine, run

```
# python /opt/intel/openvino/deployment_tools/model_optimizer/mo.py \
  --input_model /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/frozen_inference_graph.pb \
  --tensorflow_object_detection_api_pipeline_config /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/pipeline.config \
  --reverse_input_channels \
  --tensorflow_use_custom_operations_config /opt/intel/openvino/deployment_tools/model_optimizer/extensions/front/tf/ssd_v2_support.json
```

> `python` - `python` is specified when invoking Python
>
> `/opt/intel/openvino/deployment_tools/model_optimizer/mo_tf.py` - The path of the model converter script for the TensorFlow model.
>
> `--input_model /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/frozen_inference_graph.pb` - Option treats the input model file as a text protobuf format (in this case, `frozen_inference_graph.pb`)
>
> `--tensorflow_object_detection_api_pipeline_config /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/pipeline.config` - The path to the pipeline configuration file used to generate model created with help of Object Detection API. (which is also located in `/home/workspace/ssd_mobilenet_v2_coco_2018_03_29`) (one of the cofiguration file on TensorFlow.)
>
> `--reverse_input_channels` - revert input channels from RGB to BGR due to the TensorFlow models being trained on RGB images, but the Inference Engine otherwise defaulting to BGR.
>
> `--tensorflow_use_custom_operations_config /opt/intel/openvino/deployment_tools/model_optimizer/extensions/front/tf/ssd_v2_support.json` - use the configuration file with custom operation description.
>
> `\` backslash effectively allows the a command to span multiple lines to make it easier to read a long command.
>
> Reference: [What does this command with a backslash at the end do?](https://unix.stackexchange.com/questions/368753/what-does-this-command-with-a-backslash-at-the-end-do)

{::options parse_block_html="true" /}

<details>
<summary markdown="span">log</summary>

```
(venv) root@30de5ec2308a:/home/workspace# python /opt/intel/openvino/deployment_tools/model_optimizer/mo.py \
>   --input_model /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/frozen_inference_graph.pb \
>   --tensorflow_object_detection_api_pipeline_config /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/pipeline.config \
>   --reverse_input_channels \
>   --tensorflow_use_custom_operations_config /opt/intel/openvino/deployment_tools/model_optimizer/extensions/front/tf/ssd_v2_support.json
Model Optimizer arguments:
Common parameters:
        - Path to the Input Model:      /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/frozen_inference_graph.pb
        - Path for generated IR:        /home/workspace/.
        - IR output name:       frozen_inference_graph
        - Log level:    ERROR
        - Batch:        Not specified, inherited from the model
        - Input layers:         Not specified, inherited from the model
        - Output layers:        Not specified, inherited from the model
        - Input shapes:         Not specified, inherited from the model
        - Mean values:  Not specified
        - Scale values:         Not specified
        - Scale factor:         Not specified
        - Precision of IR:      FP32
        - Enable fusing:        True
        - Enable grouped convolutions fusing:   True
        - Move mean values to preprocess section:       False
        - Reverse input channels:       True
TensorFlow specific parameters:
        - Input model in text protobuf format:  False
        - Path to model dump for TensorBoard:   None
        - List of shared libraries with TensorFlow custom layers implementation:  None
        - Update the configuration file with input/output node names:   None
        - Use configuration file used to generate the model with Object Detection API:    /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/pipeline.config
        - Operations to offload:        None
        - Patterns to offload:  None
        - Use the config file:  /opt/intel/openvino/deployment_tools/model_optimizer/extensions/front/tf/ssd_v2_support.json
Model Optimizer version:        2019.3.0-408-gac8584cb7
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorflow/python/framework/dtypes.py:516: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint8 = np.dtype([("qint8", np.int8, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorflow/python/framework/dtypes.py:517: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint8 = np.dtype([("quint8", np.uint8, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorflow/python/framework/dtypes.py:518: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint16 = np.dtype([("qint16", np.int16, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorflow/python/framework/dtypes.py:519: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint16 = np.dtype([("quint16", np.uint16, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorflow/python/framework/dtypes.py:520: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint32 = np.dtype([("qint32", np.int32, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorflow/python/framework/dtypes.py:525: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  np_resource = np.dtype([("resource", np.ubyte, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:541: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint8 = np.dtype([("qint8", np.int8, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:542: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint8 = np.dtype([("quint8", np.uint8, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:543: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint16 = np.dtype([("qint16", np.int16, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:544: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint16 = np.dtype([("quint16", np.uint16, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:545: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint32 = np.dtype([("qint32", np.int32, 1)])
/opt/intel/openvino_2019.3.376/deployment_tools/model_optimizer/venv/lib/python3.5/site-packages/tensorboard/compat/tensorflow_stub/dtypes.py:550: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  np_resource = np.dtype([("resource", np.ubyte, 1)])
The Preprocessor block has been removed. Only nodes performing mean value subtraction and scaling (if applicable) are kept.

[ SUCCESS ] Generated IR model.
[ SUCCESS ] XML file: /home/workspace/./frozen_inference_graph.xml
[ SUCCESS ] BIN file: /home/workspace/./frozen_inference_graph.bin
[ SUCCESS ] Total execution time: 76.91 seconds.
(venv) root@30de5ec2308a:/home/workspace#
```

Check three output files on `/home/workspace`.

```
(venv) root@30de5ec2308a:/home/workspace# ls -l
total 252984
-rw-r--r-- 1 root   root       2579 Dec 12 23:48 app.py
-rw-r--r-- 1 root   root   67272876 Feb  2 04:34 frozen_inference_graph.bin
-rw-r--r-- 1 root   root      49263 Feb  2 04:34 frozen_inference_graph.mapping
-rw-r--r-- 1 root   root     112028 Feb  2 04:34 frozen_inference_graph.xml
-rw-r--r-- 1 root   root      68036 Feb  2 03:29 Guide.ipynb
-rw-r--r-- 1 root   root       2275 Dec 12 23:48 inference.py
drwxr-xr-x 2 root   root       4096 Dec 12 23:48 models
-rw-r--r-- 1 root   root       2422 Dec 12 23:48 README.md
drwxr-xr-x 2 root   root       4096 Dec 12 23:48 solution
drwxr-xr-x 3 345018 89939      4096 Mar 30  2018 ssd_mobilenet_v2_coco_2018_03_29
-rw-r--r-- 1 root   root  187925923 Apr  2  2018 ssd_mobilenet_v2_coco_2018_03_29.tar.gz
-rw-r--r-- 1 root   root    3306748 Dec 12 23:48 test_video.mp4
(venv) root@30de5ec2308a:/home/workspace#
```

</details>

{::options parse_block_html="false" /}

The Intermediate Representation (IR), `frozen_inference_graph.xml` and `frozen_inference_graph.bin` are ready for the Inference Engine.

The next task is pre-proceesing inputs. In this case, the input is a video. As you can see, there is the TODO to pre-process the frame on the `infer_on_video` function.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">More Detail for infer_on_video Function</summary>

There is two TODO which will be implemented later.

```
### TODO: Initialize the Inference Engine

### TODO: Load the network model into the IE
```

Get and open video capture using opencv.

```
# Get and open video capture
cap = cv2.VideoCapture(args.i)
cap.open(args.i)
```

> `cap = cv2.VideoCapture(args.i)` - To capture a video, the `cv2.VideoCapture(args.i)` initialized a VideoCapture object with `args.i`, the location of the input file. The `args.i` comes from the return value of `get_args` function.
>
> `cap.open(args.i)` - Open video file.
> Reference: [open()](https://docs.opencv.org/3.4/d8/dfe/classcv_1_1VideoCapture.html#ab5b7391cd5ec50e7237e575a758f6f05)

Grab the shape of the input

```
# Grab the shape of the input
width = int(cap.get(3))
height = int(cap.get(4))
```

> `width = int(cap.get(3))` - You can also access some of the features of this video using `cap.get(propId)` method where propId is a number from 0 to 18. (In this case, `3` is width of the video)
> Reference: [Capture Video from Camera](https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_gui/py_video_display/py_video_display.html)  
> The `int(...)` constructs an integer number if it the return would be a float.  
> Reference: [Specify a Variable Type](https://www.w3schools.com/python/python_casting.asp)  
>
> `height = int(cap.get(4))` - In this case, `4` is height of the video.  
> Reference: [Property Identifier](https://docs.opencv.org/2.4/modules/highgui/doc/reading_and_writing_images_and_video.html#videocapture-get)

Here is another object, `VideoWriter` is initialized.

```
# Create a video writer for the output video
# The second argument should be `cv2.VideoWriter_fourcc('M','J','P','G')`
# on Mac, and `0x00000021` on Linux
out = cv2.VideoWriter('out.mp4', 0x00000021, 30, (width,height))
```

> `out = cv2.VideoWriter('out.mp4', 0x00000021, 30, (width,height))` - Creates `VideoWriter` object with `'out.mp4'` output file name, `0x00000021` which represents the fourcc to the ASCII number directly for mp4 video codec, `30` which is framerate of the created video stream, and `(width,height)` for size of the video frames.  
> Reference: [VideoWriter()](https://docs.opencv.org/3.4/dd/d9e/classcv_1_1VideoWriter.html#ac3478f6257454209fa99249cc03a5c59)  
> Somehow need to specify the video codec using ASCII number.  
> Reference: [How to write MP4 with OpenCV3](http://xiaoxumeng.com/how-to-write-mp4-with-opencv3/)  

The next some codes is to process each frame for output.

```
# Process frames until the video ends, or process is exited
while cap.isOpened():
    # Read the next frame
    flag, frame = cap.read()
    if not flag:
        break
    key_pressed = cv2.waitKey(60)
```

> `while cap.isOpened():` - while loop executes the indented lines as long as `cap.isOpened()` is True, the video still lasts.
>
> `flag, frame = cap.read()` - Returns a bool (True/False). If frame is read correctly, it will be True and the video frame is returned here as `image`. If no frames has been grabbed the image will be empty.
> Reference: [Capture Video from Camera](https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_gui/py_video_display/py_video_display.html)
>
> `if not flag:` - if flag is False, break this while loop because there is no more frame to read.
>
> `key_pressed = cv2.waitKey(60)` - The function `waitKey` waits for a key event for 60 milliseconds in this case.
> Reference: [waitKey](https://docs.opencv.org/2.4/modules/highgui/doc/user_interface.html?highlight=waitkey#waitkey)

There is four TODOs.

```
### TODO: Pre-process the frame

### TODO: Perform inference on the frame

### TODO: Get the output of inference

### TODO: Update the frame to include detected bounding boxes
```

In the end of while part, there is a few more lines.

```
# Write out the frame
out.write(frame)
# Break if escape key pressed
if key_pressed == 27:
    break
```

> `out.write(frame)` - Writes the next video frame to output video.  
> Reference: [write()](https://docs.opencv.org/3.4/dd/d9e/classcv_1_1VideoWriter.html#a3115b679d612a6a0b5864a0c88ed4b39)
>
> `if key_pressed == 27:` - if `key_pressed` is escape key, break the while loop.  
> Reference: [ASCII Table and Description](http://www.asciitable.com)

The final part of `infer_on_video` function is closing.

```
# Release the out writer, capture, and destroy any OpenCV windows
out.release()
cap.release()
cv2.destroyAllWindows()
```

> `out.release()` - Closes the video writer  
> Reference: [release()](https://docs.opencv.org/3.4/dd/d9e/classcv_1_1VideoWriter.html#a667f737e56d5ba6b0533c6c7bf941140)
>
> `cap.release()` - Closes video file and allow OpenCV to release the captured file.  
> Reference: [release()](https://docs.opencv.org/3.4/d8/dfe/classcv_1_1VideoCapture.html#afb4ab689e553ba2c8f0fec41b9344ae6)
>
> `cv2.destroyAllWindows()` - Destroys all of the opened HighGUI windows.  
> Reference: [destroyAllWindows](https://docs.opencv.org/2.4/modules/highgui/doc/user_interface.html?highlight=destroyallwindows#destroyallwindows)

</details>

{::options parse_block_html="false" /}

For pre-processing the input video, do the same thing on lesson 2. Check the expected input shape of this model.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Check Model Input Shape</summary>

To check input shape of the model, print it using `IENetwork` class. On `load_model` function on `Network` class of `Inference.py`, add print statement.

```
# omitted ...
# Get the input layer
self.input_blob = next(iter(self.network.inputs))
self.output_blob = next(iter(self.network.outputs))

print(self.network.inputs[self.input_blob].shape)
exit(1)

return

# omitted ...
```

> `print(self.network.inputs[self.input_blob].shape)` - Refers the shape of `inputs` with the attribute, `self.input_blob` which means input layer name on the `IENetwork`, `network` variable here.

Run

```
# python app.py -m frozen_inference_graph.xml
```

log

```
(venv) root@57691ce18a6a:/home/workspace# python app.py -m frozen_inference_graph.xml
[1, 3, 300, 300]
(venv) root@57691ce18a6a:/home/workspace#
```

We can assume that `1` for batch size, `3` for color channel, `300` for height, and `300` for width as well.

To make more confidence, check the model's input on [SSD MobileNet V2 COCO model](https://github.com/opencv/open_model_zoo/blob/master/models/public/ssd_mobilenet_v2_coco/ssd_mobilenet_v2_coco.md)

Please make sure to delete them.

```
print(self.network.inputs[self.input_blob].shape)
exit(1)
```

</details>

{::options parse_block_html="false" /}

<br>

| name | B (batch size) | C (number of color channels) | H (image height) | W (image width) | color order |
|-------|----------------|------------------------|------------------|-----------------|-------------|
| image_tensor | 1 | 3 | 300 | 300 | RGB |

Check the ndarray shape information using numpy.

First thing first, import numpy as np.

```
import argparse
import cv2
from inference import Network
import numpy as np
```

Then under `### TODO: Pre-process the frame`, add print statement.

```
### TODO: Pre-process the frame
preprocessed_frame = np.copy(frame)
print(preprocessed_frame.shape)
exit(1)
```

> `preprocessed_frame = np.copy(frame)` - Copies the image, `frame` as `numpy.ndarray` which constructs a new compound object without references.
>
> `print(preprocessed_frame.shape)` - Print the shape of `preprocessed_frame`.
>
> `exit(1)` - Exits the program with in number 1 which means an error.

Run your `app.py`.

```
# python app.py -m frozen_inference_graph.xml
```

<details>
<summary>log</summary>

<pre>
(venv) root@bb6cb0771035:/home/workspace# python app.py -m frozen_inference_graph.xml
(720, 1280, 3)
(venv) root@bb6cb0771035:/home/workspace#
</pre>
</details>

We will pre-process `(720, 1280, 3)` to `(1, 3, 300, 300)`. Resize it first.

```
### TODO: Pre-process the frame
preprocessed_frame = np.copy(frame)
preprocessed_frame = cv2.resize(preprocessed_frame, (300, 300))
print(preprocessed_frame.shape)
exit(1)
```

> `preprocessed_frame = cv2.resize(preprocessed_frame, (300, 300))` - resize function of cv2 resizes the preprocessed_image to the desired size, 300 x 300 pixels.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Check preprocessed_frame.shape</summary>

Run `python app.py -m frozen_inference_graph.xml`

```
(venv) root@bb6cb0771035:/home/workspace# python app.py -m frozen_inference_graph.xml
(300, 300, 3)
(venv) root@bb6cb0771035:/home/workspace#
```

</details>

{::options parse_block_html="false" /}

Next transpose it so that the color channels will be first.

```
### TODO: Pre-process the frame
preprocessed_frame = np.copy(frame)
preprocessed_frame = cv2.resize(preprocessed_frame, (300, 300))
preprocessed_frame = preprocessed_frame.transpose((2,0,1))
print(preprocessed_frame.shape)
exit(1)
```

> `preprocessed_image = preprocessed_image.transpose((2,0,1))` - transpose function of numpy.ndarray with tuple data type of ints, converts the shape of image ndarray from (256, 456, 3) to (3, 256, 456).  
> above taple is (2,0,1) which means that 3-rd dimension becomes 1-st dimension, 1-st dimension becomes 2-nd dimension, and 2-nd dimension becomes 3-rd dimension.  
> Importantly, they are numbered starting with 0 in the taple (2,0,1).  
> make sure you are working on 3-dimensional array and shape is information about this array.  
> For more transpose function, [numpy.ndarray.transpose](https://docs.scipy.org/doc/numpy/reference/generated/numpy.ndarray.transpose.html)  
> Reference: [NUMPY AXES EXPLAINED](https://www.sharpsightlabs.com/blog/numpy-axes-explained/)

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Check preprocessed_frame.shape</summary>

Run `python app.py -m frozen_inference_graph.xml`

```
(venv) root@bb6cb0771035:/home/workspace# python app.py -m frozen_inference_graph.xml
(3, 300, 300)
(venv) root@bb6cb0771035:/home/workspace#
```

</details>

{::options parse_block_html="false" /}

And add batch dimension.

```
### TODO: Pre-process the frame
preprocessed_frame = np.copy(frame)
preprocessed_frame = cv2.resize(preprocessed_frame, (300, 300))
preprocessed_frame = preprocessed_frame.reshape(1, 3, 300, 300)
print(preprocessed_frame.shape)
exit(1)
```

> `preprocessed_frame = preprocessed_frame.reshape(1, 3, 300, 300)` - To add one more dimension for batch, it reshapes the image array from (3, h, w) to (1, 3, h, w).

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Check preprocessed_frame.shape</summary>

Run `python app.py -m frozen_inference_graph.xml`

```
(venv) root@bb6cb0771035:/home/workspace# python app.py -m frozen_inference_graph.xml
(1, 3, 300, 300)
(venv) root@bb6cb0771035:/home/workspace#
```

</details>

{::options parse_block_html="false" /}

Now pre-processing is done. You can delete them.

```
print(preprocessed_frame.shape)
exit(1)
```

Next we will use an async request to perform inference on each video frame.

In the `inference.py`, you can find `async_inference` function with the TODO.

```
def async_inference(self, image):
    '''
    Makes an asynchronous inference request, given an input image.
    '''
    ### TODO: Start asynchronous inference
    return
```

Add a few code under `### TODO: Start asynchronous inference`.

```
def async_inference(self, image):
    '''
    Makes an asynchronous inference request, given an input image.
    '''
    ### TODO: Start asynchronous inference
    self.exec_network.start_async(request_id=0, inputs={input_blob: image})

    return
```

> `self.exec_network.start_async(request_id=0, inputs={input_blob: image})` - The `start_async` function on `ExecutableNetwork`, `exec_net` variable starts asynchronous inference for specified infer request. And again `request_id` variable is hard coded because there is no more inference request.  
> Reference: [start_async()](https://docs.openvinotoolkit.org/latest/classie__api_1_1ExecutableNetwork.html#a314107a6b50f0ebf65751569973c760a)
>
> `self` - self represents the instance of the class. By using the “self” keyword we can access the attributes and methods of the class in python.

As a part of asynchronous inference request, write `wait` function to be complete the request.

```
def wait(self):
    '''
    Checks the status of the inference request.
    '''
    ### TODO: Wait for the async request to be complete
    status = self.exec_network.requests[0].wait(-1)

    return status
```

> `status = self.exec_network.requests[0].wait(-1)` - The `-1` argument means to wait until inference result becomes available and returns status of inference request. Using `request_id` (in this case, 0) with `requests` tuple, you can access `InferRequest` object.  
> Reference: [wait()](https://docs.openvinotoolkit.org/latest/classie__api_1_1InferRequest.html#a936fa50a7531e2f9a9e9c3d45afc9b43)

For extracting the results from the inference request, add the code of handling the output on `extract_output` function.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">What returned from Inference Engine</summary>

you can print the output.

```
def extract_output(self):
    '''
    Returns a list of the results for the output layer of the network.
    '''
    ### TODO: Return the outputs of the network from the output_blob
    output = self.exec_network.requests[0].outputs
    print(type(output))
    exit(1)

    return output
```

Run

```
# python app.py -m frozen_inference_graph.xml
```

output

```
(venv) root@89be21822017:/home/workspace# python app.py -m frozen_inference_graph.xml
<class 'dict'>
(venv) root@89be21822017:/home/workspace#
```

check the keys

```
def extract_output(self):
    '''
    Returns a list of the results for the output layer of the network.
    '''
    ### TODO: Return the outputs of the network from the output_blob
    output = self.exec_network.requests[0].outputs
    print(type(output))
    print(output.keys())
    exit(1)

    return output
```

Run

```
# python app.py -m frozen_inference_graph.xml
```

output

```
(venv) root@89be21822017:/home/workspace# python app.py -m frozen_inference_graph.xml
<class 'dict'>
dict_keys(['DetectionOutput'])
(venv) root@89be21822017:/home/workspace#
```

More you can check the output shape of key `'DetectionOutput'`.

```
def extract_output(self):
    '''
    Returns a list of the results for the output layer of the network.
    '''
    ### TODO: Return the outputs of the network from the output_blob
    output = self.exec_network.requests[0].outputs['DetectionOutput']
    print(output.shape)
    exit(1)

    return output
```

Run

```
# python app.py -m frozen_inference_graph.xml
```

output

```
(venv) root@89be21822017:/home/workspace# python app.py -m frozen_inference_graph.xml
(1, 1, 100, 7)
(venv) root@89be21822017:/home/workspace#
```

Summary of output information, shape `1, 1, N, 7`

| name | ? | ? | # of detected bounding boxes | each detection description |
|-------|----------------|------------------------|------------------|-----------------|
| DetectionOutput | 1 | 1 | 100 | 7 |

Reference: [SSD MobileNet V2 COCO model](https://github.com/opencv/open_model_zoo/blob/master/models/public/ssd_mobilenet_v2_coco/ssd_mobilenet_v2_coco.md)

The inportant information is the number of detected bounding boxes. For what is inside each detection description, describes later.

Do not forget to delete them.

```
print(output.shape)
exit(1)
```

</details>

{::options parse_block_html="false" /}


```
def extract_output(self):
    '''
    Returns a list of the results for the output layer of the network.
    '''
    ### TODO: Return the outputs of the network from the output_blob
    output = self.exec_network.requests[0].outputs['DetectionOutput']

    return output
```

> `output = self.exec_network.requests[0].outputs['DetectionOutput']` - Returns output of `DetectionOutput` key on `outputs` dictionary. Using `request_id` (in this case, 0) with `requests` tuple, It accesses `InferRequest` object.

Now `inference.py` is done. In the `app.py`, add code to make the requests and feed back the results.

In the beginning on `infer_on_video` function, add like this

```
### TODO: Initialize the Inference Engine
network = Network()

### TODO: Load the network model into the IE
network.load_model(args.m, args.d, CPU_EXTENSION)
```

> `network = Network()` - Initialized `Network` class on `inference.py`. The Inference Engine, `IECore` is initialized with `self.plugin = IECore()` on `inference.py` which is inside `load_model` function.
>
> `network.load_model(args.m, args.d, CPU_EXTENSION)` - `network.load_model` calls `load_model` function on `inference.py` with `args.m`, the location of the model XML file, `args.d`, the device name, if not 'CPU', and `CPU_EXTENSION` variable.  

For the next TODO, perform inference on each frame on the input video.

```
### TODO: Perform inference on the frame
network.async_inference(preprocessed_frame)
network.wait()
```

> `network.async_inference(preprocessed_frame)` - Calls `async_inference` function which is implemented on `inference.py`. It starts asynchronous inference request.
>
> `network.wait()` - Calls `wait` function which is also implemented on `inference.py`. this function waits until the inference result returned.

The next one is to extract the output of the inference.

```
### TODO: Get the output of inference
output = network.extract_output()
```

> `output = network.extract_output()` - To extract the output, use the `extract_output` method we wrote and assigned it to `output` variable.

The next TODO is "Perform any necessary post-processing steps to get the bounding boxes".

```
### TODO: Update the frame to include detected bounding boxes
```

To get detected bounding boxes, again check what is returned as a result of inference.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">What is Inside Each Bounding Boxes</summary>

We know the shape of output, `(1, 1, 100, 7)`.

Add

```
# omitted ...

### TODO: Update the frame to include detected bounding boxes
print(output.shape)
exit(1)

# omitted ...
```

Run `python app.py -m frozen_inference_graph.xml` and get like this.

```
(venv) root@e9d665dfa3b6:/home/workspace# python app.py -m frozen_inference_graph.xml
(1, 1, 100, 7)
(venv) root@e9d665dfa3b6:/home/workspace#
```

As you can see, the inference detected 100 bounding boxes. Accroding to [SSD MobileNet V2 COCO model](https://github.com/opencv/open_model_zoo/blob/master/models/public/ssd_mobilenet_v2_coco/ssd_mobilenet_v2_coco.md),

</details>

{::options parse_block_html="false" /}


Draw bounding boxes onto the frame. Iterating through all bounding boxes, check their confidence and draw rectangle on each frame. You can refer [this page](https://github.com/opencv/open_model_zoo/blob/master/models/public/ssd_mobilenet_v2_coco/ssd_mobilenet_v2_coco.md#converted-model-1) for what is inside each bounding box.

For each detection, the description has the format: `[image_id, label, conf, x_min, y_min, x_max, y_max]`.

```
for box in output[0][0]:
    confidence = box[2]
    if confidence >= 0.5:
        xmin = int(box[3] * width)
        ymin = int(box[4] * height)
        xmax = int(box[5] * width)
        ymax = int(box[6] * height)
        cv2.rectangle(frame, (xmin, ymin), (xmax, ymax), (0, 0, 255), 1)
```

> `for box in output[0][0]:` - Loops through `result[0][0]` which returns two-dimensional array which has like `(100, 7)` shape.
>
> `confidence = box[2]` - Extracts the item at the three index on each bounding box, `box`. The item means confidence for the predicted class.  
> Note: index counting from 0.
>
> `if confidence >= 0.5:` - If confidence is over 50 %, execute indented lines.
>
> `xmin = int(box[3] * width)` - At four place, it represents x coordinate of the top left bounding box corner in range 0~1. It scaled to output's width and height as multiplied by its width.
>
> The remaing three lines' concept is the same each indexs shows coordinates of the top left bounding box corner and the bottom right corner.
>
> `cv2.rectangle(frame, (xmin, ymin), (xmax, ymax), (0, 0, 255), 1)` - draw rectangle on a `frame`, `(xmin, ymin)` for pt1, `(xmax, ymax)` for pt2, `(0, 0, 255)` for color (In this case, BGR order so red rectangle), `1` for thickness.  
> Reference: [rectangle](https://docs.opencv.org/2.4/modules/core/doc/drawing_functions.html#rectangle)

All minimum requirements are done now. You can run this app. Note, this app will take a little bit longer to run.

```
# python app.py -m frozen_inference_graph.xml
```

<details>
<summary>log</summary>

<pre>
(venv) root@63a151d6584d:/home/workspace# python app.py -m frozen_inference_graph.xml
(venv) root@63a151d6584d:/home/workspace#
</pre>
</details>

You see the `out.mp4` on left folder navigation bar. Download with the right click and Play the video.

For the two more additional tasks, we start the TODO on `get_args` function on `app.py`.

Add the descriptions for the options.

```
### TODO: Add additional arguments and descriptions for:
###       1) Different confidence thresholds used to draw bounding boxes
###       2) The user choosing the color of the bounding boxes
c_desc = "The confidence thresholds used to draw bounding boxes, default 0.5"
cb_desc = "The color of the bounding boxes, default RED"
```

> `c_desc = "The confidence thresholds used to draw bounding boxes, default 0.5"` - Assignes string value for description to `c_desc`.
>
> `cb_desc = "The color of the bounding boxes, default RED"` - which is description for color option.

To create arguments for each option, add two more lines like:

```
# -- Create the arguments
required.add_argument("-m", help=m_desc, required=True)
optional.add_argument("-i", help=i_desc, default=INPUT_STREAM)
optional.add_argument("-d", help=d_desc, default='CPU')
optional.add_argument("-c", help=c_desc, default=0.5)
optional.add_argument("-cb", help=cb_desc, default='RED')
args = parser.parse_args()
```

> `optional.add_argument("-c", help=c_desc, default='0.5')` - For optional argument group, `add_argument` fuction has `"-c"` as option flag, `c_desc` as a brief description of what the argument does, and `0.5` as a default value if not.
>
> `optional.add_argument("-cb", help=cb_desc, default='RED')` - Goes the same way above.

Now, we finished to add two additional arguments and descriptions. Check app.py with help option like `python app.py -h`.

<details>
<summary>log</summary>

<pre>
(venv) root@d3b1eac75dbb:/home/workspace# python app.py -husage: Run inference on an input video [-h] -m M [-i I] [-d D] [-c C] [-cb CB]

required arguments:
  -m M    The location of the model XML file

optional arguments:
  -i I    The location of the input file
  -d D    The device name, if not 'CPU'
  -c C    The confidence thresholds used to draw bounding boxes, default 0.5
  -cb CB  The color of the bounding boxes, default RED
(venv) root@d3b1eac75dbb:/home/workspace#
</pre>
</details>

You can see two new help description.

```
# omitted ...
-c C    The confidence thresholds used to draw bounding boxes, default 0.5
-cb CB  The color of the bounding boxes, default RED
# omitted ...
```

To affect on our output result with `-c` option for confidence threshold, replace hard-coded `0.5` with `float(args.c)` using `float()` converting from string to float type.

```
### TODO: Update the frame to include detected bounding boxes
        for box in output[0][0]:
            confidence = box[2]
            if confidence >= float(args.c):
                xmin = int(box[3] * width)
                ymin = int(box[4] * height)
                xmax = int(box[5] * width)
                ymax = int(box[6] * height)
                cv2.rectangle(frame, (xmin, ymin), (xmax, ymax), (0, 0, 255), 1)
```

For `-cb` color option, we need to determine the color string (e.g. RED) to BGR tuple like (255, 0, 0). So add new helper function after `infer_on_video` function.

```
def convert_color(string_color):
    colors = {
        'RED': (0, 0, 255),
        'BLUE': (255, 0, 0),
        'GREEN': (0, 255, 0),
        'WHITE': (255, 255, 255),
        'BLACK': (0, 0, 0)
    }

    bgr_color = colors.get(string_color)
    if bgr_color:
        return bgr_color
    else:
        print('unsupported color')
        exit(1)    
```

Now you can replace hard-coded color `(0, 0, 255)` with `convert_color(args.cb)` using cb value.

```
### TODO: Update the frame to include detected bounding boxes
        for box in output[0][0]:
            confidence = box[2]
            if confidence >= args.c:
                xmin = int(box[3] * width)
                ymin = int(box[4] * height)
                xmax = int(box[5] * width)
                ymax = int(box[6] * height)
                cv2.rectangle(frame, (xmin, ymin), (xmax, ymax), convert_color(args.cb), 1)
```

Now run it again and download out.m4 file.

```
# python app.py -m frozen_inference_graph.xml -c 0.8 -cb WHITE
```

Maybe more less bounding boxes and colored white.

Outstanding!

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Solution: Integrate into an App</summary>

The biggest difference is that he used variable for input shape of the model. It is actually helper function, `get_input_shape()` inside `inference.py`.

```
### Load the network model into the IE
plugin.load_model(args.m, args.d, CPU_EXTENSION)
net_input_shape = plugin.get_input_shape()
```

Then when we need to preprocess each frame. You can add `(net_input_shape[3], net_input_shape[2])` tuple fushion.

```
### Pre-process the frame
p_frame = cv2.resize(frame, (net_input_shape[3], net_input_shape[2]))
p_frame = p_frame.transpose((2,0,1))
p_frame = p_frame.reshape(1, *p_frame.shape)
```

The model's input shape heavily depends on the model, so not to hardcode those values is more effective.

</details>

{::options parse_block_html="false" /}

# Lesson 5: Deploying an Edge App

In this lesson's exercise, you will do the following things:

- Handling Input Streams in OpenCV
- Processing Model Outputs for Additional Useful Information
- Sending statistics and video streams to a server

## Exercise: Handling Input Streams

You will perform a few other image processing techniques using a camera image or a video file.

Make sure to click the `SOURCE ENV` button before you get started to source the correct environment.

<details>
<summary>log</summary>

<pre>
root@2a3ccaa1f564:/home/workspace# source /opt/intel/openvino/bin/setupvars.sh -pyver 3.5
python_version = 3.5
[setupvars.sh] OpenVINO environment initialized
(venv) root@2a3ccaa1f564:/home/workspace#
</pre>
</details>

You can understand the app.py first.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">More Detail for app.py</summary>

import necessary libraries.

```
import argparse
import cv2
import numpy as np
```

> `import argparse` - import the argparse module to write user-friendly command-line interfaces more easily.
>
> `import cv2` - import statement to use the OpenCV package in code  
> [OpenCV Tutorial: A Guide to Learn OpenCV](https://www.pyimagesearch.com/2018/07/19/opencv-tutorial-a-guide-to-learn-opencv/)
>
> `import numpy as np` - this imports the numpy package in code and as np statement make it accessible using np in your code

The next function is `get_args` to get the arguments from the command line.

```
def get_args():
    '''
    Gets the arguments from the command line.
    '''
    parser = argparse.ArgumentParser("Handle an input stream")

# omitted ...
```

> `parser = argparse.ArgumentParser("Handle an input stream")` - The `argparse.ArgumentParser` creates the object of ArgumentParser class on Lib/argparse.py which you imported. The ArgumentParser object will hold all the information necessary to parse the command line into Python data types.  
> "Handle an input stream" string value is passed in for description to display before the argument help. It shows like this:  
> Reference: [Create object from class in separate file](https://stackoverflow.com/a/23238374)

For help description oon input file,

```
# -- Create the descriptions for the commands
i_desc = "The location of the input file"
```

> `i_desc = "The location of the input file"` - simply the variable, `i_desc` has `"The location of the input file"` string value.

Using `ArgumentParser`, create arguments.

```
# -- Create the arguments
parser.add_argument("-i", help=i_desc)
args = parser.parse_args()

return args
```

> `parser.add_argument("-i", help=i_desc)` - For the "-i" argument, adding `i_desc` variable as a brief description of what the argument does in `help=i_desc`.
>
> `args = parser.parse_args()` - It parses arguments (like "-h" on `python app.py -h`) through the `parse_args()` method. This will inspect the command line, convert each argument to the appropriate type and then invoke the appropriate action.  
> Reference: [Parsing a Command Line](https://pymotw.com/2/argparse/#parsing-a-command-line)
>
> `return args` - Returns as a output of `get_args` function.

In the `capture_stream` function, you will implment mainly.

```
def capture_stream(args):
    ### TODO: Handle image, video or webcam
# omitted ...
```

The main function which is the beginning of this app.py application.

```
def main():
    args = get_args()
    capture_stream(args)
```

> `def main():` - this defined the function called main() and inside this there are args = get_args() and perform_inference(args)
>
> `args = get_args()` - this statement calls get_args() function and assign return value to args variable ()
>
> `capture_stream(args)` - Performs `capture_stream` function with `args` variable as a arugument.

The final part is for

```
if __name__ == "__main__":
    main()
```

> `if __name__ == "__main__":` - this is the best practice for Python main functions. if statement checks the special \__name__ variable and compare it to the string "\__main__". If it is True, the Python interpreter executes main() function.

</details>

{::options parse_block_html="false" /}

On the `capture_stream` function, implement that it can handle camera image, video file or webcam inputs.

The input file is considered as following:

- 'CAM' to use the webcam
- the filename ends '.jpg' or '.bmp' as a image
- other than those above, as video file

```
def capture_stream(args):
    ### TODO: Handle image, video or webcam
    image_flag = False

    if args.i == 'CAM':
       args.i = 0
    elif args.i.endswith('.jpg') or args.i.endswith('.bmp'):
       image_flag = True

    ### TODO: Get and open video capture
    video_capture = cv2.VideoCapture(args.i)
    video_capture.open(args.i)
```

> `if args.i == 'CAM':` - Checks whether or not a user specified to use camera. If so, it sets `0` as a camera input.
>
> `elif args.i.endswith('.jpg') or args.i.endswith('.bmp'):` - Or if file name ends with `.jpg` or `.bmp`, it detects as image file. (I know this is so limited, but much easier for now)
>
> `video_capture = cv2.VideoCapture(args.i)` - Using input file, `args.i`, the `VideoCapture` function opens video file or image file sequence and VideoCapture object assigned with `video_capture` variable.
>
> `video_capture.open(args.i)` - Open video file or a capturing device for video capturing.  
> Reference: [Reading and Writing Images and Video](https://docs.opencv.org/2.4/modules/highgui/doc/reading_and_writing_images_and_video.html#videocapture-videocapture)

The next TODO is to re-size the frame to 100x100, but there are few things to do before.

```
# Get video writer for video
if image_flag:
    video_writer = None
else:
    video_writer = cv2.VideoWriter('out.mp4', 0x00000021, 30, (100,100))
```

> `if image_flag:` - If input file is image, run the following.
>
> `video_writer = None` - No need to initialize VideoWriter for image. The None keyword is used to define a null value, or no value at all.  
> Reference: [Python None Keyword](https://www.w3schools.com/python/ref_keyword_none.asp)
>
> `else:` - Then not image file, run the following.
>
> `video_writer = cv2.VideoWriter('output.mp4', 0x00000021, 30, (100,100))` - Creates `VideoWriter` object with `'output.mp4'` output file name, `0x00000021` which represents the fourcc to the ASCII number directly for mp4 video codec, `30` which is framerate of the created video stream, and `(width,height)` for size of the video frames.  
> Reference: [VideoWriter()](https://docs.opencv.org/3.4/dd/d9e/classcv_1_1VideoWriter.html#ac3478f6257454209fa99249cc03a5c59)  
> Somehow need to specify the video codec using ASCII number.  
> Reference: [How to write MP4 with OpenCV3](http://xiaoxumeng.com/how-to-write-mp4-with-opencv3/)

Using while loop, read all frames on video or images.

```
# Process frames until the video ends, or process is exited
while video_capture.isOpened():
    # Read the next frame
    flag, frame = video_capture.read()
    if not flag:
        break
    key_pressed = cv2.waitKey(60)
```

> `while video_capture.isOpened():` - while loop executes the indented lines as long as `video_capture.isOpened()` is True, the video still lasts.
>
> `flag, frame = video_capture.read()` - Returns a bool (True/False). If frame is read correctly, it will be True and the video frame is returned here as `image`. If no frames has been grabbed the image will be empty.  
> Reference: [Capture Video from Camera](https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_gui/py_video_display/py_video_display.html)
>
> `if not flag:` - if flag is False, break this while loop because there is no more frame to read.
>
> `key_pressed = cv2.waitKey(60)` - The function `waitKey` waits for a key event for 60 milliseconds in this case.  
> Reference: [waitKey](https://docs.opencv.org/2.4/modules/highgui/doc/user_interface.html?highlight=waitkey#waitkey)

Then re-size them.

```
### TODO: Re-size the frame to 100x100
frame = cv2.resize(frame, (100,100))
```

> `frame = cv2.resize(frame, (100, 100))` - OpenCV built-in function, `resize` each frame with the desired size for the output image, (100, 100).  
> Reference: [OpenCV Resize image using cv2.resize()](https://www.tutorialkart.com/opencv/python/opencv-python-resize-image/)

Add Canny Edge Detection to the frame with min & max values of 100 and 200, respectively

```
### TODO: Add Canny Edge Detection to the frame,
###       with min & max values of 100 and 200
###       Make sure to use np.dstack after to make a 3-channel image
frame = cv2.Canny(frame, 100, 200)
frame = np.dstack((frame, frame, frame))
```

> `frame = cv2.Canny(frame, 100, 200)` - Finds edges in an image using the Canny algorithm. It retruns single channels 8-bit image, which has the same size as image, (100, 100). The following values, 100 and 200, will be used for the Canny algorithm.  
> Reference: [Canny()](https://docs.opencv.org/trunk/dd/d1a/group__imgproc__feature.html#ga04723e007ed888ddf11d9ba04e2232de)
>
> `frame = np.dstack((frame, frame, frame))` - Stack arrays in sequence depth wise (along third axis). Each frame has now `(100, 100)` array and stack them three same frame along third axis. The result shape looks like `(100, 100, 3)` and it is valid on mp4 file.  
> Reference: [numpy.dstack](https://numpy.org/doc/1.18/reference/generated/numpy.dstack.html)

Save down the image or video output.

```
### TODO: Write out the frame, depending on image or video
if image_flag:
    cv2.imwrite('output.jpg', frame)
else:
    video_writer.write(frame)

# Break if escape key pressed
if key_pressed == 27:
    break
```

> `if image_flag:` - If `image_flag` is True (input file is image), run `cv2.imwrite('output.jpg', frame)`.
>
> `cv2.imwrite('output.jpg', frame)` - Saves an image to a specified file. Here, `frame` converts to as a `output.jpg`.  
> Reference: [imwrite](https://docs.opencv.org/2.4/modules/highgui/doc/reading_and_writing_images_and_video.html#imwrite)
>
> `else:` - Otherwise, executes `video_writer.write(frame)`.
>
> `video_writer.write(frame)` - Writes the next video frame to output video.  
> Reference: [write()](https://docs.opencv.org/3.4/dd/d9e/classcv_1_1VideoWriter.html#a3115b679d612a6a0b5864a0c88ed4b39)
>
> `if key_pressed == 27:` - if `key_pressed` is escape key, break the while loop.  
> Reference: [ASCII Table and Description](http://www.asciitable.com)

Close the stream and any windows at the end of the application

```
### TODO: Close the stream and any windows at the end of the application
if not image_flag:
    video_writer.release()
video_capture.release()
cv2.destroyAllWindows()
```

> `if not image_flag:` - if input file is not image, executes `video_writer.release()`.
>
> `video_writer.release()` - Closes the video writer  
> Reference: [release()](https://docs.opencv.org/3.4/dd/d9e/classcv_1_1VideoWriter.html#a667f737e56d5ba6b0533c6c7bf941140)
>
> `video_capture.release()` - Closes video file and allow OpenCV to release the captured file.  
> Reference: [release()](https://docs.opencv.org/3.4/d8/dfe/classcv_1_1VideoCapture.html#afb4ab689e553ba2c8f0fec41b9344ae6)
>
> `cv2.destroyAllWindows()` - Destroys all of the opened HighGUI windows.  
> Reference: [destroyAllWindows](https://docs.opencv.org/2.4/modules/highgui/doc/user_interface.html?highlight=destroyallwindows#destroyallwindows)

Now you can test your `app.py` using

For image,

```
# python app.py -i blue-car.jpg
```

For video,

```
# python app.py -i test_video.mp4
```

For example, converted blue-car.jpg looks like this, 100x100 picture.

{% include helpers/image.html name="download.jpeg" %}

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Solution: Handling Input Streams</summary>

The main difference is to display the resulting frame if it's video. Unfortunately, it won't work on the udacity worksapce.

```
cv2.imshow('display', edges)
```

You can download it using VideoWriter class.

</details>

{::options parse_block_html="false" /}

## Exercise: Process Model Outputs

Make sure to click the `SOURCE ENV` button before you get started to source the correct environment.

<details>
<summary>log</summary>

<pre>
(venv) root@598c7e4937de:/home/workspace# source /opt/intel/openvino/bin/setupvars.sh -pyver 3.5
python_version = 3.5
[setupvars.sh] OpenVINO environment initialized
(venv) root@598c7e4937de:/home/workspace#
</pre>
</details>

Process the model output correctly. Add code that will print to the terminal anytime the bad combination of the cat and dog #2 are detected together.

If you are not familiar with `get_args` function and `infer_on_video` function on app.py, please check these notes.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">More Detail for get_args Function</summary>

This is the first step in using the argparse is creating an ArgumentParser object.

```
def get_args():
    '''
    Gets the arguments from the command line.
    '''
    parser = argparse.ArgumentParser("Run inference on an input video")

# omitted ...
```

> `parser = argparse.ArgumentParser("Run inference on an input video")` - The `argparse.ArgumentParser` creates the object of ArgumentParser class on Lib/argparse.py which you imported. The ArgumentParser object will hold all the information necessary to parse the command line into Python data types.  
> "Run inference on an input video" string value is passed in for description to display before the argument help. It shows like this:  
> Reference: [Create object from class in separate file](https://stackoverflow.com/a/23238374)

log
```
(venv) root@598c7e4937de:/home/workspace# python app.py -husage: Run inference on an input video [-h] -m M [-i I] [-d D]

required arguments:
  -m M  The location of the model XML file

optional arguments:
  -i I  The location of the input file
  -d D  The device name, if not 'CPU'
(venv) root@598c7e4937de:/home/workspace#
```

For preparation of the descriptions for the each arguments, it creates string vlues wich is used later.

```
# -- Create the descriptions for the commands
m_desc = "The location of the model XML file"
i_desc = "The location of the input file"
d_desc = "The device name, if not 'CPU'"
```

The next few lines are configuring the argument groups for showing the help messages when running with `-h` or `--help` argument.

```
# -- Add required and optional groups
parser._action_groups.pop()
required = parser.add_argument_group('required arguments')
optional = parser.add_argument_group('optional arguments')
```

> `parser._action_groups.pop()` -  By default, ArgumentParser groups command-line arguments into “positional arguments” and “optional arguments” which is stored in `_action_groups` internally when displaying help messages. To show the argument groups more sophisticated way, it can be removed last argument group from the list, “optional arguments”. Without popping (removing) the “optional arguments”, optional argument group shows up first by default.  
> Reference: [Argparse: Required arguments listed under “optional arguments”?](https://stackoverflow.com/questions/24180527/argparse-required-arguments-listed-under-optional-arguments)
>
> `required = parser.add_argument_group('required arguments')` - New argument group called 'required arguments' is created for a better conceptual grouping of arguments than this default one. the returned argument group object assignes the variable, required.
>
> `optional = parser.add_argument_group('optional arguments')` - The same concept is applied here. It re-creates the 'optional arguments' group because the the default 'optional arguments' group is deleted and to shows the optional group under the 'required arguments' group

Check the data type of the `parser._action_groups` and comment out the `parser._action_groups.pop()` line to understand how it works in `app.py` code.

```
# -- Add required and optional groups
print(type(parser._action_groups))
# parser._action_groups.pop()
required = parser.add_argument_group('required arguments')
optional = parser.add_argument_group('optional arguments')
```

Then run on the command line to show help messages.

```
python app.py -h
```

> `-h` - which is a default option to show help messages.

As you can see that `_action_groups` is list class accroding to `<class 'list'>` and `optional arguments:` part is shown here because it is not deleted using pop function.

log

```
(venv) root@598c7e4937de:/home/workspace# python app.py -h
<class 'list'>
usage: Run inference on an input video [-h] -m M [-i I] [-d D]

optional arguments:
  -h, --help  show this help message and exit

required arguments:
  -m M        The location of the model XML file

optional arguments:
  -i I        The location of the input file
  -d D        The device name, if not 'CPU'
(venv) root@598c7e4937de:/home/workspace#
```

Those arguments such as "-i" and "-m" is defined with some parameters and assigned to the each required and optional argument groups created at the above part.

```
# -- Create the arguments
required.add_argument("-m", help=m_desc, required=True)
optional.add_argument("-i", help=i_desc, default=INPUT_STREAM)
optional.add_argument("-d", help=d_desc, default='CPU')
args = parser.parse_args()

return args
```

> `required.add_argument("-m", help=m_desc, required=True)` - For the "-m" argument, adding `m_desc` variable as a brief description of what the argument does in `help=m_desc`. Also it is flaged as a required argument when you use `app.py`.
>
> `optional.add_argument("-i", help=i_desc, default=INPUT_STREAM)` - Almost same one as you did above, the "-i" argument is added in optional argument group you created above and the value parameter produced as None here if the argument is absent from the command line which means optional argument, in other words.
>
> `optional.add_argument("-d", help=d_desc, default="CPU")` - If "-d" is not passed in on the command line, the value, "CPU" is filled in by default.
>
> `args = parser.parse_args()` - It parses arguments (like "-h" on `python app.py -h`) through the parse_args() method. This will inspect the command line, convert each argument to the appropriate type and then invoke the appropriate action.  
> Reference: [Parsing a Command Line](https://pymotw.com/2/argparse/#parsing-a-command-line)
>
> `return args` - return args object with parsed arguments.

</details>

{::options parse_block_html="false" /}

<br>

{::options parse_block_html="true" /}

<details>
<summary markdown="span">More Detail for infer_on_video Function</summary>

Let's look closer each part of `infer_on_video` function.

```
def infer_on_video(args):
```

> `def infer_on_video(args):` - The first line of function definition. The `args` variable can be passed into this function as `args` argument. (This function is used like `infer_on_video(args)`)

```
# Initialize the Inference Engine
plugin = Network()

# Load the network model into the IE
plugin.load_model(args.m, args.d, CPU_EXTENSION)
net_input_shape = plugin.get_input_shape()
```

> `plugin = Network()` - Initialized `Network` class on `inference.py`. The Inference Engine, `IECore` is initialized with `self.plugin = IECore()` on `inference.py` which is inside `load_model` function.
>
> `plugin.load_model(args.m, args.d, CPU_EXTENSION)` - `plugin.load_model` calls `load_model` function on `inference.py` with `args.m`, the location of the model XML file, `args.d`, the device name, if not 'CPU', and `CPU_EXTENSION` variable.
>
> `net_input_shape = plugin.get_input_shape()` - The variable `net_input_shape` is for input shape of the model. It is helper function, `get_input_shape()` inside `inference.py`.

```
# Get and open video capture
cap = cv2.VideoCapture(args.i)
cap.open(args.i)
```

> `cap = cv2.VideoCapture(args.i)` - Using input file, `args.i`, the `VideoCapture` function opens video file and VideoCapture object assigned with `cap` variable.
>
> `cap.open(args.i)` - Open video file for video capturing.  
> Reference: [Reading and Writing Images and Video](https://docs.opencv.org/2.4/modules/highgui/doc/reading_and_writing_images_and_video.html#videocapture-videocapture)

```
# Process frames until the video ends, or process is exited
while cap.isOpened():
    # Read the next frame
    flag, frame = cap.read()
    if not flag:
        break
    key_pressed = cv2.waitKey(60)
```

> `while cap.isOpened():` - while loop executes the indented lines as long as `cap.isOpened()` is True, the video still lasts.
>
> `flag, frame = cap.read()` - Returns a bool (True/False). If frame is read correctly, it will be True and the video frame is returned here as `image`. If no frames has been grabbed the image will be empty.
> Reference: [Capture Video from Camera](https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_gui/py_video_display/py_video_display.html)
>
> `if not flag:` - if flag is False, break this while loop because there is no more frame to read.
>
> `key_pressed = cv2.waitKey(60)` - The function `waitKey` waits for a key event for 60 milliseconds in this case.
> Reference: [waitKey](https://docs.opencv.org/2.4/modules/highgui/doc/user_interface.html?highlight=waitkey#waitkey)

```
# Pre-process the frame
p_frame = cv2.resize(frame, (net_input_shape[3], net_input_shape[2]))
p_frame = p_frame.transpose((2,0,1))
p_frame = p_frame.reshape(1, *p_frame.shape)
```

> `p_frame = cv2.resize(frame, (net_input_shape[3], net_input_shape[2]))` - resize function of cv2 resizes the preprocessed_image to the desired size which is the same with input requirements on this model. It extracts using `net_input_shape`.
>
> `p_frame = p_frame.transpose((2,0,1))` - transpose function of numpy.ndarray with tuple data type of ints, converts the shape of image ndarray like from (224, 224, 3) to (3, 224, 224).  
> above taple is (2,0,1) which means that 3-rd dimension becomes 1-st dimension, 1-st dimension becomes 2-nd dimension, and 2-nd dimension becomes 3-rd dimension.  
> Importantly, they are numbered starting with 0 in the taple (2,0,1).  
> make sure you are working on 3-dimensional array and shape is information about this array.  
> For more transpose function, [numpy.ndarray.transpose](https://docs.scipy.org/doc/numpy/reference/generated/numpy.ndarray.transpose.html)  
> Reference: [NUMPY AXES EXPLAINED](https://www.sharpsightlabs.com/blog/numpy-axes-explained/)
>
> `p_frame = p_frame.reshape(1, *p_frame.shape)` - To add one more dimension for batch, it reshapes the image array from (3, h, w) to (1, 3, h, w). The * (star/asterisk) unpacks argument lists when calling a function. So `1, *p_frame.shape` looks like `1, 3, 224, 224`.  
> Reference: [What does ** (double star/asterisk) and * (star/asterisk) do for parameters?](https://stackoverflow.com/questions/36901/what-does-double-star-asterisk-and-star-asterisk-do-for-parameters)

```
# Perform inference on the frame
plugin.async_inference(p_frame)
```

> `network.async_inference(preprocessed_frame)` - Calls `async_inference` function which is implemented on `inference.py`. It starts asynchronous inference request.

```
# Get the output of inference
if plugin.wait() == 0:
    result = plugin.extract_output()
    ### TODO: Process the output
```

> `if plugin.wait() == 0:` - Determines if the `wait` function returns 0 as the asynchronous inference request is finished, which is also implemented on `inference.py`. This function waits until the inference result returned.
>
> `result = plugin.extract_output()` - To extract the output, use the `extract_output` method we wrote and assigned it to `result` variable.
>
> `### TODO: Process the output` - comments. This is our TODO which will be implemented later.

```
# Break if escape key pressed
if key_pressed == 27:
    break
```

> `if key_pressed == 27:` - if `key_pressed` is escape key, break the while loop.  
> Reference: [ASCII Table and Description](http://www.asciitable.com)

```
# Release the capture and destroy any OpenCV windows
cap.release()
cv2.destroyAllWindows()
```

> `cap.release()` - Closes video file and allow OpenCV to release the captured file.  
> Reference: [release()](https://docs.opencv.org/3.4/d8/dfe/classcv_1_1VideoCapture.html#afb4ab689e553ba2c8f0fec41b9344ae6)
>
> `cv2.destroyAllWindows()` - Destroys all of the opened HighGUI windows.  
> Reference: [destroyAllWindows](https://docs.opencv.org/2.4/modules/highgui/doc/user_interface.html?highlight=destroyallwindows#destroyallwindows)

</details>

{::options parse_block_html="false" /}

<br>

{::options parse_block_html="true" /}

<details>
<summary markdown="span">More Detail for main Function</summary>

The main function is the very beginning of `app.py` python application.

```
def main():
    args = get_args()
    infer_on_video(args)
```

> `def main():` - this defined the function called main() and inside this there are args = get_args() and perform_inference(args)
>
> `args = get_args()` - this statement calls get_args() function and assign return value to args variable ()
>
> `infer_on_video(args)` - This code executes perform_inference function with the args parameter which is assigned on args = get_args()

```
if __name__ == "__main__":
    main()
```

> `if __name__ == "__main__":` - this is the best practice for Python main functions. if statement checks the special \__name__ variable and compare it to the string "\__main__". If it is True, the Python interpreter executes main() function.
>
> The special \__name__ variable is defined by Python when it executed.  
> When you execute the Python file as a script using the command line like `python app.py`, \__name__ variable will have the string value "\__main__".  
> As the second way, the Python interpreter will execute your code: imports using like `import cv2`, \__name__ variable will have the string value "cv2" in this case.  
> Reference: [Defining Main Functions in Python](https://realpython.com/python-main-function/)

</details>

{::options parse_block_html="false" /}

We process the result of inference on the TODO: Process the output. First add code so that check what the result looks like.

```
### TODO: Process the output
print(result.shape)
print(result)
exit(1)
```

Then run

```
# python app.py -m model.xml
```

{::options parse_block_html="true" /}

<details>
<summary markdown="span">log</summary>

```
(venv) root@598c7e4937de:/home/workspace# python app.py -m model.xml
(1, 3)
[[0. 0. 1.]]
(venv) root@598c7e4937de:/home/workspace#
```

</details>

{::options parse_block_html="false" /}

now you know that the output shape is (1, 3) and three dicimal value in it. This result fits the explanation on Udacity guide, the provided model will return three classes, one for one or less pets on screen, one for the bad combination of the cat and dog #2, and one for the fine combination of the cat and dog #1.

you can assumes that the result, `[[0. 0. 1.]]` means for the fine combination, for example.

So the situation that we can warn here is `[[0. 1. 0.]]` represents the bad combination.

Also we focus on only the second value so that it chacks the bad combination.

```
### TODO: Process the output
result = result[0][1]
print(result)
if result > 0:
    print('WARN: this is bad combination')
```

> `result = result[0][1]` - Extracts the second value from `result` and reassign to `result` variable.
>
> `print(result)` - print the result for debugging purpose.
>
> `if result > 0:` - if result value is greater than 0, print "WARN: this is bad combination".

Now run

```
# python app.py -m model.xml
```

As you can see, if the value is 1, print every time like

```
# omitted ...
1.0
WARN: this is bad combination
1.0
WARN: this is bad combination
1.0
WARN: this is bad combination
1.0
WARN: this is bad combination
1.0
# omitted ...
```

It looks like mess and you know the note:

> Note: It's important to consider whether you really want to output a warning every single time both pets are on-screen - is your warning helpful if it re-starts every 30th of a second, with a video at 30 fps?

Now we use the previous result. You can initilize `previous_result` variable outside of the loop like:

```
def infer_on_video(args):
    previous_result = None
```

Then add one more condition for if the result is changed comparing the previous result.

```
### TODO: Process the output
result = result[0][1]
print(result)
if previous_result != result and result > 0:
    print('WARN: this is bad combination')

previous_result = result
```

> `if previous_result != result and result > 0:` - If `result` is changed and `result` is greater than 0 at the same time, it warns you on terminal.
>
> `previous_result = result` - After if statement, assign the `result` into `previous_result` variable.

Now it's time to run again, `python app.py -m model.xml`.

```
0.0
0.0
1.0
WARN: this is bad combination
1.0
1.0
1.0
1.0
1.0
```

Now it's not annoying at all, but it warns when it turn into the bad combination.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">Solution: Process Model Outputs</summary>

He is using `counter` for timestamp and `incident_flag` to send a message to the pets to break it up.

The `timestamp` by checking how many frames had been processed so far at 30 fps by dividing `counter` by 30.

```
timestamp = counter / 30
```

And it print the `timestamp` when the incident happens.

```
print("Log: Incident at {:.2f} seconds.".format(timestamp))
```

> `print("Log: Incident at {:.2f} seconds.".format(timestamp))` - The `format` function is for the string formatting method. It has a `{placeholder:format_spec}` format, `placeholder` is not specified here. The right-hand side `.2f` shows two decimal places using `f` which fix point number format.  
Reference: [Python String format() Method](https://www.w3schools.com/python/ref_string_format.asp)

If also the bad combination of pets was on screen, but also to track whether I already warned them in the current incident using `incident_flag`.

```
if result[0][1] == 1 and not incident_flag:
```

After warning, it sets True as we already warned them.

```
incident_flag = True
```

Then if the next frame is not the bad combination, the `incident_flag` will be set as False for warning next time.

```
elif result[0][1] != 1:
     incident_flag = False
```

</details>

{::options parse_block_html="false" /}

## Exercise: Server Communications

Make sure to click the `SOURCE ENV` button before you get started to source the correct environment.

<details>
<summary>log</summary>

<pre>
(venv) root@dd84b8a14c61:/home/workspace# source /opt/intel/openvino/bin/setupvars.sh -pyver 3.5
python_version = 3.5
[setupvars.sh] OpenVINO environment initialized
(venv) root@dd84b8a14c61:/home/workspace#
</pre>
</details>

First, let's understand what the `app.py` is doing and what should we implement for sending statistics over MQTT and images with FFMPEG.

As you can see, there are some import statements and TODO for importing any libraries for MQTT and FFmpeg

```
import argparse
import cv2
import numpy as np
import socket
import json
from random import randint
from inference import Network
### TODO: Import any libraries for MQTT and FFmpeg
```

> `import argparse` - import the argparse module to write user-friendly command-line interfaces more easily.
>
> `import cv2` - import statement to use the OpenCV package in code  
> [OpenCV Tutorial: A Guide to Learn OpenCV](https://www.pyimagesearch.com/2018/07/19/opencv-tutorial-a-guide-to-learn-opencv/)
>
> `import numpy as np` - this imports the numpy package in code and as np statement make it accessible using np in your code
>
> `import socket` - Import socket library which is network interface for connecting two nodes on a network to communicate with each other.  
> Reference: [Socket Programming in Python](https://www.geeksforgeeks.org/socket-programming-python/)
>
> `import json` - json is a built-in package to work with JSON data.  
> Reference: [Python JSON](https://www.w3schools.com/python/python_json.asp)
>
> `from random import randint` - Import `randint` is an inbuilt function of the `random` module in Python3.
> Reference: [Python | randint() function](https://www.geeksforgeeks.org/python-randint-function/)
>
> `### TODO: Import any libraries for MQTT and FFmpeg` - TODO comment for implementing later.

The next few lines is constant variables which is written in all capital letters.  
Reference: [Constants](https://www.python.org/dev/peps/pep-0008/#constants)

```
INPUT_STREAM = "test_video.mp4"
CPU_EXTENSION = "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"
ADAS_MODEL = "/home/workspace/models/semantic-segmentation-adas-0001.xml"


CLASSES = ['road', 'sidewalk', 'building', 'wall', 'fence', 'pole',
'traffic_light', 'traffic_sign', 'vegetation', 'terrain', 'sky', 'person',
'rider', 'car', 'truck', 'bus', 'train', 'motorcycle', 'bicycle', 'ego-vehicle']
```

> `INPUT_STREAM = "test_video.mp4"` - The `INPUT_STREAM` constant for input value.
>
> `CPU_EXTENSION = "/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64/libcpu_extension_sse4.so"` - Assignes cpu extension for your workspace's cpu.
>
> `ADAS_MODEL = "/home/workspace/models/semantic-segmentation-adas-0001.xml"` - The pre-trained model for semantic segmentation.  
> Refernece: [semantic-segmentation-adas-0001](https://docs.openvinotoolkit.org/2019_R1/_semantic_segmentation_adas_0001_description_semantic_segmentation_adas_0001.html)
>
> `CLASSES = ['road', 'sidewalk', 'building', 'wall', 'fence', 'pole',
'traffic_light', 'traffic_sign', 'vegetation', 'terrain', 'sky', 'person',
'rider', 'car', 'truck', 'bus', 'train', 'motorcycle', 'bicycle', 'ego-vehicle']` - The class names for semantic-segmentation-adas-0001.

The next section is about MQTT server environment variables.

```
# MQTT server environment variables
HOSTNAME = socket.gethostname()
IPADDRESS = socket.gethostbyname(HOSTNAME)
MQTT_HOST = IPADDRESS
MQTT_PORT = None ### TODO: Set the Port for MQTT
MQTT_KEEPALIVE_INTERVAL = 60
```

> `HOSTNAME = socket.gethostname()` - The `HOSTNAME` has a string containing the hostname of the current workspace.  
> Reference: [socket.gethostname()](https://docs.python.org/3.8/library/socket.html#socket.gethostname)
>
> `IPADDRESS = socket.gethostbyname(HOSTNAME)` - The `gethostbyname` function translates a host name to IPv4 address format.  It goes `IPADDRESS` variable.
> Reference: [socket.gethostbyname(hostname)](https://docs.python.org/3.8/library/socket.html#socket.gethostbyname)
>
> `MQTT_HOST = IPADDRESS` - The `MQTT_HOST` has the same with `IPADDRESS`.
>
> `MQTT_PORT = None ### TODO: Set the Port for MQTT` - We will specify port later.
>
> `MQTT_KEEPALIVE_INTERVAL = 60` - The interval which the client sends a packet to confirm that the network connection is still alive.  
> Reference: [Keep Alive and Client Take-Over - MQTT Essentials Part 10](https://www.hivemq.com/blog/mqtt-essentials-part-10-alive-client-take-over/)

The `get_args` function is the same function as described those above exercises which taks input file and device name.

The next section is for the `draw_masks` helper function to add mask on each flame.

```
def draw_masks(result, width, height):
```

> `def draw_masks(result, width, height):` - Defines `draw_masks` function with three inputs result, width, height.

The output by the pre-trained model describes [here](https://docs.openvinotoolkit.org/2019_R1/_semantic_segmentation_adas_0001_description_semantic_segmentation_adas_0001.html).

```
# Create a mask with color by class
classes = cv2.resize(result[0].transpose((1,2,0)), (width,height),
    interpolation=cv2.INTER_NEAREST)
unique_classes = np.unique(classes)
out_mask = classes * (255/20)
```

> `classes = cv2.resize(result[0].transpose((1,2,0)), (width,height), interpolation=cv2.INTER_NEAREST)` - Resize the result, (H, W, B) ndarray to the (width,height) comes from function arguments. The interpolation is a method how it shrink the output. The output result shape is (B, H=1024, W=2048).  
Reference: [cv2 resize interpolation methods](https://chadrick-kwag.net/cv2-resize-interpolation-methods/)
>
> `unique_classes = np.unique(classes)` - Extract the sorted unique elements of an array which stored the detected classes.  
> Reference: [numpy.unique](https://docs.scipy.org/doc/numpy/reference/generated/numpy.unique.html)
>
> `out_mask = classes * (255/20)` - Convert each classes to grayscale.

Then stack them as a frame.

```
# Stack the mask so FFmpeg understands it
out_mask = np.dstack((out_mask, out_mask, out_mask))
out_mask = np.uint8(out_mask)

return out_mask, unique_classes
```

> `out_mask = np.dstack((out_mask, out_mask, out_mask))` - Stack `out_mask` arrays in sequence depth wise (color channels in this case). Now the shape is like `(720, 1280, 3)`  
> Reference: [numpy.dstack](https://docs.scipy.org/doc/numpy/reference/generated/numpy.dstack.html)
>
> `out_mask = np.uint8(out_mask)` - Dataype, `uint8` is Used as a function to convert python numbers to array scalars.  
> Reference: [Data types](https://docs.scipy.org/doc/numpy-1.13.0/user/basics.types.html)
>
> `return out_mask, unique_classes` - Returns out_mask and unique_classes as outputs.

On the `infer_on_video` function, you can see the function already implemented performing inference on a frame and some more TODO related MQTT and node servers.

And the final section is about main function to run the functions which we looked at so far.

```
def main():
    args = get_args()
    model = ADAS_MODEL
    infer_on_video(args, model)
```

For the MQTT server port, we set `3001` port mentioned on discription.

```
MQTT_PORT = 3001 ### TODO: Set the Port for MQTT
```

Then we make this app.py connect to the MQTT server.

```
### TODO: Connect to the MQTT server
client = mqtt.Client()
client.connect(MQTT_HOST, port=MQTT_PORT, keepalive=MQTT_KEEPALIVE_INTERVAL)
```

> `client = mqtt.Client()` - Create a client instance
> Reference: [Constructor / reinitialise](https://pypi.org/project/paho-mqtt/#constructor-reinitialise)
>
> `client.connect(MQTT_HOST, port=MQTT_PORT, keepalive=MQTT_KEEPALIVE_INTERVAL)` - Connects the client to a broker using pre-defined contants.  
> Reference: [Connect / reconnect / disconnect](https://pypi.org/project/paho-mqtt/#connect-reconnect-disconnect)

Now, we import `paho.mqtt.client` for using them.

```
### TODO: Import any libraries for MQTT and FFmpeg
import paho.mqtt.client as mqtt
```

The next TODO is to publish data to the MQTT server.

```
### TODO: Send the class names and speed to the MQTT server
### Hint: The UI web server will check for a "class" and
### "speedometer" topic. Additionally, it expects "class_names"
### and "speed" as the json keys of the data, respectively.
client.publish("class", json.dumps({"class_names": class_names}))
client.publish("speedometer", json.dumps({"speed": speed}))
```

> `client.publish("class", json.dumps({"class_names": class_names}))` - Publish topic named `class` and json payload. The next line is the same for `speedometer` as well. The `json.dumps` serialize obj to a JSON formatted str.  
> Reference: [json.dumps](https://docs.python.org/3/library/json.html#json.dumps)

Again using `json` for payload, add imports.

```
### TODO: Import any libraries for MQTT and FFmpeg
import paho.mqtt.client as mqtt
import json
```

The next TODO is

```
### TODO: Send frame to the ffmpeg server
```

With the `sys` Python library, can use `sys.stdout.buffer.write(frame)` and `sys.stdout.flush()` to send the frame to the ffserver when it is running.  It actually pass each frame to the stdout on your terminal and then read them by ffmpeg command which you run later.

```
### TODO: Send frame to the ffmpeg server
sys.stdout.buffer.write(out_frame)
sys.stdout.flush()
```

> `sys.stdout.buffer.write(out_frame)` - Write binary data to stdout in python 3. The stdout also known as standard streams are preconnected input and output communication channels between a computer program and its environment when it begins execution.
> Reference: [How to write binary data to stdout in python 3?](https://stackoverflow.com/questions/908331/how-to-write-binary-data-to-stdout-in-python-3)
>
> `sys.stdout.flush()` - Forces it to "flush" the buffer, meaning that it will write everything in the buffer to the terminal, when they have `frame` each time.  
> [Usage of sys.stdout.flush() method](https://stackoverflow.com/questions/10019456/usage-of-sys-stdout-flush-method)

Let's import `sys` library.

```
### TODO: Import any libraries for MQTT and FFmpeg
import paho.mqtt.client as mqtt
import paho.mqtt.publish as publish
import sys
```

In the final TODO, disconnect from MQTT.

```
### TODO: Disconnect from MQTT
client.disconnect()
```

Now, all work is done. let's run all applications.

Move cd `/home/workspace/webservice/server` directory, then run

```
npm install
```

> `npm install` - Install the dependencies in the local node modules and npm is package maneger.

long output here. make sure it added some packages.

```
# omitted ...
added 280 packages from 315 contributors and audited 1717 packages in 51.302s
found 9 vulnerabilities (2 low, 1 moderate, 6 high)
  run `npm audit fix` to fix them, or `npm audit` for details
(venv) root@1bf3cac2288a:/home/workspace/webservice/server#
```

Also run `npm install` on `/home/workspace/webservice/ui`

```
# omitted ...
added 1418 packages from 860 contributors and audited 20842 packages in 43.493s
found 41 vulnerabilities (27 low, 8 moderate, 6 high)
  run `npm audit fix` to fix them, or `npm audit` for details


   ╭────────────────────────────────────────────────────────────────╮
   │                                                                │
   │       New minor version of npm available! 6.7.0 → 6.13.7       │
   │   Changelog: https://github.com/npm/cli/releases/tag/v6.13.7   │
   │               Run npm install -g npm to update!                │
   │                                                                │
   ╰────────────────────────────────────────────────────────────────╯

(venv) root@1bf3cac2288a:/home/workspace/webservice/ui#
```

You can open four new terminals in the workspace in the upper left (File>>New>>Terminal).

On the first terminal,

Change directory with `cd /home/workspace/webservice/server/node-server` then run to start as MQTT broker server.

```
node ./server.js
```

```
(venv) root@1bf3cac2288a:/home/workspace/webservice/ui# cd /home/workspace/webservice/server/node-server
(venv) root@1bf3cac2288a:/home/workspace/webservice/server/node-server# node ./server.js
Mosca server started.

```

then just leave it here.

In the next terminal, run after changing directory with `cd /home/workspace/webservice/ui` for UI.

```
npm run dev
```

```
root@1bf3cac2288a:/home/workspace# cd /home/workspace/webservice/ui
root@1bf3cac2288a:/home/workspace/webservice/ui# npm run dev

> vehicle-edge-app@0.1.0 dev /home/workspace/webservice/ui
> cross-env NODE_ENV=development webpack-dev-server --history-api-fallback --watch --hot --inline

Project is running at http://0.0.0.0:3000/
webpack output is served from /
404s will fallback to /index.html
(node:1451) DeprecationWarning: loaderUtils.parseQuery() received a non-string value which can be problematic, see https://github.com/webpack/loader-utils/issues/56
parseQuery() will be replaced with getOptions() in the next major version of loader-utils.
Hash: 18f4bf285e29efaf31e0
Version: webpack 2.7.0
Time: 6486ms
     Asset       Size  Chunks                    Chunk Names
 bundle.js    6.12 MB       0  [emitted]  [big]  main
index.html  426 bytes          [emitted]         
chunk    {0} bundle.js (main) 2.22 MB [entry] [rendered]
    [6] ./~/react/react.js 56 bytes {0} [built]
   [68] ./~/redux/es/index.js 1.08 kB {0} [built]
   [92] ./~/react-redux/es/index.js 229 bytes {0} [built]
  [102] ./~/url/url.js 23.3 kB {0} [built]
  [289] ./~/react-router-redux/es/index.js 420 bytes {0} [built]
  [315] (webpack)/hot/emitter.js 77 bytes {0} [built]
  [317] ./src/index.jsx 2.64 kB {0} [built]
  [318] (webpack)-dev-server/client?http://0.0.0.0:3000 7.93 kB {0} [built]
  [319] (webpack)/hot/dev-server.js 1.57 kB {0} [built]
  [325] ./src/components/navigation/ConnectedNavigation.jsx 850 bytes {0} [built]
  [327] ./src/dux/reducers.js 509 bytes {0} [built]
  [329] ./src/features/stats/ConnectedStats.jsx 537 bytes {0} [built]
  [331] ./src/pages/monitor/Monitor.jsx 2.6 kB {0} [built]
  [400] ./~/history/createBrowserHistory.js 146 bytes {0} [built]
  [588] multi (webpack)-dev-server/client?http://0.0.0.0:3000 webpack/hot/dev-server ./src/index.jsx 52 bytes {0} [built]
     + 574 hidden modules
Child html-webpack-plugin for "index.html":
    chunk    {0} index.html 414 bytes [entry] [rendered]
        [0] ./~/html-webpack-plugin/lib/loader.js!./src/index.html 414 bytes {0} [built]
webpack: Compiled successfully.

```

In the next terminal, run for handling ffmpeg.

```
sudo ffserver -f ./ffmpeg/server.conf
```

```
root@1bf3cac2288a:/home/workspace# sudo ffserver -f ./ffmpeg/server.conf
ffserver version 2.8.15-0ubuntu0.16.04.1 Copyright (c) 2000-2018 the FFmpeg developers
  built with gcc 5.4.0 (Ubuntu 5.4.0-6ubuntu1~16.04.10) 20160609
  configuration: --prefix=/usr --extra-version=0ubuntu0.16.04.1 --build-suffix=-ffmpeg --toolchain=hardened --libdir=/usr/lib/x86_64-linux-gnu --incdir=/usr/include/x86_64-linux-gnu --cc=cc --cxx=g++ --enable-gpl --enable-shared --disable-stripping --disable-decoder=libopenjpeg --disable-decoder=libschroedinger --enable-avresample --enable-avisynth --enable-gnutls --enable-ladspa --enable-libass --enable-libbluray --enable-libbs2b --enable-libcaca --enable-libcdio --enable-libflite --enable-libfontconfig --enable-libfreetype --enable-libfribidi --enable-libgme --enable-libgsm --enable-libmodplug --enable-libmp3lame --enable-libopenjpeg --enable-libopus --enable-libpulse --enable-librtmp --enable-libschroedinger --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libssh --enable-libtheora --enable-libtwolame --enable-libvorbis --enable-libvpx --enable-libwavpack --enable-libwebp --enable-libx265 --enable-libxvid --enable-libzvbi --enable-openal --enable-opengl --enable-x11grab --enable-libdc1394 --enable-libiec61883 --enable-libzmq --enable-frei0r --enable-libx264 --enable-libopencv
  libavutil      54. 31.100 / 54. 31.100
  libavcodec     56. 60.100 / 56. 60.100
  libavformat    56. 40.101 / 56. 40.101
  libavdevice    56.  4.100 / 56.  4.100
  libavfilter     5. 40.101 /  5. 40.101
  libavresample   2.  1.  0 /  2.  1.  0
  libswscale      3.  1.101 /  3.  1.101
  libswresample   1.  2.101 /  1.  2.101
  libpostproc    53.  3.100 / 53.  3.100
./ffmpeg/server.conf:32: Setting default value for video bit rate tolerance = 2048000. Use NoDefaults to disable it.
./ffmpeg/server.conf:32: Setting default value for video rate control equation = tex^qComp. Use NoDefaults to disable it.
./ffmpeg/server.conf:32: Setting default value for video max rate = 16384000. Use NoDefaults to disable it.
Sun Feb 23 11:29:01 2020 FFserver started.

```

In the final terminal, first source the environment for OpenVINO

```
source /opt/intel/openvino/bin/setupvars.sh -pyver 3.5
```

then run the application

```
python app.py | ffmpeg -f rawvideo -pixel_format bgr24 -video_size 1280x720 -framerate 24 -i - http://0.0.0.0:3004/fac.ffm
```

> `python app.py` - Run app.py application.
>
> `ffmpeg` - Run ffmpeg using pipe `|` to combine python and ffmpeg command.
>
> `-f rawvideo` - Force input or output file format as a rawvideo.
>
> `-pixel_format bgr24` - Set pixel format as BGR.
>
> `-video_size 1280x720` - Set the video size as well.
>
> `-framerate 24` - Specify the frame rate with 24.
>
> `-i -` - Means input from stdin stream.  
> Reference: [What does dash "-" at the end of a command mean?](https://unix.stackexchange.com/questions/41828/what-does-dash-at-the-end-of-a-command-mean)
>
> `http://0.0.0.0:3004/fac.ffm` - Specifies the target server.

```
root@1bf3cac2288a:/home/workspace# source /opt/intel/openvino/bin/setupvars.sh -pyver 3.5
python_version = 3.5
[setupvars.sh] OpenVINO environment initialized
(venv) root@1bf3cac2288a:/home/workspace#
(venv) root@1bf3cac2288a:/home/workspace# python app.py | ffmpeg -v warning -f rawvideo -pixel_format bgr24 -video_size 1280x720 -framerate 24 -i - http://0.0.0.0:3004/fac.ffm
```

awesome your work!

{% include helpers/image.html name="Screen Shot 2020-02-23 at 20.51.36.png" %}
