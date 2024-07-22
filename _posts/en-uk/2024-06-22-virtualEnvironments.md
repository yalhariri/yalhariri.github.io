---
layout: post
title: Adding Virtual Environment
date: 2024-06-22 12:00:00
description: Adding virtual environment with specific version of Python.
tags: Virtual environments 
categories: #Virtual environments 
thumbnail:
align: lft
dir: ltr
images:
  compare: true
  slider: true
---


In this article, I will explain how to avoid the limitations associated with creating a virtual environment using a specific version of Python, particularly when root privileges are unavailable for installing that version. This guidance is essential for those needing to work within constrained software environments. This article provides useful steps to solve the failure of the following command:

```
python3.8 -m venv venv
```

This approach is particularly important for objectives such as avoiding libraries' compatibility issues. The solution I discuss involves using a conda virtual environment with the desired version of Python. If conda is not already installed on your system, it can be downloaded from the Conda website[https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html]. For the purposes of this example, Python version 3.8 is required.

```
conda create -n temp python=3.8
```

After creating the conda environment, we need to activate it:

```
conda activate temp
```

Next, we need to install the virtual environment library:

```
pip install virtualenv
```

By completing this step successfully, we can use the library (virtualenv) with Python3.8 version to create the new virtual environment (venv) in the system as follows:

```
virtualenv -p $(which python3.8) venv
```

Next, we need to deactivate the conda virtual environment, temp, and then activate the newly created virtual environment (venv).

```
conda deactivate
source venv/bin/activate
```

Now, to test the Python version in the virtual environment, we use the following command:
```
python --version
```

The expected output is something similar to the following:
```
Python 3.8.##
```

Where the 'hashes' refer to the Python's patch version number. To ensure that the current Python version is in the virtual environment (venv) and not located in another path, use the following command:
```
which python
```

The output should include the folder, where (venv) is the name of the virtual environment:
```
./venv/bin/python
```

By reaching this, we have successfully created a virtual environment with specific version of Python without having it installed in the system, and without having the root access priviligies to install that version of Python in the system.