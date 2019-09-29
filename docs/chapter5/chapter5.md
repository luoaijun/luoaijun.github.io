##  How to publish JAR packages to Pypi?

#### Create your python project 
> In your project, you must have the following directory structure

```
.
├── LICENSE
├── README.md
├── <your project name>
│   ├── __init__.py
│   ├── xxx.py
│   ├── xxx.py
│   ├── xxx.py
│   ├── xxx.py
│   ├── xxx.py
│   └── xxx.py
├── setup.cfg
├── setup.py 
```

#### Configuration setup.cfg

```
[metadata]
description-file = README.md
```

#### Configuration __init__.py code

```
name = "KongFuPanda"  # 项目名称
```

#### Configuration setup.py

```
# -- coding: UTF-8 --
import platform
import io
from setuptools import setup, find_packages

VERSION = '1.0.0'

requires = ['six', 'pynput']
with io.open("README.md", "r", encoding="utf-8") as fh:
    long_description = fh.read()
system = platform.system()
if system == 'Darwin':
    requires.append('pyobjc-framework-Quartz')

setup(
    name='KongFuPanda',  # 指定包名
    version=VERSION,  # 指定版本号
    description='Framework for Advanced Statistics and Data Sciences',  # 一句话描述，
    long_description='Framework for Advanced Statistics and Data Sciences.',  # 详细介绍
    keywords='knn ml svm tree NaiveBayes AdbBoost',  # 关键字
    author='luoaijun',  # 作者
    author_email='3191287315@qq.com',
    maintainer='luoaijun',
    maintainer_email='3191287315@qq.com',
    url='https://github.com/luoaijun/MachineLearning.git',  # 项目目录
    packages=find_packages(),
    include_package_data=True,
    zip_safe=True,
    install_requires=requires,  # 上层依赖的包
    classifiers=[
        # 'Development Status :: 1 - Planning',
        # 'Development Status :: 2 - Pre-Alpha',
        # 'Development Status :: 3 - Alpha',
        # 'Development Status :: 4 - Beta',
        # 'Development Status :: 5 - Production/Stable'
        'Development Status :: 5 - Production/Stable',  # 当前开发进度等级（测试版，正式版等）
        'Intended Audience :: Developers',  # 模块适用人群
        'Topic :: Software Development :: Code Generators',  # 给模块加话题标签
        'License :: OSI Approved :: MIT License',  # 模块的license

        'Programming Language :: Python :: 3',
        'Programming Language :: Python :: 3.4',
        'Programming Language :: Python :: 3.5',
        'Programming Language :: Python :: 3.6',
        'Programming Language :: Python :: 3.7',
    ],
    project_urls={  # 项目相关的额外链接
        'github.io': 'https://luoaijun.github.io/self',
    },
)

```

#### Create. pypirc under the user directory

```
[distutils]
index-servers =
  pypi 

[pypi]
repository = https://upload.pypi.org/legacy/
username=your pypi username
password=your pypi username's password

```

#### Execute commands after switching to setup.py peer directory


```
# First install the upload tool
pip3 install -U pip setuptools twine

# packages
python3 setup.py sdist  # This command packages the project under the current directory and generates the corresponding egg

# upload
twine upload dist/*     # It's actually the zip package in the uploaded dist directory

``` 
