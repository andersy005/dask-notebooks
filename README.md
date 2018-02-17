<img src="https://i.imgur.com/M3BRrh1.png" align="right" width="30%">

# Dask Python Notebooks

This is a collection of [**Jupyter**](https://jupyter.org/) notebooks intended to train the reader on different [Dask](https://dask.pydata.org/en/latest/) concepts, from basic to advanced.

## Overview

Dask provides multicore and distributed parallel execution on larger-than-memory datasets.

We can think of Dask at a high and a low level

- **High Level collections:** Dask provides high-level
  - Arrays
  - Bag
  - and DataFrame
 
 collections that mimic NumPy, Lists, and Pandas but can operate in parallel on datasets that don't fit into memory. Dask's high-level collections are alternatives to NumPy and Pandas for large datasets.
 
 - **Low level schedulers:** Dask provides dynamic task schedulers that execute task graphs in parallel. These execution engines power the high-level collections mentioned above but can also power custom, user-defined workloads. These schedulers are low-latency (around 1 ms) and work hard to run computations in a small memory footprint. Dask's schedulers are an alternative to direct use of `threading` or `multiprocessing` libraries in complex cases or other task scheduling systems like `Luigi` or `IPython parallel`.
 
 
Diferent users operate at different levels but it is useful to understand both.

## Basics of Dask 


The basics of dask can be summarized as follows:
- process data that doesn't fit into memory by breaking it into blocks and specify task chains.
- parallelize execution of tasks across cores and even nodes of a cluster.
- move computation to the data rather than the other way around, to minimize communication overheads.


## Distributed 

Dask comes with four available schedulers:
- `dask.threaded.get`: a scheduler backed by a thread pool
- `dask.multiprocessing.get`: a scheduler backed by a process pool
- `dask.get`: a synchronous scheduler, good for debugging
- `distributed.Client.get`: a distributed scheduler for executing graphs on multiple machines.


To select one of these for computation, you can specify at the time of asking for a result

```python
myvalue.compute(get=dask.async.get_sync)  # for debugging
```

or set the current default, either temporarily or globally

```python
with dask.set_options(get=dask.multiprocessing.get):
    # set temporarily fo this block only
    myvalue.compute()

dask.set_options(get=dask.multiprocessing.get)
# set until further notice
```

For single-machine use, the threaded and multiprocessing schedulers are fine choices. However, for scaling out work across a cluster, the distributed scheduler is required. Indeed, this is now generally preferred for all work, because it gives you additional monitoring information not available in the other schedulers. (Some of this monitoring is also available with an explicit progress bar and profiler, see [here](http://dask.pydata.org/en/latest/diagnostics.html).)


## Instructions

A good way of using these notebooks is by first cloning the repo, and then starting your own Jupyter notebook after installing all necessary packages. 


    git clone https://github.com/andersy005/dask-notebooks.git

and then install necessary packages.

### a) Install into an existing environment

You will need the following core libraries

    conda install numpy pandas h5py Pillow matplotlib scipy toolz pytables snakeviz dask distributed

You may find the following libraries helpful for some notebooks

    pip install graphviz cachey
    
### b) Create a new environment

In the repo directory

    conda env create -f environment.yml 

and then on osx/linux

    source activate dask-tutorial

on windows

    activate dask-tutorial

### c) Use Dockerfile

You can build a docker image out of the provided Dockerfile.



### Graphviz on Windows

Windows users can install graphviz as follows

1. Install Graphviz from http://www.graphviz.org/Download_windows.php
2. Add C:\Program Files (x86)\Graphviz2.38\bin to the PATH

Alternatively one can use the following conda commands (one installs graphviz and one installs python-bindings for graphviz):

1. `conda install -c conda-forge graphviz`
2. `conda install -c conda-forge python-graphviz`


## Datasets  

We will be using datasets from the [KDD Cup 1999](http://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html). The results 
of this competition can be found [here](http://cseweb.ucsd.edu/~elkan/clresults.html).  


## Notebooks  

The following notebooks can be examined individually, although there is a more
or less linear 'story' when followed in sequence. By using the same dataset
they try to solve a related set of tasks with it.

1. [**Dask Bag creation**](https://github.com/andersy005/dask-notebooks/blob/master/01-dask-bags/01-bag-creation.ipynb): About reading files and creating bags.
2. [**Dask Bag basics**](https://github.com/andersy005/dask-notebooks/blob/master/01-dask-bags/02-bag-basics.ipynb): A look at `map`, `filter`, `compute`, `persist`, `flatten`

## Contributing
Contributions are welcome!  For bug reports or requests please [submit an issue](https://github.com/andersy005/dask-notebooks/issues).

## To Do List
This section is for myself, but feel free to **fork the repo** and add your contributions!

- [ ] Add DockerFile
- [ ] Add environment.yml file
- [ ] Add Binder Support
