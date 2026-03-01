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
 Annotation_1.png 
 Annotation_2.png
Annotation_3.png 
Annotation_4.png
Annotation_5.png 
