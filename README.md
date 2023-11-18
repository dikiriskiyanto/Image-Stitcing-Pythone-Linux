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
    <img src="https://user-images.githubusercontent.com/150429308/284002446-b28c4ea1-1626-48f9-8695-605bc2940c59.jpg" alt="1" width="200"/>
    <img src="https://user-images.githubusercontent.com/150429308/284002451-3cb65ee9-cdb8-41ba-a7b1-eabaa912820c.jpg" alt="2" width="200"/>
    <img src="https://user-images.githubusercontent.com/150429308/284002455-fb821b1e-38ce-4359-9162-b686444e35be.jpg" alt="3" width="200"/>
    <img src="https://user-images.githubusercontent.com/150429308/284002458-45a63d38-112d-4146-be10-b8a526166352.jpg" alt="4" width="200"/>
    <img src="https://user-images.githubusercontent.com/150429308/284002461-6f2c325a-eaf7-41e6-8c27-e312fde22851.jpg" alt="5" width="200"/>
    <img src="https://user-images.githubusercontent.com/150429308/284002465-7d3e7fb1-909a-4cbe-bd9e-522561b05bd7.jpg" alt="6" width="200"/>
    <img src="https://user-images.githubusercontent.com/150429308/284002468-9dd95752-c5c2-4c20-8275-75f770d61178.jpg" alt="7" width="200"/>
    <img src="https://user-images.githubusercontent.com/150429308/284002471-7449f9b9-7adb-4b53-834b-f1ee9a18092a.jpg" alt="8" width="200"/>
    <img src="https://user-images.githubusercontent.com/150429308/284002473-a8d545d9-421f-481f-8ccc-8cf2853f1354.jpg" alt="9" width="200"/>
    <img src="https://user-images.githubusercontent.com/150429308/284002477-6d4470e5-eb71-4035-9960-98894ad25221.jpg" alt="10" width="200"/>
    <img src="https://user-images.githubusercontent.com/150429308/284002481-04bff590-64a5-40f6-aa73-f5f569903a96.jpg" alt="11" width="200"/>
    <img src="https://user-images.githubusercontent.com/150429308/284002486-eef69080-c1fa-484e-a903-c345d4abaa56.jpg" alt="12" width="200"/>
    <img src="https://user-images.githubusercontent.com/150429308/284002491-99f29c50-3919-4321-be60-73a3f035dc37.jpg" alt="13" width="200"/>
    <img src="https://user-images.githubusercontent.com/150429308/284002495-7a2ac112-31c9-414c-8345-0e454d5b06ee.jpg" alt="14" width="200"/>
    <img src="https://user-images.githubusercontent.com/150429308/284002498-49254143-341b-4522-81d2-8716f558a23c.jpg" alt="15" width="200"/>
    <img src="https://user-images.githubusercontent.com/150429308/284002501-dbf54a44-b13e-484a-8605-4c51cb231511.jpg" a <img src="" alt="17" width="200"/>
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
python3 image_stitching.py --images image-input/image3 --output image-output/image3/output.png
```
Setelah kode dieksekusi, hasilnya akan ditampilkan:
```
[INFO] loading image...
[INFO] stitching images...
[INFO] Image stitched and saves to image-output/image3/output.png
```

Dan file output akan muncul dalam direktori yang Anda tentukan dalam perintah.

## hasil
Berikut adalah hasilnya:
<p align="center">
  <img src="https://user-images.githubusercontent.com/150429308/284002504-50095ede-1bc1-4860-981d-6d09d2e7156a.jpg">
</p>
