---
layout: post
title: Moving from Conda to Python Virtual Environments
date: 2025-08-16 12:00:00
description: Moving from Conda to Python Virtual Environments. (AI translation version from the Arabic version - reviewed).
tags: Virtual environments
categories: #Virtual environments
thumbnail:
align: lft
dir: ltr
images:
  compare: true
  slider: true
---

Anaconda has updated its license terms in March 2024, and the updates began to be effectively applied since mid-July 2025. These updates have created a fundamental shift for research institutions, government organizations, and companies that have more than 200 employees. While Anaconda exempts companies with number of employees equal to or less than a threshold of 200 employee and excludes educational institutions that use its products within thier educational curricula (for teaching and learning), it requires others to purchase the required license, including research uses or any use outside the scope of education in educational institutions. As a result, many engineers and researchers looked for alternatives to maintain data and information flow and thus maintain workflow and productivity.

Although the open-source Conda tool is still available for free use by everyone, using the default channel (Conda's default channel) to install libraries is subject to the usage terms applied to Anaconda in terms of the necessity of purchasing a license for use by companies, entities, and institutions whose number of employees exceeds the 200-employee threshold. As solutions to these requirements, the Conda tool can be used with the open-source community channels like conda-forge to install libraries. Additionally, alternative distributions to conda such as Miniforge or Mamba can be installed, which are not subject to the commercial licensing.

The problem with these channels is that they do not enjoy the protection and security advantages provided by managed and supported packages from Conda's default channel. Although there is debate about the impact of this on user data and the reliability of open-source packages, data protection remains sensitive for companies and institutions that care about protecting their data and avoiding the use of tools that are not reviewed or managed by trusted entities like Anaconda.

In this space, I would like to present an available alternative that avoids or at least reduces the drawbacks of community channels from Conda, which is using virtual environments directly using Python. These are the same steps I followed to transition from Conda to environments from the base version of Python.

First, it's better to copy the existing environments on your device from Conda. To do this, you need to activate the virtual environment, then extract the packages/libraries that were installed in that virtual environment. After copying these packages, Anaconda can be completely removed, and all files associated with it can be removed from your device.

After that, you can install the required version of Python from the official website (https://www.python.org/). While the ideal case is installing the latest version to benefit from the latest security updates and improvement advantages, previous versions can be chosen if they are compatible with necessary packages or libraries for work. Multiple versions can also be installed on the device. In this example, we installed two versions of Python: Python 3.13.7 and Python 3.11.0. To know the default version on the device, from the Command Prompt (cmd), you can enter the command python -V, while to use the other version, you need to use the full path, as shown in the following command:

```shell
C:\PYTHON_INSTALLATION_PATH\Python\Python311\python.exe -V
```

Following the same method, you can create the required virtual environment. For example, to create a virtual environment based on Python 3.13 and name it venv_3.13, we will write the following command in the command prompt:

```shell
python -m venv venv_3.13
```

To create a virtual environment based on Python 3.11 and name it venv_3.11, we will enter the command in the command prompt (replacing PYTHON_INSTALLATION_PATH with the path used to install Python 3.11 version):

```shell
"C:\PYTHON_INSTALLATION_PATH\Python\Python311\python.exe" -m venv venv_3.11
```

Please note that the created environment will be created in the folder where the command pointer is located, so attention should be paid to ensure the pointer is in the intended folder, and it can be in the root folder of the project. In this case, the folder should be added to the folders that are ignored if the project is within version control system tools like GitHub.

To activate the created environment, you can enter the following command:

```shell
venv_3.13\Scripts\activate
```

To verify the Python version used in the activated environment, we enter the following command:

```shell
python -V
```

We will notice that the Python version in the version specific to the activated environment is version 3.13.7.

You can then use the pip library to install the required packages and libraries.

To deactivate the virtual environment, you can write the command:

```shell
deactivate
```

And the virtual environment will be deactivated.

While managing virtual environments in this method does not provide all the advantages of Conda in managing packages, libraries, and dependencies, you can use additional open-source tools to bridge this gap, such as:

- `pip-tools`: A tool for installing and managing dependencies precisely with version pinning.
- `Poetry`: An integrated package and environment manager for Python that combines virtual environment creation, dependency management, and project building for deployment.
- `virtualenvwrapper`: A tool for easily managing multiple virtual environments from the command prompt.
