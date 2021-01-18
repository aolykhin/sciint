# Content Segmentation 

This module segments  compound figure into panels (region of interest). For this task, we used the implementation of Satoshi Tsutsui, and David Crandall [1]. Their code, model and weights can be found in this [link](https://github.com/apple2373/figure-separator). 

- We are making available an adapted version of FigureSeparete[1] - [Google Drive](https://drive.google.com/file/d/1BVVN736dIm2Gb39g1A9yHNwAJT7PuKX6/view?usp=sharing) to our data

# Evaluation

### Ground-Truth

To evaluate the method [1] on our data, first, two experts annotated the coordinates of each region of interest from a subset of figures from our dataset. Then, the final ground-truth was selected as the agreement regions - AND Map. 

Thus, for each figure from the subset, we generate a binary map that indicates where the regions of interest are. These regions are all located as bounding-box annotations in [figure-panel-segmentation.json](dataset_taks/segmentation/figure-panel-segmentation.json).
To recover the original images, please make use of the script at [Generate Painels from the Annontation.ipynb](Generate%20Painels%20from%20the%20Annontation.ipynb).



### Metric

We use the **Jaccard** metric to evaluate the regions generated by [1] on our ground-truth.

All the evaluation process can be found in the `Content Segmentation` notebook.

# References

[1] Tsutsui, Satoshi, and David J. Crandall. "A data driven approach for compound figure separation using convolutional neural networks." *2017 14th IAPR International Conference on Document Analysis and Recognition (ICDAR)*. Vol. 1. IEEE, 2017.
