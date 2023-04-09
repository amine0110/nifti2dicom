[![GitHub issues](https://img.shields.io/github/issues/amine0110/nifti2dicom)](https://github.com/amine0110/nifti2dicom/issues) [![GitHub stars](https://img.shields.io/github/stars/amine0110/nifti2dicom)](https://github.com/amine0110/nifti2dicom/stargazers) [![GitHub license](https://img.shields.io/github/license/amine0110/nifti2dicom)](https://github.com/amine0110/nifti2dicom) [![GitHub forks](https://img.shields.io/github/forks/amine0110/nifti2dicom)](https://github.com/amine0110/nifti2dicom/network) ![PyPI - Python Version](https://img.shields.io/pypi/pyversions/pydicom)  [![YouTube Video Views](https://img.shields.io/youtube/views/xJ27jQVnh1M?style=social)](https://youtu.be/xJ27jQVnh1M) ![GitHub watchers](https://img.shields.io/github/watchers/amine0110/nifti2dicom?style=social)
# Convert nifti files into dicoms

This repository contains the complete code for converting nifti files to dicom series. I needed this conversion during my internship while working on tumor segmentation, so I wanted to share the method I discovered with you.

You can simply clone this repository and begin using it. All of the details can be found on my blog, which I dedicated to this function.

[Here is the article](https://pycad.co/nifti2dicom/)

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

## The main function

This is the main function that does all the work:

```python
def convertNsave(arr,file_dir, index=0):
    """
    `arr`: parameter will take a numpy array that represents only one slice.
    `file_dir`: parameter will take the path to save the slices
    `index`: parameter will represent the index of the slice, so this parameter will be used to put 
    the name of each slice while using a for loop to convert all the slices
    """
    
    dicom_file = pydicom.dcmread('images/dcmimage.dcm')
    arr = arr.astype('uint16')
    dicom_file.Rows = arr.shape[0]
    dicom_file.Columns = arr.shape[1]
    dicom_file.PhotometricInterpretation = "MONOCHROME2"
    dicom_file.SamplesPerPixel = 1
    dicom_file.BitsStored = 16
    dicom_file.BitsAllocated = 16
    dicom_file.HighBit = 15
    dicom_file.PixelRepresentation = 1
    dicom_file.PixelData = arr.tobytes()
    dicom_file.save_as(os.path.join(file_dir, f'slice{index}.dcm'))
```

## Versions 🚀
| Version | Description| Limitation |
| --- | --- | --- |
| [1.0.0](https://github.com/amine0110/nifti2dicom/releases/tag/v1.0.0) | Convert nifti to dicom by filling an existing dicom file with the new information | All the slices have the same `Series Number` | 
| [1.1.0](https://github.com/amine0110/nifti2dicom/releases/tag/v1.1.0) | The same method as the previous version | The generated dicoms can't be opened in all the medical imaging software |
| [2.0.0](https://github.com/amine0110/nifti2dicom/releases/tag/v2.0.0) | New method based on [SimpleITK](https://simpleitk.readthedocs.io/en/next/Examples/DicomSeriesFromArray/Documentation.html) | All the previous issues are resolved |


## 🆕 NEW

Full course about medical imaging segmentation is coming soon, join the waitlist here:

https://pycad.co/monai-and-pytoch-for-medical-imaging/
