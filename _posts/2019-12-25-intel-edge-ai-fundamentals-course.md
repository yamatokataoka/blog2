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

# Leveraging Pre-Trained Models
## Loading Pre-Trained Models
The models are available in OpenVINO™ as pre-trained models like:

- Text Detection

- Pose Detection

- Roadside Segmentation

- Pedestrian Detection

You can check out the full list of pre-trained models available in the Intel® Distribution of OpenVINO™ [here](https://software.intel.com/en-us/openvino-toolkit/documentation/pretrained-models).

On the [Intel® Edge AI Fundamentals Course](https://www.udacity.com/scholarships/intel-edge-ai-scholarship), you can see this workspace.

{% include helpers/image.html name="Screen Shot 2019-12-25 at 22.35.27.png" %}

## Find the Right Models

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

## Download the Models

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
ools/downloader# ls -ltotal 292
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

## Verify the Downloads

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

> `ls -l` - ls command to lists files and directories within the current directory. With the -l option, ls will list out files and directories in long list format.

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

# Preprocessing Inputs

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

## Human Pose Estimation

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

## Text Detection

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

## Determining Car Type & Color

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

## Solution: Pre-processing Inputs

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
<summary>The Solution Code</summary>

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

# Deploy Your First Edge App

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

## TODOs

You will implement the handling of the outputs of our three models on `handle_models.py`.

Notice that there are two TODOs for each handle function to determine the each output on the first three functions.

The 4th function, named `handle_output` is the function returns one of the above three functions to handle an output, based on the `model_type` being used.

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

    return output


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

    return output
```

Check what is exactly the output type to extract the second blob which contains keypoint heatmaps.

For checking the data type, implement `app.py` first, because the `handle_pose` function calling from `app.py` is much more easier for debugging.

## app.py

Let's have a close look at the the first part of the `app.py` to understand the basic structure of the code and how should you implement TODOs.

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
