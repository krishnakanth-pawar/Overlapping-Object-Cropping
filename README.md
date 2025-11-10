# Overlapping Object Cropping

##  Overview
This project implements an automated system to **detect and crop the primary object** from images containing **two overlapping objects** — typically a **hand** overlapping a **face**.  
The system identifies both regions, determines which object should be considered *primary*, and crops that object accurately. Note: Sample images can be used for the test.

---

### Step-by-step Pipeline
1. **Detection**  
   - Uses **MediaPipe FaceMesh** and **MediaPipe Hands** to detect facial and hand landmarks.

2. **Mask Generation**  
   - Converts landmark coordinates into **binary masks** using convex hull polygons.

3. **Overlap Analysis**  
   - Calculates the **Intersection-over-Union (IoU)** between face and hand masks.  
   - Determines how much one object occludes the other.

4. **Primary Object Selection**  
   - Applies logical rules:
     | Condition | Selected Primary Object |
     |------------|--------------------------|
     | Hand overlaps face heavily (>60%) | Hand |
     | Face more visible than hand | Face |
     | Minimal overlap | Larger visible region |

5. **Cropping**  
   - Crops the selected object using its mask’s bounding box (with optional padding).

6. **Output Generation**  
   - Saves a visualization overlay (`visual_overlay.jpg`) and the cropped region (`primary_crop.jpg`).


---

## ⚙️ Requirements
You can run this code in Google Colab or Jupyter Notebook.

Install all dependencies using pip:

```bash
pip install mediapipe opencv-python numpy
