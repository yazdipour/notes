# Image Processing

## Opencv

* Resouces: https://mh-salari.me/opencv-resources/
* Mouse: https://mh-salari.me/handling-mouse-events-opencv/
* Drawing https://mh-salari.me/drawing-over-an-image-in-opencv/
* SNR / PSNR: https://mh-salari.me/snr-and-psnr-in-python/
* Add-gaussian-noise: https://mh-salari.me/add-gaussian-noise-to-image-in-python/
* Basic-image-operations-opencv https://mh-salari.me/basic-image-operations-opencv/

| Action | Description|
|--- |--- |
|import|import cv2 import numpy|
|Write|cv2.imwrite('address.jpg',img)|
|Read|img=cv2.imread('img.tiff',0)|
|Show|cv2.imshow('title',img)|
|Gray PIL to OpenCV|img=ImageGrab.grab() //take scrn shot img = numpy.array(img.convert('L'))  img = img[:, :].copy()|
|Wait|cv2.waitKey(0)|
|Close windows|cv2.destroyAllWindows()|
|Crop|dst = dst[y:y+h, x:x+w]|
|W H in BW|w, h = template.shape[::-1]|
|To Gray|img_gray = cv2.cvtColor(img_rgb, cv2.COLOR_BGR2GRAY)|