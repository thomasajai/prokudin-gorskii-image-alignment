# Image Alignment Project

This project implements automatic alignment and colorization of digitized Prokudin-Gorskii glass plate images using image processing techniques.

## Overview

The program takes as input a glass plate image (containing three color channels: Blue, Green, and Red) and produces a single aligned color RGB image. The alignment is performed using both simple exhaustive search and multi-scale pyramid approaches.

## Requirements

- Python 3.x
- NumPy
- Matplotlib
- Jupyter Notebook (for running the .ipynb file)

## Installation

Install the required packages using pip:

```bash
pip install numpy matplotlib jupyter
```

## Usage

### Running the Jupyter Notebook

The main implementation is in `align-tiff.ipynb`. To run:

```bash
jupyter notebook align-tiff.ipynb
```

Run the ```import``` section to load all the required packages

Update the ```input_file``` varible to the location of the glass plate image, and the ```output_file``` to the desired output location of the aligned color image

Run the ```load image``` section. This section loads the image and splits it into its RGB color channels

Run the ```show image``` section. This section sets up the functions that is used to view the image within the notebook after alignment. The ```show_image``` function also performs automatic contrast

Run the ```crop image``` section. This section sets up the function to crop into the image, this cropped in image is then used for alignment

To align the images using the **L2 alignment algorithm**, run either the ```L2 - single-scale alignment``` section (for low resolution images) or the ```L2 - multi-scale pyramid alignment ``` section (for any of the images). The aligned RGB image is generated along with the vertical(y) and horizontal(x) shifted pixel distance of the image for the green and red channels with respect to the blue channel. 

To align the images using the **NCC alignment algorithm**, first run the ```normalize``` section to set up the normalize function. Run either the ```NCC - single-scale alignment``` section (for low resolution images) or the ```NCC - single-scale alignment ``` section (for any of the images). The aligned RGB image is generated along with the vertical(y) and horizontal(x) shifted pixel distance of the image for the green and red channels with respect to the blue channel. 


After an aligned RGB image is generated within the notebook, it can be saved as a jpg by running the ```save image``` section. 



### Input Data

The program expects glass plate images where:
- The image is divided into three equal parts (Blue, Green, Red channels from top to bottom)
- Images can be either .jpg (low resolution) or .tif (high resolution) format

### Output

For each processed image, the program outputs:
- The aligned RGB color image in jpg format
- Displacement vectors (x, y) used to align the Green and Red channels to the Blue channel

## Implementation Details

### Alignment Methods

1. **Simple Alignment (for .jpg files)**
   - Exhaustive search over a window of displacements ([-15, 15] pixels)
   - Uses either L2 (Euclidean Distance) or NCC (Normalized Cross-Correlation) metrics
   - Suitable for low-resolution images

2. **Multi-scale Pyramid Alignment (for .tif files)**
   - Coarse-to-fine pyramid approach for efficiency
   - Handles large displacements in high-resolution images
   - Scales down the image iteratively, aligns at coarse level, then refines at finer levels

### Scoring Metrics

- **L2 Norm (Euclidean Distance)**: Measures pixel-wise differences between images
- **NCC (Normalized Cross-Correlation)**: Dot product between normalized image vectors
- The method used is chosen based on which gives better results for each image

### Additional Features

- **Automatic Contrast Enhancement**: Rescales image intensities to improve visual quality

## Results

The implementation successfully aligns:
- All provided low-resolution (.jpg) images
- All provided high-resolution (.tif) images
- Additional 3 images downloaded from the Prokudin-Gorskii collection

### Alignment Offsets

The computed displacement vectors for each image are documented  on the webpage.

## Notes

- Most of the images work better with NCC metric, certain ones like melons.tif and self_portrait.tif perform better with L2
- The choice of metric is documented for each image in the results


## Files

- `code.ipynb`: Main Jupyter notebook with implementation
- `index.html`: Web presentation of results
- `README.md`: This file
- `assets\`: A folder with .jpg images of the aligned images used in the web page
## Author

Submitted by Thomas Ajai as part of the HW 1 for COMS 4732: Computer Vision ii course