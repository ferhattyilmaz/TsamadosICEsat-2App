# Thoughts on ICEsat-2 for cloud detection trianing


## Why this project?
It was difficult to pick one out of the 3 projects offered as all 3 were very interesting, but I would like to apply for the cloud detection project for the following reasons:

This is an unsupervised learning project and when choosing any project which relies on machine/deep learning, it is imperative to first determine the quality and quantity of the dataset we wish to work with. A brief look at the data products <sup>[1](#1)</sup> that the ATLAS instrument outputs from ICEsat-2; specifically the relevant datasets for this project which are profiles of atmospheric backscatter: ATL04 <sup>[2](#2)</sup> (Normalised backscatter profiles) and ATL09 <sup>[3](#3)</sup> (Calibrated backscatter profiles) showed that quantity would not be an issue as there is a combined 23TB of data available to use or train on (subject to test/train splits). In addition to this, the data is well organised and known issues are well documented and the low-level HDF5 files are also available.

I am also drawn to this project due to the potential applications of it which are many. The most apparent is an additional method for cloud prediction (supporting predictions from optical satellite imagery). Cloud cover often disturbs analyses (e.g. when using other data products like ATL06) and checking whether if the disruption is caused by cloud cover or not seems to be standard procedure <sup>[*](*)</sup>, and there may be some space for automating this process (which is another application of this project).

Finally atmospheric physics is something that we as undergrad physics students did not get an opportunity to study, so the idea of applying prior knowledge to  (as of yet) unfamiliar domains is a challenge that I look forward to!

## The research problem and my skill set

Although the project summary was a little light on detail, here is my understanding of the project:

Advanced Topographic Laser Altimeter System (ATLAS) provides [altimetry](http://www.altimetry.info/radar-altimetry-tutorial/how-altimetry-works/) data from the ICEsat-2. The low-level binary data are transferred from ATLAS several times a day to a data centre in Alaska which are then converted to more useful formats for analyses. The dataset that would be relevant for this project are ATL09 and ATL04 which contain signals picked up with the atmospheric channels of ICEsat-2 (atmospheric backscatter). From this dataset it is possible to determine whether or not a cloud was present using an estimate for the “apparent surface reflectivity”. There are two flags present in the dataset: cloud_flag_ASR and cloud_flag_atm, the former is preferred (as mentioned in [docs](https://icesat-2.gsfc.nasa.gov/sites/default/files/files/ATL09_Layer_Parameters.pdf)) in daylight conditions and the latter for night. There is also a confidence level associated with the flags ranging from 0-5 (with meaning clear with high/med/low confidence to cloud with low/med/high confidence). It is possible to use this as training data to feed into a deep neural network (CNN or LSTM) which can detect whether there was cloud/no cloud. It may also be possible to take it one more step and identify whether the cloud is thin or thick.

The following python libraries will be useful in the project:
+ SciPy ecosystem (Numpy, Scipy, Pandas etc...) 
+ Sklearn <sup>[4](#4)</sup>
+ icepyx <sup>[5](#5)</sup> 
+ Keras (with tflow backend) or pytorch <sup>[6](#6)</sup> (using CUDA; I found the setup for this to be difficult)

With the exception of icepyx (which is quite specific to this project and I hope to learn to use) I have prior experience with all the packages listed above (in prior machine learning module/ physics modules and personal mini projects I have mentioned in my academic CV) which will be useful. I also believe that UCL Myriad <sup>[7](#7)</sup> could be something to look into, especially due to its tensorflow capabilities (subject to access).

## References

<a name="1">1</a>: https://nsidc.org/sites/nsidc.org/files/images/icesat-2-prod-map-rev.png 

<a name="2">2</a>: https://nsidc.org/data/ATL04 

<a name="3">3</a>: https://nsidc.org/data/ATL09/versions/3

<a name="4">4</a>: https://www.scipy.org/docs.html

<a name="5">5</a>: https://icepyx.readthedocs.io/en/latest/

<a name="6">6</a>:https://pytorch.org/docs/stable/index.html

<a name="7">7</a> https://www.rc.ucl.ac.uk/docs/Clusters/Myriad/#tensorflow

<a name="n">*</a>: I found this as a very useful introduction to the datasets and the functions of ICEsat-2 https://www.youtube.com/watch?v=0guml7ihfdA

