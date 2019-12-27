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

first, press SOURCE ENV button (to source the correct environment).

<details>
<summary>log</summary>

<pre>
root@a2c7959d88c3:/home/workspace# pip install requests pyyaml -t /usr/local/lib/python3.5/dist-packages && clear && source /opt/intel/openvino/bin/setupvars.sh -pyver 3.5Collecting requests  Downloading https://files.pythonhosted.org/packages/51/bd/23c926cd341ea6b7dd0b2a00aba99ae0f828be89d72b2190f27c11d4b7fb/requests-2.22.0-py2.py3-none-any.whl (57kB)
    100% |████████████████████████████████| 61kB 2.6MB/s
Collecting pyyaml
  Downloading https://files.pythonhosted.org/packages/8d/c9/e5be955a117a1ac548cdd31e37e8fd7b02ce987f9655f5c7563c656d5dcb/PyYAML-5.2.tar.gz (265kB)
python_version = 3.5
[setupvars.sh] OpenVINO environment initialized
(venv) root@a2c7959d88c3:/home/workspace#
</pre>
</details>

> Using the [Pre-Trained Model list](https://software.intel.com/en-us/openvino-toolkit/documentation/pretrained-models), determine which models could accomplish the following tasks (there may be some room here in determining which model to download):

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

In the first documentation page of each model, the ttitle at the top of the page is the model name to use for downloading. Below example image of Human Pose Estimation shows the name, human-pose-estimation-0001.

{% include helpers/image.html name="Screen Shot 2019-12-27 at 21.25.19.png" %}

Using [downloader.py](http://docs.openvinotoolkit.org/latest/_tools_downloader_README.html) and options specifing precision levels, download the models.

First, go to the openvino downloader directory:

```
# cd /opt/intel/openvino/deployment_tools/open_model_zoo/tools/downloader
```

> cd - command changes directories

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

> --name human-pose-estimation-0001 - --name option specifies the identifier of the model for downloading (this case, human-pose-estimation-0001)
>
> -o /home/workspace - -o option specifies the output directory

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

> --name text-detection-0004 - choosing text-detection-0004 model
>
> --precisions FP16 - --precisions flag to specify precision. By default, the script will produce models in every precision that is supported for conversion.

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
you should see three directories - one for each downloaded model (human-pose-estimation-0001, text-detection-0004, and vehicle-attributes-recognition-barrier-0039) with listing command `ls -l`.

```
# ls -l
```

> ls -l - ls command to lists files and directories within the current directory. With the -l option, ls will list out files and directories in long list format.

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
Within those directories, there should be separate subdirectories for the precisions that were downloaded, and then .xml and .bin files within those subdirectories, that make up the model. `tree` command will you to check those more easily.

```
# tree
```

> tree - command to display the content of a directory in a tree-like format

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

<br>
