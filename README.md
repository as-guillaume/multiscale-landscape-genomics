# A multiscale framework for landscape genomic analyses

This repository will provide code and explanations for implementing multiscale frameworks into landscape genomic analyses. This tutorial will be completed in January 2024, providing code to allow others to personalise this framework for their research. The background and outline of the framework are indicated below.

This work is associated with the Ph.D. thesis of Annie S. Guillaume at EPFL, Switzerland. The methods presented here are associated with the fourth chapter containing the following article that is currently under review at Evolutionary Applications: 
Guillaume, A. S., Leempoel, K., Rogivue, A., Gugerli, F., Parisod, C., & Joost, S. (in review). A multiscale framework to integrate very high resolution synthetic environmental variables in genome-environment association studies. Evolutionary Applications.





 ### Background:

The reliability and accuracy of ecological models depends on access to high-quality input data, particularly for environmental variables. Topographic variables derived from digital elevation models (DEMs) are becoming increasingly popular in biodiversity modelling. These variables serve as proxies for ecologically relevant environmental factors, offering high resolutions ranging from less than 1cm through to hundreds of meters across local to global extents, generally at low costs for the end user. 

Given the sensitivity of ecological models to spatial scale, generalisations about the optimal resolution for a given variable, terrain, or species can be challenging to make. As the number of variables multiplies with each multiscale generalisation step, it can become time-consuming and impractical to systematically investigate each variable type and spatial resolution to uncover the optimal combination for a particular study. A three-step multiscale framework was developed and implemented to provide a simple and pragmatic approach for exploring the importance of spatial resolutions in ecological modelling.


 ### Three step framework
 
**1. Produce multiscale variables.** Sets of multiscale variables are first generated across all spatial resolutions of interest based on high resolution variables. Ideally, studies should be designed to allow for multiscale generalisation of variables, where the necessary resolutions hypothesised as important for the research context should be considered before sampling. Here, a resample-calculate method approach ([Misiuk et al., 2021](https://doi.org/10.1080/01490419.2021.1925789)) was implemented: DEMs were first generalised to multiple resolutions using Gaussian pyramid decompositions before deriving topographic variables of interest.

**2. Select types of variables.** Variables across the entire continuum of scales can theoretically be produced, so selecting relevant variable types becomes important to avoid computational and statistical challenges. To enable multiple resolutions per variable, only a selection of a few variable types should be used. Standard procedures are used here to reduce collinearity amongst variable types at the finest resolution, where Spearman’s pairwise correlation is used to retain one variable type per pair with a |rs|≥0.8 ([Fischer et al., 2013](https://doi.org/10.1111/mec.12521)), which is then checked using variation inflation factors (VIF) with a threshold <10 ([Dormann et al., 2013](https://doi.org/10.1111/j.1600-0587.2012.07348.x)). Priority was be given to variables considered most ecologically meaningful to the study organism, where guidelines for selecting terrain attributes were consulted ([Lecours et al., 2017b](http://dx.doi.org/10.1016/j.envsoft.2016.11.027)). 

**3. Modelling with multiscale variables.** Once variable types are selected and generalised to multiple resolutions, different methods can be used to integrate variable-resolution combinations into models. Here, a predictive stepwise forward selection procedure ([Blanchet et al., 2008](https://doi.org/10.1016/j.ecolmodel.2008.04.001)) was used to retain the variable-resolution combinations that maximised genomic variance, following [Capblancq and Forester (2021)](https://doi.org/10.1111/2041-210X.13722). 


