# sc-PHENIX
# sc-PHENIX Imputation  (2022; Code for paper)


### What is sc-PHENIX

 sc-PHENIX was developed to improve imputation of scRNA-seq data avoiding over-smoothing; it falls into the category of smooth-based imputation based on benchmarking. However, the methods used in sc-PHENIX to obtain the low dimensional manifold is UMAP(*Uniform Manifold approximation and Projection*), and the M<sup>t (exponentiated Markov matrix) is from diffusion maps, both techniques based on manifold learning being part of the nonlinear dimensionality reduction methods category, a subfield of machine learning. In this work, our approach is an improvement to the popular method MAGIC by integrating UMAP in the imputation process. Consequently, there is an improvement in the computation of Mt (exponentiated markov matrix) reflecting the denoised cell-neighborhood that captures local, continuum and global data structures. The advantage of  preserving data structures with sc-PHENIX compared to MAGIC is that we can share gene expression among more accurate nearest neighbors cells on the manifold of Mt sc-PHENIX. Following these procedures, we obtain more biological insights and at the same time mitigate the risk of over-smoothing data among spurious distinct cell phenotypes.

### What you need to know first

The user needs to have knowledge of how to use of pandas and numpy libraries, this implies that the user has python knowledge. Any free course, cursera or udeamy course can be used to learn faster this python libraries, for recent users please go in here  [click here](https://www.udemy.com/share/101WaU3@3A6uj9QXHRFfZxf59mg8aLG7J1eXrfzT5RKo5SO1VRl9RxsqCEINIxSf67WH3GsG/) to learn the basics.

mC-PHENIX is based mainly of the use of UMAP, so the abundance matrix need to be transformed into a lower dimensional space using UMAP if data has no cluster strucutre please use UMAP in supervised manner(needs label information controls and cases for example in integers), more information in here [click here](https://umap-learn.readthedocs.io/en/latest/supervised.html). 



###How to use
The input for the funcion mb-PHENIX are objects pandas or numpy object from the abundance matrix and the UMAP output, in the example of the image showed below are count matrix for the abundance matrix, data_umap_vis_super for the UMAP output.
==============================

!![myimage-alt-tag](https://github.com/resendislab/sc-PHENIX/blob/main/Screen%20Shot%202022-06-13%20at%2015.03.13.png)


Citation: 

```
@article{sc-PHENIX,
  author={Padron-Manrique Cristian, Vázquez-Jiménez Aarón, 
  Esquivel-Hernandez Diego Armando,
  Martinez Lopez Yoscelina Estrella, Neri-Rosario Daniel, 
  Sánchez-Castañeda Jean Paul, Giron-Villalobos David,  
  Resendis-Antonio Osbaldo},
  
  
}

```
### What is sc-PHENIX

SThis software was developed to improve imputation of sparse data avoiding over-smoothing. Therefore, our method captures local, global, and continuum structure of data. There is always some inherent danger in over-smoothing the data by running dimensional reduction techniques like PCA, after having performed smoothing/imputation. For that reason, to improve the imputation of data, we consecutively applied PCA and UMAP on the count matrix, then we build a distant matrix through an euclidean metric between all the pairs of data in a multidimensional space. In this PCA-UMAP multidimensional space, sc-PHENIX represents data into a reduced projection which generates the best denoise representation of cell distances measurement for the diffusion process. Having computed the distance matrix, we constructed the Markov transition matrix by applying a similar approach in MAGIC [1]. After that, we applied the diffusion process by exponentiating the transition Markov matrix (M) to a chosen power t (random walk of length t named “diffusion time”). At this point, the imputed and denoised scRNA-seq matrix is obtained by multiplying the single cell-matrix data with the exponentiated Markov transition matrix (Mt). The algorithm is described in more detail in Fig 1 and in the methods section. Finally to have a quality control of imputation, we also provide a diagnostic plot to visualize the M<sup>t</sup> cell-neighborhood. For example, the gene expression information will be shared incorrectly among distinct cell phenotypes if they are the spurious nearest neighbors in this plot. 


### How to use

The main implementation of this code is available in `umap.parametric_umap` in the [UMAP repository](https://github.com/lmcinnes/umap) (v0.5+). Most people reading this will want to use that code, and can ignore this repository. 
The code in this repository is the 'messy' version. It has custom training loops which are a bit more verbose and customizable. It might be more useful for integrating UMAP into your custom models. 

The code can be installed with `python setup.py develop`. Though, unless you're just trying to reproduce our results, you'll probably just want to pick through the notebooks and tfumap folder for the code relevant to your project. 

In addition, we have a more verbose Colab notebook to walk you through the algorithm:

mb-PHENIX is available in [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1lpdCy7HkC5TRI9LfUtIHBBW8oRO86Nvi?usp=sharing)
