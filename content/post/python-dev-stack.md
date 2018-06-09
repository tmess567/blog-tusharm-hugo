---
title: Python Dev Stack
author: tusharm
type: post
date: '2018-06-09'
image: /wp-content/uploads/wallhaven-342160.jpg
categories:
  - kaggle
  - python
tags:
  - kaggle
  - python
  - ipython
  - jupyter
  - notebook
  - exectuable
  - development
---
Running and benchmarking python is easier if you have a standard place to run and share them. Kaggle fits this profile perfectly. It is a hosted service for your code which can be run and shared online.

## Developing in Cloud

Kaggle allows me to write python in a browser while documenting things around my code in markdown. This can help me better explain the code to the user.

This is useful in cases like when my sister wanted some data manipulation scripts. I could've written a python script in vim and shared it, but it wouldn't make sense to her and even I would be confused later when I might want to revisit this (I'm learning a lot of new stuff and need to reference a lot of tricks to do things in python).

https://www.kaggle.com/tusharm567

As an added advantage, I get direct access to loads of public datasets to play and sharpen my skills on.

## Benchmarking Code

```
from math import *
%timeit tan(atan(exp(log(sqrt(1*1)))))
```

This kind of stuff is helpful while learning and testing out algorithms and/or comparing different approaches to a solution based on compute.

You can also time an entire cell of code while running multiple iterations to make sure the machine is warmed up.

```
%%timeit 
```

Or maybe you wanna check the profiler output.

```
%prun my_func(100)
```

Sometimes it's not about compute, but all about the memory

```
def large_mem(count):
    a = []
    for i in range(count):
        a.append(i)
        
%memit large_mem(100000000)
```

```
peak memory: 4121.68 MiB, increment: 3838.79 MiB
```

> Reference: https://jakevdp.github.io/PythonDataScienceHandbook/01.07-timing-and-profiling.html

## Running in Production

This service is prominently used to work on datasets and so they provide efficient data upload and download services for the notebooks. It's made to test the notebook with sample data during development but when I need to run the code on an optimized hardware (on any sort of compute unit including server-less functions), it would be helpful to export the notebook in a runnable format.

Easy enough, Kaggle supports a download button for ipynb version of the notebook.

Converting to python is a single command, but you might need to install some stuff.

```
sudo pip install jupyter
```

```
sudo pip install nbconvert
```

Then export a python executable version of notebook.

```
jupyter nbconvert --to python notebook.ipynb
```

The above command creates a notebook.py file. However this script expects a structure. The structure below includes the output files generated after running the script from inside src.

```
|-- input
|   |-- file1.txt
|   |-- file2.txt
|   |-- file3.txt
|-- src
    |-- notebook.py
    |-- output_1.csv
    |-- output_2.csv
```
