---
title: Python Dev Stack
author: tusharm
type: post
date: '2018-06-09'
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

This is useful in cases like when my sister wanted some data manipulation scripts. I could've written a python script in vim and shared it, but it wouldn't make sense to her and even me later when I might want to revisit this (I'm learning a lot of new stuff and need to reference a lot of tricks to do things in python).

Kaggle allows me to write python in a browser while documenting things around my code in markdown. This can help me better explain the code to the user.

This service is more prominently used to work on datasets and so they provide efficient data upload and download services for the notebooks. It's made to test the notebook with sample data during development but when I need to run the code on an optimized hardware (on any sort of compute unit including serverless functions), it would be helpful to export the notebook in a runnable format.

Easy enough, Kaggle supports a download button for ipynb version of the notebook.

Converting to python is a single command, but you might need to install some stuff.

```
sudo pip install jupytersudo pip install nbconvert
```

Then export a python executable version of notebook.

```
jupyter nbconvert --to python notebook.ipynb
```

The above command creates a notebook.py file. However this script expects a structure.

```
.
```

```
├── input
```

```
│   ├── file1.txt
```

```
│   ├── file2.txt
```

```
│   └── file3.txt
```

```
└── src
```

```
    ├── notebook.py
```

```
    ├── output_1.csv
```

```
    └── output_2.csv
```
