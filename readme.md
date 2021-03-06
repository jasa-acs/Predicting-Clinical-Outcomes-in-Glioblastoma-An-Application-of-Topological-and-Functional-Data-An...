# Predicting Clinical Outcomes in Glioblastoma: An Application of Topological and Functional Data Analysis


# Author Contributions Checklist Form

## Data

### Abstract

Radiomics is focused on the extraction of quantitative features from medical images, typically constructed by tomography and digitally stored as shapes or surfaces. In our manuscript, we explore the use of a novel statistic, the smooth Euler characteristic transform (SECT), as an automated procedure to extract geometric or topological statistics from tumor images. More generally, the SECT is designed to integrate shape information into regression models by representing shapes and surfaces as a collection of curves. Due to its well-defined inner product structure, the SECT can be used in a wider range of functional and nonparametric modeling approaches than other previously proposed topological summary statistics. We illustrate the utility of the SECT in a radiomics context by showing that the topological quantification of tumors, assayed by magnetic resonance imaging (MRI), are better predictors of clinical outcomes in patients with glioblastoma multiforme (GBM). Using publicly available data from The Cancer Genome Atlas (TCGA) and The Cancer Imaging Archive (TCIA), we show that SECT features alone explain more of the variance in patient survival than gene expression, volumetric features, and morphometric features.



### Availability 

The results shown in our manuscript are in whole or part based upon data generated by the TCGA Research Network. DICOM formatted MRI scans and patient clinical information were taken directly from the TCIA web portal. Matched molecular data were downloaded directly from the Genomic Data Commons (GDC) by selecting the RNA-Seq tab option under GBM. Shapebased summary statistics necessary for replicating this study (i.e. the segmented tumor images, the volumetric measurements, morphometric data, and topological summary statistics) will be made publicly available. For the purposes of review, the data and code are attached to this manuscript as a supplement.

### Description

Segmented TCIA Magnetic Resonance Images (MRIs): MRIs of primary GBM tumors were
collected from 48 patients archived by The Cancer Imaging Archive (TCIA) (Clark et al., 2013).
The TCIA is a publicly accessible data repository containing medical images of cancer patients
with matched genomic and clinical data collected by The Cancer Genome Atlas (TCGA) (The
Cancer Genome Atlas Research Network, 2008). The patients analyzed in the manuscript were
selected based on two sets of criteria, namely: (i) they had post-contrast T1 axial MRIs taken at
the time of their diagnosis, and (ii) they had available matching (mRNA) gene expression data
and clinical correlates on cBioPortal.

We segmented the TCIA MRIs using the Medical Imaging Interaction Toolkit with augmented
tools for segmentation (MITKats) (Chen and Rabadan; 2017) to extract tumor lesions from the
surrounding brain tissue. Briefly, this algorithm first converts MRI images to grayscale, and then
thresholds to generate binary images. Morphological segmentation is then applied to delineate
connected components. More specifically, the program selects contours corresponding to
enhanced tumor lesions, which are lighter than healthy brain tissue. For instance, necrosis
presents as dark regions nested within the indicated lesion. Examples of the raw image
obtained from TCIA and the final segmented result are given in the manuscript in Figure 3(a)
and Figure 3(b), respectively.

Currently, both the R and Matlab versions of the SECT software package is set up to take in
images/shapes that are formatted as png files. The Bayesian functional kernel regression model
is written in R and C++ code and analyzes matrix valued variables. To this end, the SECT
function produces functional covariates in matrix form. Moreover, the preprocessed version of
the gene expression from the TCGA may be loaded as a data frame. Lastly, the tumor
morphometry and volumetric features are saved as csv files that may also be read in as data
frames.

## Code

### Abstract

The smooth Euler characteristic transform for images and three-dimensional shapes is
implemented as a set of R and MATLAB routines. Results in the manuscript were derived by
using the R version of the code. The Bayesian Gaussian process (GP) regression model that
we used to incorporate shape statistics in predictive analyses is also carried out within the R
environment.

