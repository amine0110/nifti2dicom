# Convert nifti files into dicoms

This repository contains the complete code for converting nifti files to dicom series. I needed this conversion during my internship while working on tumor segmentation, so I wanted to share the method I discovered with you.

You can simply clone this repository and begin using it. All of the details can be found on my blog, which I dedicated to this function.

## The steps

- Using pre-existing dicom file.
- The packages that we need.
- Extract the frame data from the nifti file.
- Prepare the array to be converted.
- Convert one nifti file into dicom series.
- Convert multiple nifti files into multiple dicom series.

## The Packages that We Need
As with any other program, we need some packages to complete this conversion, so in this project, you will need to install the following packages individually.

- nibabel: ```pip install nibabel```

- pydicom: `pip install pydicom`

- numpy: `pip install numpy`

- tqdm: `pip install tqdm` (this one is just to print the progress of the conversion)
