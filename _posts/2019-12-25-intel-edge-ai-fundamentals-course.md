---
layout: post
title: Intel® Edge AI Fundamentals Course
---

This is a complete guide to walk through Intel® Edge AI Fundamentals Course. Especially, this focuses on the Exercise sections. The Intel® Edge AI Fundamentals Course is the first phase of the Intel® Edge AI Scholarship Program for skills in Intel® Distribution of OpenVINO™ toolkit fundamentals.

# Prerequisites
- Work on Intel® Edge AI Fundamentals Course on [Intel® Edge AI Scholarship Program](https://www.udacity.com/scholarships/intel-edge-ai-scholarship) or [Intel® Edge AI for IoT Developers Nano degree](https://www.udacity.com/scholarships/intel-edge-ai-scholarship)

# Goal
Finish Intel® Edge AI Fundamentals Course sucessfully.

# Play around with Pre-Trained Models
## Pre-Trained Models
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

Once you have found the models, download them into the workspace with the precision levels:

- Human Pose Estimation: All precision levels

- Text Detection: FP16 only

- Determining Car Type & Color: INT8 only
