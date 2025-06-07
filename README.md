# sam-i-am

This project is a work-in-progress that uses **SAM2** to track small fish.

It builds off the following resources: 
- [Meta AI – Segment Anything Model 2 (SAM2)](https://github.com/facebookresearch/segment-anything-2) 
- [Roboflow – SAM2 Video Segmentation Tutorial](https://github.com/roboflow-ai/notebooks/blob/main/notebooks/how-to-segment-videos-with-sam-2.ipynb). 

This notebook is intended to be run with Colab Pro on a L4 GPU (or similar). 

--- 

### Overview 

The [**Meta**](https://github.com/facebookresearch/segment-anything-2) tutorial accepted scaled video frames as input and produced scaled video frames as output. Each subject had to be added separately with manually specified coordinates. The tutorial demonstrated the functionality of SAM2 for general segmentation but was not streamlined for multi-object-tracking or longer videos.

The [**Roboflow**](https://github.com/roboflow-ai/notebooks/blob/main/notebooks/how-to-segment-videos-with-sam-2.ipynb) tutorial accepted a video as input and produced an annotated video as output. It also used a widget that allowed users to prompt the model with one point (x,y) per object. This helped to streamline the process. For larger subjects, the point prompt worked relatively well. For tiny subjects (like fish), however, the point prompt did not provide enough specificity for reliable segmentation. It also quickly hit memory limits on longer videos.

--- 

### What's new in this notebook
* support for bounding box prompts (better for tiny objects)
* an option to choose a best mask to propagate (of 3 candidates) for each object
* fixes for threading and frame caching issues (see [issue #264](https://github.com/facebookresearch/sam2/issues/264))
* chunking strategy to reduce memory use (also from [issue #264](https://github.com/facebookresearch/sam2/issues/264))
* export of segmentation masks and centroid coordinates to the disk
* an option to merge processed chunks into a final video with centroids overlaid

--- 
### A note on memory use
For example, in an 1800 frame video, these fixes reduced the memory use considerably.

**Before changes:**  
- RAM: 29.7 / 53 GB  
- GPU: 19.7 / 22.5 GB

**After changes:**  
- RAM: ~6.7 / 53 GB  
- GPU: ~6.3 / 22.5 GB

--- 

### Recommended workflow

1. Upload a video file (such as `3tiny_1m.mp4`)
2. Run the notebook cells:
    - to split video into chunks
    - annotate objects with bboxes
    - choose best mask
    - propagate masks through chunks
3. Download the final annotated video and centroids
---

**Repository URL**: [https://github.com/erikamoore/sam-i-am.git](https://github.com/erikamoore/sam-i-am.git)
