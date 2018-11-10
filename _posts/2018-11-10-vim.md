---
title: "Deep Learning Setup with Python3: CPU Only"
layout: post
date: 2018-11-10
tags: blog
comments: true
---
*Working on Ubuntu 16.04 (Only CPU) with Python3*

###### Update the Repository:
{% highlight unix %}
sudo apt-get update
{% endhighlight %}

###### Install scipy Stack
{% highlight unix %}
sudo apt-get install -y python3-numpy python3-scipy python3-nose python3-h5py python3-skimage python3-matplotlib python3-pandas python3-sklearn python3-sympy
{% endhighlight %}

{% highlight unix %}
sudo apt-get install -y python3-dev python3-pip g++ python3-pygments python3-sphinx libjpeg-dev zlib1g-dev
{% endhighlight %}

{% highlight unix %}
sudo pip3 install matplotlib ipython[all] jupyter pandas scikit-image
{% endhighlight %}

###### Install Theano and Keras from PyPI
{% highlight unix %}
sudo pip3 install theano
sudo pip3 install keras
{% endhighlight %}

*Add specific instructions to .theanorc file, to avoid a glibc bug:*
{% highlight unix %}
echo -e "\n[nvcc]\nflags=-D_FORCE_INLINES\n" >> ~/.theanorc
{% endhighlight %}

###### Install CPU-only version of Tensorflow
{% highlight unix %}
sudo pip3 install --upgrade https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.9.0-cp35-cp35m-linux_x86_64.whl
{% endhighlight %}

###### Verify the installation by importing them in python3:
{% highlight unix %}
python3
>>> import tensorflow
>>> import theano
>>> import keras
>>> exit()
{% endhighlight %}
