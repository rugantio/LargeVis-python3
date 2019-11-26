# LargeVis-python3
LargeVis graph visualization algorithm port to python3

## Achtung!
This software has not been tested on Windows and MacOS.
The included build is for Linux x64, however I suggest to make your own binary (is fast!)


## Introduction
This project is a fork of the python2 implementation of the [LargeVis](https://github.com/lferry007/LargeVis) algorithm for graph drawing, provided by the authors of the paper, [Visualizing Large-scale and High-dimensional Data](https://arxiv.org/abs/1602.00370) and currently unmaintained.

The main scope of this project is to keep this software available also to python3 users (Windows, Mac and Linux) through a simple python package, while still maintaining python2 compatibility.

A future aim of the project is to facilitate the integration of LargeVis with more popular, front-end based, graph visualization software, which often struggle to draw large graph (such as [Gephi](https://github.com/gephi/gephi)).

If you are looking into large networks, you might want to check out [trimap](https://github.com/eamid/trimap), which has provided interesting benchmarks in its release paper [TriMap: Large-scale Dimensionality Reduction Using Triplets
](https://arxiv.org/abs/1910.00204), claiming to surpass LargeVis in some applications.

Other popular graph drawing for large graphs are [t-SNE](http://www.jmlr.org/papers/volume9/vandermaaten08a/vandermaaten08a.pdf), available through the [author's own website](https://lvdmaaten.github.io/tsne/) and provided also in [scikit-learn](https://scikit-learn.org/stable/modules/generated/sklearn.manifold.TSNE.html). Another recent algorithm is [UMAP](https://arxiv.org/abs/1802.03426), also [available in python](https://github.com/lmcinnes/umap) thanks to the paper's author; further readings about UMAP and SNE can be found [here](https://jlmelville.github.io/uwot/umap-for-tsne.html).

Most of these algorithms have larger support and community in their R implementations. A project that collects different techniques in a single R library is [smallvis](https://github.com/jlmelville/smallvis).

## Dependencies
LargeVis is written in C++ using the BOOST library and GSL (GNU Scientific Library).

Python is used only to interface with the C++ routines and to draw the final plot. 

## Installing
Refer to the [original official repo](https://github.com/lferry007/LargeVis) for instructions not mentioned here and further info.

* clone this repo and cd into the platform directory (Linux or Windows)
* follow the compiling instructions in the official repo, for Linux is enough to launch 

```
    g++ LargeVis.cpp main.cpp -o LargeVis -lm -pthread -lgsl -lgslcblas -Ofast -march=native -ffast-math
```

* if compilation succeeds, install the python package locally using the setupy.py - since it's a local install I suggest to record in a txt files the dirs created, with:

```
    sudo python setup.py install --record files.txt
```

* check that the lib was installed properly. Open a python interpreter and type

```
    import LargeVis
```

the interpreter should reply with `LargeVis successfully imported!`.

## Uninstalling
If you installed using the procedures, you can remove all the files create by setup.py with:

```
    sudo xargs rm -rf < files.txt
```

## Usage
LargeVis can be used inside the Python environment - check out the LargeVis() class.

Also LargeVis can be executed through a simple script, such as the `LargeVis_run.py` provided with the repo.

You can try it out and confirm that is working correctly, with the example datasets of this repo. For example to try visualizing the MNIST dataset try:

```
python LargeVis_run.py -input mnist_vec784D.txt -output mnist_vec2D.txt -threads 8 -fea 1
```

## Improvements and changes
* The input data can now also be loaded in LargeVis through a numpy array
* the `-fea` parameter defaults to 0 (networks) and not 1 (vectors).


## Help and Contribute
* Test the code on Windows / MacOS
* Enlarge this library to include other viz algos
* Clever initialization of hyperparameters needed (AutoML anyone?)
* Export this package to pip
* Create a Qt frontend for graph visualization (would love this soo much)