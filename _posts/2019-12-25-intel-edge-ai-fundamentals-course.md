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

# LESSON 2: Leveraging Pre-Trained Models

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

Make sure to click the button below before you get started to source the correct environment.

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

```python
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
> `preprocessed_image = np.copy(input_image)` - this copy() function on np copies the image as numpy.ndarray which is an object stands for a N-dimensional array and then the returning copy assignes to the preprocessed_image variable. Here copy() function works the same as python's deepcopy() which means it constructs a new compound object without references.  
> Reference: [8.10. copy — Shallow and deep copy operations](https://docs.python.org/3.5/library/copy.html)
>
> `return preprocessed_image` - return the value of preprocessed_image which is literally processed image on pose_estimation function

To meet the image size expectation, add below to resize the input image.

```python
preprocessed_image = cv2.resize(preprocessed_image, (456, 256))
```

> `preprocessed_image = cv2.resize(preprocessed_image, (456, 256))` - resize function of cv2 resizes the preprocessed_image to the desired size, 456 x 256 pixels. resized image assignes preprocessed_image again.

Now check the ndarray shape information and ndarray itself with print statement which is also useful on debugging. The `pose_estimation` function looks like this:

```python
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

```python
preprocessed_image = preprocessed_image.transpose((2,0,1))
```

> `preprocessed_image = preprocessed_image.transpose((2,0,1))` - transpose function of numpy.ndarray with tuple data type of ints, converts the shape of image ndarray from (256, 456, 3) to (3, 256, 456).  
> above taple is (2,0,1) which means that 3-rd dimension becomes 1-st dimension, 1-st dimension becomes 2-nd dimension, and 2-nd dimension becomes 3-rd dimension.  
> Importantly, they are numbered starting with 0 in the taple (2,0,1).  
> make sure you are working on 3-dimensional array and shape is information about this array.  
> For more transpose function, [numpy.ndarray.transpose](https://docs.scipy.org/doc/numpy/reference/generated/numpy.ndarray.transpose.html)  
> Reference: [NUMPY AXES EXPLAINED](https://www.sharpsightlabs.com/blog/numpy-axes-explained/)

Check ndarray of `preprocessed_image` with `pose_estimation` function which looks like:

```python
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

```python
def pose_estimation(input_image):
    # omitted ...
    preprocessed_image = np.copy(input_image)

    preprocessed_image = cv2.resize(preprocessed_image, (456, 256))
    preprocessed_image = preprocessed_image.transpose((2,0,1))
    preprocessed_image=preprocessed_image.reshape(1, 3, 256, 456)
    print('Shape: {}'.format(preprocessed_image.shape))
    print(preprocessed_image)

    return preprocessed_image
```

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

```python
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

```python
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

```python
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

```python
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

 ```python
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

```python
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

```python
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

```python
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
> `from handle_models import handle_output, preprocessing` - this imports handle_output and preprocessing functions from handle_models.py file.
>
> `from inference import Network` - this imports Network class from inference.py file.
>
> `CAR_COLORS = ["white", "gray", "yellow", "red", "green", "blue", "black"]`  
> `CAR_TYPES = ["car", "bus", "truck", "van"]` - defines these arrays for labeling car colors and car types of output on vehicle-attributes-recognition-barrier-0039 pre-trained model

There are two parts having a defined starting point for the execution of a program called main function.

```python
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

```python
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

```python
# -- Create the descriptions for the commands

c_desc = "CPU extension file location, if applicable"
d_desc = "Device, if not CPU (GPU, FPGA, MYRIAD)"
i_desc = "The location of the input image"
m_desc = "The location of the model XML file"
t_desc = "The type of model: POSE, TEXT or CAR_META"
```

The next few lines are configuring the argument groups for showing the help messages when running with `-h` or `--help` argument.

```python
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

```python
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

```python
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

```python
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

```python
  ### TODO: Preprocess the input image
  preprocessed_image = preprocessing(image, h, w)
```

> `preprocessed_image = preprocessing(image, h, w)` - The `preprocessed_image` variable name comes from the next code  `inference_network.sync_inference(preprocessed_image)`. The `preprocessing` function is defined `handle_models.py`.  
> The` preprocessing` function takes `image` as a input image (from the privious line `image = cv2.imread(args.i)`) with image hight and width, `h` and `w` (`n, c, h, w = inference_network.load_model(args.m, args.d, args.c)` function actually returned).

The next TODO is about processing the output of the pre-trained model. Accroding to the Note suggestion, it uses handle_output function which returns the correct output handling function by feeding in the model type, `args.t`. The second line sends the output of inference and image shape to `output_function`.

```python
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

```python
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
```python
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

```python
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

```python
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

```python
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

```python
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

```python
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

```python
# Remove final part of output not used for heatmaps
output = output[:-1]
```

{::options parse_block_html="false" /}

The final part of output is about background.

{% include helpers/image.html name="POSE-output-background.png" %}

{::options parse_block_html="true" /}

code

```python
# Change output[:-1] to output[-1:] to extract only the last element
output = output[-1:]
```

</details>

{::options parse_block_html="false" /}
<br>

Create new ndarray for output using input shape and keypoint heatmaps.

```python
  # TODO 2: Resize the heatmap back to the size of the input
  # Create an array of zeros
  processed_output = np.zeros([heatmaps.shape[1], input_shape[0], input_shape[1]])
```

Resize each ndarray using for loop. `cv2.resize` function only takes dimensions of 1 or 3 for the channels which is usually color or grayscale image. In our case, there is 19 of these layers.

```python
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

```python
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

```python
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

```python
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
```python
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

```python
# omitted ...
    # Get the color and car type from their lists
        color = CAR_COLORS[output[0]]
        car_type = CAR_TYPES[output[1]]
# omitted ...
```

So it is reasonable to get rid of unnecessary dimensions. The argmax suggests to use argmax function to get the indices of the maximum values.

```python
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

Make sure to click the button below before you get started to source the correct environment.

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

<details>
<summary>log</summary>

<pre>
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
</pre>
</details>

As you see at the end of the log, the TensorFlow Model, the SSD MobileNet V2 COCO model sucessfully converts the Intermediate Representation (IR) model for OpenVINO Toolkit.

```
# omitted...
[ SUCCESS ] Generated IR model.
[ SUCCESS ] XML file: /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/./frozen_inference_graph.xml
[ SUCCESS ] BIN file: /home/workspace/ssd_mobilenet_v2_coco_2018_03_29/./frozen_inference_graph.bin
[ SUCCESS ] Total execution time: 89.62 seconds.
```

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
