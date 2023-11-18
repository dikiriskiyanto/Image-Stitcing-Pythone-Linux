# Image Stitching using Python and OpenCV

Image stitching adalah proses menggabungkan beberapa gambar dengan lapangan pandang yang tumpang tindih untuk membuat gambar panorama atau wide-angle. Repositori ini berisi skrip Python untuk image stitching menggunakan perpustakaan OpenCV.

## Hal hal yang dibutuhkan

- Python3
- NumPy
- OpenCV
- Imutils

## Library Install

Anda dapat menginstal dependensi yang diperlukan menggunakan perintah berikut:

```bash
pip3 install numpy
```
```bash
pip3 install opencv-python
```
```bash
pip3 install imutils
```

## Input Gambar

<div align="center">
  <div style="display:flex; flex-wrap:wrap;">
    <img src="" alt="1" width="200"/>
    <img src="" alt="2" width="200"/>
    <img src="" alt="3" width="200"/>
    <img src="" alt="4" width="200"/>
    <img src="" alt="5" width="200"/>
    <img src="" alt="6" width="200"/>
    <img src="" alt="7" width="200"/>
  </div>
</div>


## Eksekusi

```py
# import the necessary packages
from imutils import paths
import numpy as np
import argparse
import imutils
import cv2

# construct the argument parser and parse the arguments
ap = argparse.ArgumentParser()
ap.add_argument("-i", "--images", type=str, required=True,
        help="path to input directory of images to stitch")
ap.add_argument("-o", "--output", type=str, required=True,
        help="path to the output image")
args = vars(ap.parse_args())

# grab the paths to the input images and initialize our images list
print("[INFO] loading images...")
imagePaths = sorted(list(paths.list_images(args["images"])))
images = []

# loop over the image paths, load each one, and add them to our
# images to stich list
for imagePath in imagePaths:
        image = cv2.imread(imagePath)
        images.append(image)

# initialize OpenCV's image sticher object and then perform the image
# stitching
print("[INFO] stitching images...")
stitcher = cv2.createStitcher() if imutils.is_cv3() else cv2.Stitcher_create()
(status, stitched) = stitcher.stitch(images)

# if the status is '0', then OpenCV successfully performed image
# stitching
if status == 0:
        # write the output stitched image to disk
        cv2.imwrite(args["output"], stitched)
        print("[INFO] Image stitched and saved to {}".format(args["output"]))

# otherwise the stitching failed, likely due to not enough keypoints)
# being detected
else:
        print("[INFO] image stitching failed ({})".format(status))
```

Jalankan kode ini dengan menggunakan perintah berikut:
```bash
python3 <image stitching file> --images <images input direcotry> --output <image output directory>/<output name.png>
```
Contoh:
```bash
python3 image_stitching.py --images image-input/image1 --output image-output/image1/output.png
```
Setelah kode dieksekusi, hasilnya akan ditampilkan:
```
[INFO] loading image...
[INFO] stitching images...
[INFO] Image stitched and saves to image-output/image1/output.png
```

Dan file output akan muncul dalam direktori yang Anda tentukan dalam perintah.

## hasil
Berikut adalah hasilnya:
<p align="center">
  <img src="">
</p>
