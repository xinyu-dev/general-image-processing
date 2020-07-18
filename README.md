# general-image-processing
A collection of Python scripts for batch-processing images and facial recognition. 

1. **Logo Resizer**: dynamically resizes images to fit bounding box.
 
2. **Headshot Cropper**: identifies faces using CV2, then extracts faces into round thumbnail images and resizes them. 

3. **Volunteer Certificate**: reads data from CSV, dynamically resizes text to fit bounding box, then applies text style, and outputs image as pdf

This is part of the volunteer projects I made for the Chinese Antibody Society.


# LogoResizer

## Description
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

Input files are stored in `input_PNG_JPG_logo` folder. The script reads every `*.png` and `*.jpg` file in that folder, and process them, and export the result for each image to the `result` folder. A zip file of the `result` folder is also recreated for convenience of downloading from web-hosted jupyter notebooks.


## Examples

For the purpose of illustration, in the following examples, I marked the bounding box for the logo in GREY and the whole image frame in RED.

1. Resizing `logoResizer/examples/lonza-transparentBackground.png`. The raw images has a transparent background

**Before**

![lonza-raw](logoResizer/examples/lonza-transparentBackground.png)

**After**

![lonza-after](logoResizer/examples/lonza-2.png)

2. Resizing `logoResizer/examples/harbormed-transparentBackground.png`. The raw images has a white background

**Before**

![harbormed-raw](logoResizer/examples/harbormed-whiteBacground.png)

**After**

![harbormed-after](logoResizer/examples/harbormed-2.png)


## Relevant Files
See everything in `logoResizer` folder

# Headshot Cropper

## Description
Batch-process images: first use openCV to detect faces, then expand the face bounding box to max possible, then crop a circle out of the bounding box, finally soften the edges.

## Features

**1. 1-line code for face recognition and cropping into a circle image with feathered (adjustable) edges, on a transparent background**

```python
    result=blurEdge(cropImage(img, faceDetection(img_cv)), blur_radius, offset=0)
```

**2. Process multiple files and batch export to destination folder**

Input files are stored in `input_PNG_images` folder. The script reads every `*.png` file in that folder, and process them, and export the result for each image to the `result` folder. A zip file of the `result` folder is also recreated for convenience of downloading from web-hosted jupyter notebooks.

**Note:**

**1. If multiple faces are detected in a single photo, only the first face box will be extracted. The program does a generally good job at handling professional headshot, but it can also handle images with a certain level of complex backgrounds (depending on the accuracy of the openCV face detection)**

**2. For the simplicity of demo,  script only reads PNG images, but you can change this parameter in the `os.path.join(img_path, '*.png')` line**

## Examples

**Note: All resulting images resized to 200x200px. This parameter is user-adjustable. The extent of edge feather effect is also adjustable**

### **1. Simple background**

**Before**

![simple-bg](headshotCropper/input_PNG_images/simple-background.png)

**After**

![simple-bg-after](headshotCropper/result/simple-background_2.png)


### 2. Complex background

**Before**

![complex-1](headshotCropper/input_PNG_images/complex_background1.png)


**After**

![complex-1-after](headshotCropper/result/complex_background1_2.png)

**Before**

![complex-2](headshotCropper/input_PNG_images/complex_background2.png)

**After**

![complex-2-after](headshotCropper/result/complex_background2_2.png)

*Example pictures credit: freepik (obtained under CAS's image license with freepik)*


# Volunteer Certificate

## Description

The script reads data from CSV, dynamically resizes text to fit bounding box, then applies text style, and outputs image as pdf. 

## Features

1. The script loads an empty image template (e.g. a **.png** file), then reads data from csv file (columns: **name**, **start**, **end**). The **start** and **end** columns are the year the volunteer joined and left respectively.

2. Dynamic text-resizing: If a volunteer has a very long name, its font size will decrease gradually until the text is able to fit in the bounding box.

3. 1-year term and multi-year terms: If a volunteer joined and left in the same year (i.e. in the csv file,  `start == 2020`, `end == 2020 ` ), then on the certificate, only that year will appear in the lower right corner (e.g. `2020`). Otherwise, on the certificate the year will appear as a range (e.g. `2016 - 2020`).

4. Output file as **name.pdf**, where the **name** is the volunteer name. For convenience a zip file of all pdf outputs is also generated. 

5. Unique file names: In a scenario where volunteers have the same name, the output file for the 2nd volunteer will say **name_1.pdf** (where **name** is the name of the volunteer), and for the 3rd volunteer it will say **name_2.pdf**, etc. In this you don't have to worry about overwriting the previous files.

## Examples 

### Long Name
![longname](https://res.cloudinary.com/dpfqlyh21/image/upload/v1595110216/github/long_name_ppezcy.png)

### 1-Year Term vs Multi-Year Term

#### Multi-Year Term (e.g. 2019-2020, see above)

#### 1-Year Term (e.g. 2018)

![oneyearterm](https://res.cloudinary.com/dpfqlyh21/image/upload/v1595110384/github/one_year_term_jz6xc0.png)


### Unique file names
See `Zhidan Tu.pdf`, `Zhidan Tu_1.pdf` and `Zhidan Tu_2.pdf` in the output folder 




