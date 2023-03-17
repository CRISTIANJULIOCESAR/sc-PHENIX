# sc-PHENIX Imputation 


### What is sc-PHENIX

 sc-PHENIX was developed to improve imputation of scRNA-seq data avoiding over-smoothing; it falls into the category of smooth-based imputation based on benchmarking. However, the methods used in sc-PHENIX to obtain the low dimensional manifold is UMAP(*Uniform Manifold approximation and Projection*), and the **M<sup>t</sup>** (exponentiated Markov matrix) is from diffusion maps, both techniques based on manifold learning being part of the nonlinear dimensionality reduction methods category, a subfield of machine learning. In this work, our approach is an improvement to the popular method MAGIC by integrating UMAP in the imputation process. Consequently, there is an improvement in the computation of **M<sup>t</sup>** reflecting the denoised cell-neighborhood that captures local, continuum and global data structures. The advantage of  preserving data structures with sc-PHENIX compared to MAGIC is that we can share gene expression among more accurate nearest neighbors cells on the manifold of **M<sup>t</sup>** sc-PHENIX. Following these procedures, we obtain more biological insights and at the same time mitigate the risk of over-smoothing data among spurious distinct cell phenotypes.

### What you need to know first

The user needs to have knowledge of how to use of pandas and numpy libraries, this implies that the user has python knowledge. Any free course, cursera or udeamy course can be used to learn faster this python libraries, for recent users please go in here  [click here](https://www.udemy.com/share/101WaU3@3A6uj9QXHRFfZxf59mg8aLG7J1eXrfzT5RKo5SO1VRl9RxsqCEINIxSf67WH3GsG/) to learn the basics.

sc-PHENIX is based mainly of the use of UMAP, more information of how to use UMAP please [click here](https://umap-learn.readthedocs.io/en/latest/index.html). Please keep in mind that we suggest that n_components  (UMAP dimensions) can be set for more than 3 in a non-visual manner to capture better data structure for the diffusion process.  

The important parameters for sc-PHENIX function are:

`knn` and `decay`: For the adaptive kernel to construct the Markovian matrix, the user chooses a `knn` value that is the number of nearest neighbors from which to compute kernel bandwidth. The parameter `decay` is the decay rate of kernel tails. For small datasets we recommend a set knn value sufficient to avoid over-smoothing to other clusters but not too small to alter the connectivity of data as a graph.

`t` : For the diffusion process, the parameter t (diffusion time) is the power
value to which the Markovian matrix is powered. This sets the level of
diffusion.

The `knn` and `t` values need to be sufficient to build a complete graph (considering the class) and less to avoid over-smooth taxa to other distinct classes.


plase make sure if you want to use on colab download and install umap 


## 1) install umap
put this in a colab cell and run it to pip install UMAP! from [click here](https://umap-learn.readthedocs.io/en/latest/supervised.html). 
```python
!pip install umap-learn
```
## 2) import libraries
then in other cell import the libraries to connect our github to the colab and pandas and visualization (use the visualization that you want)
```python
import requests
import os
import urllib.request
import pandas as pd
import numpy as np
import seaborn as sns
```
## 3) download sc-PHENIX python script 

in other cell download sc-phenix
```python
url_sc_phenix = 'https://raw.githubusercontent.com/resendislab/sc-PHENIX/main/sc-PHENIX%20tutorial%20colab/sc_PHENIX.py'
urllib.request.urlretrieve(url_sc_phenix, 'sc_PHENIX.py')
os.listdir()
!cd /content
!ls
```
## 4) import sc-PHENIX and reduces dimensionality with PCA 
then in other cell import sc-phenix 
```python
from sc_PHENIX import run_pca, sc_PHENIX
pca_data= run_pca(data,n_components=500, random_state=1)
```

## 5) import umap and reduce PCA space into a UMAP space
```python

import umap
#umap parameters we reduced the 500 PCA dimensions to 50 umap dimensions
fit = umap.UMAP(n_components=50,n_neighbors=10,verbose= True,metric='cosine',random_state=42)
%time u_no_3 = fit.fit_transform(pca_data) #u_no_3 variable is the 50 umap dimenions coordinates for sc-PHENIX
#the default output from UMAP is a euclidean interpretable space, but can be changed.
```

## 6) impute with sc-PHENIX
```python
neuro_phenix = sc_PHENIX(data, u_no_3,t=15,metric='euclidean',knn=15,decay=500)
neuro_phenix
```


sc-PHENIX is available in colab [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/resendislab/sc-PHENIX/blob/main/sc-PHENIX%20tutorial%20colab/sc_PHENIX_try_me_example.ipynb)
