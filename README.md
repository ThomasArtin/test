# Simple Object detection approach
[colab notebook](https://colab.research.google.com/drive/18p8A-g9umyKG4-7yGT7Dshe08yTHBfj7?usp=sharing)

This method only requires object detection with bounding boxes that detects crops only which makes it a much faster alternative than semantic segmentation and easily scalable to other types of crops other than carrots and only requires an object detection model to be trained on the crops.

Steps:
* Image sample :
* <img src="https://i.postimg.cc/Pq5Zgpj9/download-2.png" width="250" height="250">

* Run plantCV on the image
* Run a morphological closing to fill gaps and de-noise
* Detect all the contours and fill them to remove child contours
* Run a morphological opening to remove any weak connections and any remaining noise
* Re-Detect new final contours
* <img src="https://i.postimg.cc/sXfhYFMS/download.png" width="250" height="250">
* Convert the contours and the bounding boxes to shapely polygons for faster operations
* For every bounding box and plant if the intersection area/ the plant area is over a certain threshold (0.75 is good by trial and error) then assign that plant to the bounding box as a crop 
* algorithm output:
* <img src="https://i.postimg.cc/mZwXMMr1/download-1.png" width="250" height="250">
* segmentation annotation:
* <img src="https://i.postimg.cc/HxCc9B2w/download.png" width="250" height="250">
* remove the crops from the frame, and you are left with a weed only frame

Notes:
* As this algorithm depends heavily on openCV using the GPU version greatly increases the speed
* There are some minor cases when the crops and the weeds are heavily overlapping and in that case this weed is left out.
