# test
<img src="https://i.postimg.cc/zfs0mVBc/download.png" width="500" height="500">

This method only requires object detection with bounding boxes that detects crops only which makes it a much faster alternative than semantic segmentation and esily scalable to other types of crops other than carrots and only requires an object detection model to be trained on the crops.

Steps:
1. Run plantCV on the image
2. Run a morphological closing to fill gaps and de-noise
3. Detect all the contours and fill them to remove child contours
4. Run a morphological openning to remove any weak connections and any remainning noise
5. Re-Detect new final contours
6. Convert the contours and the bounding boxes to shapely polygons for faster operations
7. For every bounding box and plant if the intersection area/ the plant area is over a certain threshold (0.75 is good by trial and error) then assign that plant to the bounding box as a crop
8. remove the crops from the frame and you are left with a weed only frame

