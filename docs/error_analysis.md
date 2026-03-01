## SAM Exploration Notes 
Segment Anything Model (SAM) was used in Roboflow as an AI assisted annotation tool to speed up the labelling process of construction activities.

## What Helped
SAM helped reduce annotation time by automatically detecting object boundaries after selecting the target area. It was particularly useful in images where construction elements had clear edges and visible boundaries, such as reinforcement cages. 
SAM was also effective in detecting construction machinery with well-defined shapes, such as concrete mixer trucks and excavators, where the object edges were clear and easy to identify. The tool made the labeling process faster compared to drawing bounding boxes manually.
## What Failed
SAM performance was weaker when construction activities did not have clearly defined boundaries. In some excavation images, the transition between soil and working areas was not always clear, which caused inaccurate selections.
Under harsh weather conditions, especially in foggy environments, SAM sometimes struggled to correctly detect the object because the visibility was reduced. This resulted in incomplete or incorrect selections that required manual correction.
SAM also had difficulty when there was material overlap, such as steel reinforcement partially covered by concrete, where the model could not clearly distinguish between the two materials.
## Annotaion 1 
SAM successfully detected the excavator because it has clear boundaries and a defined shape. However, the excavation ground required manual adjustment since soil areas do not have clear edges.
## Annotaion 2
This excavation area was labeled manually because SAM could not clearly detect the boundaries of the excavation. Irregular soil surfaces required manual annotation to ensure accurate labeling.
## Annotation 3
SAM successfully detected the concrete slab because it has clear and defined boundaries. The tool produced an accurate selection and required only minor adjustments.
## Annotation 4
SAM successfully detected the excavator because it has clear boundaries, but it could not accurately detect the excavation area due to unclear soil boundaries and difficult conditions.
## Annotation 5
SAM detected the concrete surface well, but manual editing was required where steel reinforcement overlapped with fresh concrete to ensure accurate labeling.
## Annotation Evidence

The SAM annotation examples used for this exploration are stored in:

results/evidence/

Example files:

- Annotation_1.png 
- Annotation_2.png
- Annotation_3.png 
- Annotation_4.png
- Annotation_5.png 

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
