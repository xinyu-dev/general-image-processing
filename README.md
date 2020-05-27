# general-image-processing
A collection of scripts for batch processing images: 1) dynamically resizes text and images to fit bounding box. 2)Reads data from CS,  apply text style, and output image files 

This is part of the volunteer projects I made for the Chinese Antibody Society.


# LogoResizer

## Usage
Batch-transform sponsor logos to uniform dimensions without shape distortion.

## Features

1. 1-line code for preprocessing, trimming, resizing, and pasting logo images into the user-defined bounding box of your background template

```python
    result_img=resizer(trim(imgPrep(logo_raw)), logoBox, temp)
```

2. Preprocessing: handling images on a transparent background

For an image of `RGBA` mode, it is first pasted onto a white background of the same size as the original image, then it processed for trimming and resizing.


3. Trimming: cut out extra white background of the original image

Extra white background of the original logo image is trimmed prior to resizing to fit into the bounding box. This ensures that the logo image extends to the fullest possible size within the bounding box.

4. Resizing: adjust images that are too large or too small.

  - if logo's starting width and/or height exceed the bounding box, we will to shrink the logo so that it is just a bit smaller than the bounding box

  - if logo's starting width and/or height is smaller than the bounding box, we will to enlarge the logo so that it is just a bit larger the bounding box

5. Process multiple files and batch export to destination folder

Input files are stored in `input_PNG_logo` folder. The script reads every `*.png` file in that folder, and process them, and export the result for each image to the `result` folder. A zip file of the `result` folder is also recreated for convenience of downloading from web-hosted jupyter notebooks.

## Examples

For the purpose of illustration, in the following examples, I marked the bounding box for the logo in GREY and the whole image frame in RED.

1. Resizing `logoResizer/examples/lonza-transparentBackground.png`. The raw images has a transparent background

**Before**

![lonza-raw](logoResizer/examples/harbormed-2.png)

**After**

![lonza-after](examples/lonza-2.png)

2. Resizing `logoResizer/examples/harbormed-transparentBackground.png`. The raw images has a white background

**Before**

![harbormed-raw](logoResizer/examples/harbormed-whiteBacground.png)

**After**

![harbormed-after](logoResizer/examples/harbormed-2.png)


## Relevant Files
See everything in `logoResizer` folder


