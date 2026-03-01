

## Error Analysis 
Root Cause Legend:

Occlusion:Construction elements or machinery are partially hidden by other site objects or structural components.

Scale Variance: The object is too small or too far from the camera.

Illumination: Lighting conditions such as shadows, fog, or low light reduce visual clarity.

Class Confusion: Objects with similar textures, colors, or shapes are visually difficult to distinguish (e.g., excavated soil vs. machinery components).
False Positive (FP) Analysis
ID: FP1

Image Reference: Annotation 1.jpg

Predicted Class: Excavator

Actual Object: Dirt Mound/Trench Edge

Root Cause Hypothesis: Class Confusion. The color and jagged texture of the earth mound (left side of the image) closely resemble the mechanical arm of the excavator.

ID: FP2
Image Reference: Annotation 2.jpg
Predicted Class: Excavator
Actual Object: Orange Construction Material/Pipe
Root Cause Hypothesis: Class Confusion. The bright orange color of the onsite material triggered a high confidence score because it mimics the "Safety Orange" paint commonly found on heavy machinery.

False Negative (FN) Analysis
ID: FN1

Image Reference: Annotation 4.jpg

Missed Class: Machinery (Distant)

Condition: Tiny scale in the background

Root Cause Hypothesis: Scale Variance. The model struggles to detect machinery that is far in the background and occupies very few pixels.
ID: FN2
Image Reference: Annotation 5.jpg
Missed Class: Workers/People
Condition: Complex Background
Root Cause Hypothesis: Occlusion. The workers are partially obscured by the rebar grid and structural elements, breaking the human silhouette that the model expects to see.

---
## 🛠️ Prioritized Next Data Improvements
Based on the failure analysis above, we prioritize the following three steps to improve model reliability for AECO site safety:

1. **Hard Negative Mining for Site Terrain:** To resolve FP1, we will add 100+ images of empty trenches and dirt mounds labeled as "background" to teach the model to distinguish natural earth textures from metallic machinery.
2. **Color Augmentation for PPE/Machinery:** To resolve FP2 (Orange Pipe confusion), we will apply "Hue" and "Saturation" augmentations in Roboflow. This helps the model differentiate between the specific "Safety Orange" of machinery and other onsite construction materials.
3. **Mosaic & Blur Augmentation for Occlusion:** To resolve FN2 (Workers behind rebar), we will enable Mosaic 4-way training. This forces the model to identify objects using only partial features, making it more robust when workers are obscured by structural grids.
