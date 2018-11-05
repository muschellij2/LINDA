
[![Travis build
status](https://travis-ci.com/muschellij2/LINDA.svg?branch=master)](https://travis-ci.com/muschellij2/LINDA)
[![AppVeyor Build
Status](https://ci.appveyor.com/api/projects/status/github/muschellij2/LINDA?branch=master&svg=true)](https://ci.appveyor.com/project/muschellij2/LINDA)
[![Coverage
status](https://codecov.io/gh/muschellij2/LINDA/branch/master/graph/badge.svg)](https://codecov.io/gh/muschellij2/LINDA)
<!-- README.md is generated from README.Rmd. Please edit that file -->

# LINDA Package:

The goal of `LINDA` is to provide a neuroimaging toolkit for automatic
segmentation of chronic stroke lesions.

## Install:

Download the [latest
release](https://github.com/dorianps/LINDA/releases/download/0.2.7/LINDA_v0.2.7.zip)
(v0.2.7, 580Mb) and unzip in a local folder.

*IMPORTANT: Only the above link contains the full release with trained
models, templates, etc. Do not use the “Download” button on Github. It
contains only smaller scripts because Github does not accept files above
100mb in main
repositories.*

###### Please send an email tp <LINDA-tools+subscribe@googlegroups.com> to register to the mailing list and receive notifications of new releases.

## What is LINDA?

Is a neuroimaging toolkit for automatic segmentation of **chronic**
stroke lesions. The method is described in [Hum Brain Mapp. 2016
Apr;37(4):1405-21](http://onlinelibrary.wiley.com/doi/10.1002/hbm.23110/abstract).  
\*\*\*\*\*  
\#\# Requirements:  
\* Linux or Mac (since Oct 2016 ANTsR [can run in Windows
10](https://github.com/stnava/ANTsR/wiki/Installing-ANTsR-in-Windows-10-\(along-with-FSL,-Rstudio,-Freesurfer,-etc\).))  
\* [R v3.0 or above](http://www.r-project.org/) \* The
[ANTsR](http://stnava.github.io/ANTsR/) package installed in R \* A
T1-weighted MRI of a patient with (left hemispheric) stroke

-----

-----

## Run:

Open R and source the file linda\_predict.R
`source('/data/myfolder/stroke/LINDA/linda_predict.R')`  
A file dialog will allow you to select the T1 nifti file of the patient
with left hemispheric brain damage.  
LINDA will run and you will see the timestamp of the various steps.  
Results will be saved in a folder named “linda” in the same path where
the T1 is located.

*Note, LINDA will stop if you don’t have `ANTsR` installed, and will
automatically install the `randomForest` package.*

**Available prediction models:**  
*Currently a model trained on 60 patients from Penn is used. The
internal prediction engine works with 2mm voxel resolution. This does
not mean your images need to be 2mm, any resolution should work.*

-----

## Example:

`source('/data/myfolder/stroke/LINDA/linda_predict.R')`  
\> 14:47 Starting LINDA v0.2.6 …  
randomForest 4.6-12  
Type rfNews() to see new features/changes/bug fixes.  
14:47 Loading file: subjA\_T1.nii  
14:47 Creating folder: /mnt/c/Users/TESTsubject/linda  
14:47 Loading template…  
14:47 Skull stripping… (long process)  
14:54 Saving skull stripped files  
14:54 Loading LINDA model  
14:54 Computing asymmetry mask…  
14:55 Saving asymmetry mask…  
14:55 Running 1st registration…  
14:56 Feature calculation…  
14:58 Running 1st prediction…  
14:58 Saving 1st prediction…  
14:58 Backprojecting 1st prediction…  
14:58 Running 2nd registration…  
15:00 Feature calculation…  
15:01 Running 2nd prediction…  
15:02 Saving 2nd prediction…  
15:02 Backprojecting 2nd prediction…  
15:02 Running 3rd registration… (long process)  
15:35 Saving 3rd registration results…  
15:36 Feature calculation…  
15:37 Running 3rd prediction…  
15:38 Saving 3rd final prediction…  
15:38 Saving 3rd final prediction in template space…  
15:38 Saving 3rd final prediction in native space…  
15:38 Saving probabilistic prediction in template space…  
15:38 Saving probabilistic prediction in native space…  
15:38 Transferring data in MNI (ch2) space…  
15:38 Saving subject in MNI (ch2) space…  
15:38 Saving lesion in MNI (ch2) space…  
DONE

Wonder what to expect? Check individual results from our [60 patients
Penn
dataset](https://drive.google.com/file/d/0BxHeqEv37qqDT085MHAyMzFJcVk)
and [45 patients Georgetown
dataset](https://drive.google.com/open?id=0BxHeqEv37qqDY1psaC14QXZSOXc).  
Our users have reported quite good lesion segmentations for typical
large stroke lesions, but less accurate segmentations with tiny lesions.

-----

## OUTPUT files:

**BrainMask.nii.gz** - Brain mask used to skull strip (native space)  
**N4corrected.nii.gz** - Bias corrected, full image (native space)  
**N4corrected\_Brain.nii.gz** - Bias corrected, brain only (native
space)  
**N4corrected\_Brain\_LRflipped.nii.gz** - Flipped image used to compute
asymmetry mask (native space)  
**Mask.lesion(1)(2)(3).nii.gz** - masks used for registrations (native
space)  
**Prediction(1)(2)(3).nii.gz** - lesion predictions after each iteration
(template space, but 2mm)  
**Prediction3\_template.nii.gz** - final prediction (template space)  
**Prediction3\_native.nii.gz** - final prediction (native space)  
**Prediction3\_probability\_template.nii.gz** - final graded probability
(template space)  
**Prediction3\_probability\_native.nii.gz** - final graded probability
(native space)  
**Reg3\_registered\_to\_template.nii.gz** - Subject’s MRI, skull
stripped, bias corrected, registered to template (template space)  
**Reg3\_sub\_to\_template\_(affine)(warp)** - transformation matrices to
register subject to template  
**Reg3\_template\_to\_sub\_(affine)(warp)** - transformation matrices to
backproject template to subject  
**Subject\_in\_MNI.nii.gz** - Subject’s MRI, skull stripped, bias
corrected, transformed in MNI space  
**Lesion\_in\_MNI.nii.gz** - Lesion mask in MNI space

-----

**Important Note**  
MNI is a space, not a template. There are many templates in MNI space,
most of which do not have the same gyri or sulci at the same
coordinates. LINDA uses the CH2 template which is included in LINDA.
Please don’t use other MNI templates to overlay results. They may look
good from a first look, but they will be wrong. Use the CH2 template
that comes with LINDA. In alternative, you can register the CH2 template
to another template (i.e., ICBM 2009a) and transform back and forth the
results as necessary.

-----

## Frequently Asked Questions

**- What file formats are accepted**?  
Nifti images (.nii and .nii.gz) are accepted. The platform can read many
other formats, but the is limtied script to Nifti in order to avoid
confusion with some formats (i.e., Analyze) that have unclear left-right
orientation.  
**- Can I use it with right hemispheric lesions?**  
Yes, but you need to flip the L-R orientation before. After that, the
prediction will work just as well.  
**- Can I use it with bilateral lesions?**  
It will likely be less accurate. One of the features LINDA uses is the
left-right signal asymmetry.  
**- Can I use it to segment acute and subacute stroke lesions?**  
No, the current model is trained only on chronic stroke patients. It
might be possible to segment acute stroke with models trained on acute
data.  
**- Can I use other images: FLAIR, T2, DWI?**  
No, the existing model accepts only T1w. In principle, additional models
can be built from other modalities (T2, FLAIR, DWI).  
**- Can I train a model with my own data?**  
This is perfectly doable, but the training script is not available
online (needs some work to adapt it for widepsread use). If you want the
example script used for the current model, I can send it easily, just
contact me.  
**- Can I use LINDA to obtain registrations in MNI?**  
The transfer in MNI is obtained by concatenating transformations
“Subject” -\> “Penn Template” -\> “ch2 MNI template”. Thus there are
two sources of potential error. The second source of error is fixed for
all subjects because our template has always the same registration on
MNI. However, a fixed error is always an error. If you really want
precise registration on MNI, I advise to register directly the subject
to an MNI template (possibly using a group MNI template rather than the
ch2).  
**- Will you maintain LINDA and publish new models in the future?**  
There is no plan, time, or funding to do this at this time. If other
researchers want to contribute, this can be done easily because LINDA is
open source.

## Support:

The best way to keep track of bugs or failures is to open a [New
Issue](https://github.com/dorianps/LINDA/issues) on the Github system.
You can also contact the author via email: dorian dot pustina at uphs
dot upenn dot edu (translate from english). If the algorithm proceeds
without errors but the automatic segmentation is erroneous, please send
(i) your T1 image and (ii) the segmentation produced by LINDA in native
space. Try also overlaying `Mask.lesion*.nii.gz` files on the T1 to
check whether the brain mask is wrong somewhere.

## Other software for lesion studies

Check out the LESYMAP package for lesion to symptom mapping:
<https://github.com/dorianps/LESYMAP>.

## Installation of Development Branchgh

You can install `LINDA` from GitHub with:

``` r
# install.packages("remotes")
remotes::install_github("muschellij2/LINDA")
```
