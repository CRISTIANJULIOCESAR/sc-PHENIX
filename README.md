# PHENIX
# sc-PHENIX Imputation  (2022; Code for paper)


[![Open Example In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1lpdCy7HkC5TRI9LfUtIHBBW8oRO86Nvi?usp=sharing)


==============================

!![myimage-alt-tag]()


Citation: 

```
@article{sc-PHENIX,
  title={Padron-Manrique Cristian, Vázquez-Jiménez Aarón, Esquivel-Hernandez Diego Armando, Martinez Lopez Yoscelina Estrella, Neri-Rosario Daniel, Sánchez-Castañeda Jean Paul, Giron-Villalobos David,  Resendis-Antonio Osbaldo},
}

```
### What is sc-PHENIX

Single-cell transcriptomics (scRNA-seq) is becoming a technology that is transforming biological discovery in many fields of medicine. Despite its impact in many areas, scRNASeq is technologically and experimentally limited by the inefficient transcript capture and the high rise of noise sources. For that reason, imputation methods were designed to denoise and recover missing values. Many imputation methods (e.g., neighbor averaging or graph diffusion) rely on k nearest neighbor graph construction derived from a mathematical space as a low-dimensional manifold. Nevertheless, the construction of mathematical spaces could be misleading the representation of densities of the distinct cell phenotypes due to the negative effects of the curse of dimensionality. In this work, we demonstrated that the imputation of data through diffusion approach on PCA space favor over-smoothing when increases the dimension of PCA and the diffusion parameters, such k-NN (k-nearest neighbors) and t (value of the exponentiation of the Markov matrix) parameters. In this case, the  diffusion on PCA space distorts the cell neighborhood captured in the Markovian matrix creating an artifact by connecting densities of distinct cell phenotypes, even though these are not related phenotypically. In this situation, over-smoothing of data is due to the fact of shared information among spurious cell neighbors. Therefore, it can not account for more information on the variability (from principal components) or nearest neighbors for a well construction of a cell-neighborhood. To solve above mentioned issues, we propose a new approach called sc-PHENIX( single cell-PHEnotype recovery by Non-linear Imputation of gene eXpression) which uses PCA-UMAP initialization for revealing new insights into the recovered gene expression that are masked by diffusion on PCA space.


### How to use

The main implementation of this code is available in `umap.parametric_umap` in the [UMAP repository](https://github.com/lmcinnes/umap) (v0.5+). Most people reading this will want to use that code, and can ignore this repository. 
The code in this repository is the 'messy' version. It has custom training loops which are a bit more verbose and customizable. It might be more useful for integrating UMAP into your custom models. 

The code can be installed with `python setup.py develop`. Though, unless you're just trying to reproduce our results, you'll probably just want to pick through the notebooks and tfumap folder for the code relevant to your project. 

In addition, we have a more verbose Colab notebook to walk you through the algorithm:

mb-PHENIX is available in [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1lpdCy7HkC5TRI9LfUtIHBBW8oRO86Nvi?usp=sharing)