### Description 

The smooth Euler characteristic transform for images and three-dimensional shapes is
implemented as a set of R and MATLAB routines. Results in the manuscript were derived by
using the R version of the code. The Bayesian Gaussian process (GP) regression model that
we used to incorporate shape statistics in predictive analyses is also carried out within the R
environment.

### Optional Information 


The Matlab Environment (version 2017a): MATLAB is a multi-paradigm numerical computing
environment and a proprietary programming language developed by MathWorks. MATLAB
allows matrix manipulations, plotting of functions and data, implementation of algorithms,
creation of user interfaces, and interfacing with programs written in other languages. For more
on licensing options, please visit here.

The R Environment (version 3.6.1): R is a widely used, free, and open source software
environment for statistical computing and graphics. The most recent version of R can be
downloaded from the Comprehensive R Archive Network (CRAN). CRAN provides precompiled
binary versions of R for Windows, MacOS, and select Linux distributions that are likely sufficient
for many users' needs. Users can also install R from source code; however, this may require a
significant amount of effort. For specific details on how to compile, install, and manage R and Rpackages,
refer to the manual R Installation and Administration.

R Packages Required for SECT and the GP Regression: The statistical implementation of the
SECT topological summaries using functional RKHS models requires the installation of the
following R libraries:
• BGLR (version 1.0.8)
• doParallel (version 1.0.14)
• Rcpp (version 1.0.1)
• RcppArmadillo (version 0.9.400.3.0)
• RcppParallel (4.4.2)
• R.matlab (if using the MATLAB version of SECT)

The easiest method to install these packages is with the following example command entered in
an R shell:

install.packages("BGLR", dependecies = TRUE)

Alternatively, one can also install R packages from the command line.

C++ Functions Required for Covariance Functions: The code in this repository assumes that
basic C++ functions and applications are already set up on the running personal computer or
cluster. If not, the BAKR functions and necessary Rcpp packages will not work properly. A
simple option is to use gcc. macOS users may use this collection by installing the Homebrew
package manager and then typing the following into the terminal:

brew install gcc.

For macOS users, the Xcode Command Line Tools include a GCC compiler. Instructions on
how to install Xcode may be found here. For extra tips on how to run C++ on macOS, please
visit here. For tips on how to avoid errors dealing with "-lgfortran" or "-lquadmath", please
visit here.

Note that results for the manuscript were derived using gcc version 9.2.0.

## Instructions for Use

Please ensure that the versions of the software match those specified in the descriptions above.
Also, please ensure that the working directory is set appropriately, and that all of the necessary files from the repository have been downloaded to the working directory. The “Analysis” folder
contains the script Paper_Scripts.R, which provides a sequence of commands to be run in
subsequent order and presents the final results in a table, which matches Table 1 in the
manuscript; detailed instructions are given in the code commentary. The “Tutorial” folder
contains the script SECT_Tutorial.R, which provides sample SECT curves for an example
segmented tumor; detailed instructions are given in the code commentary.

### Reproducibility

The script SECT_Tutorial.R contains the commands needed to reproduce Figure 3 in the
manuscript, which are the SECT curves for an example segmented tumor. This script should
take approximately 5.5 to 6 minutes to complete on a personal laptop.

The script Paper_Scripts.R contains the commands needed to reproduce the data analyses
presented in Table 1 in the manuscript. This script should take approximately 3.5 to 4 minutes to
complete on a personal laptop.

Note that these run times and results were recorded on a 2017 MacBook Pro (Processor: 3.1-
gigahertz (GHz) Intel Core i5, Memory: 8GB 2133-megahertz (MHz) LPDDR3, macOS: Mojave
10.14.6, Platform: x86_64-apple-darwin15.6.0 (64-bit)).

 
### Code Availiability
Code for this work (including scripts to reproduce the main results in the paper) are located on
public GitHub repository at https://github.com/lorinanthony/SECT.
