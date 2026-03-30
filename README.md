This is the accompanying notebook for the discussion. It loads the blood-smear image, converts it to grayscale, builds a binary mask to separate cells from the background, and then uses watershed segmentation to split touching red blood cells into likely individual objects.

After the cells are separated, the notebook measures features such as area, major-axis length, minor-axis length, aspect ratio, eccentricity, and solidity. Those measurements are used to flag cells that look unusually elongated or irregular, which makes them possible sickle-cell candidates. The final result is both visual and numerical: the notebook saves an annotated overlay image and a table of erythrocyte measurements.

## Image comparison

### Original blood smear

![Original blood smear](Blood-smear-of-a-patient-with-Sickle-Cell-Disease.webp)

This image is the raw microscope view of the blood smear. Most erythrocytes appear round or slightly oval, while a smaller number show the elongated crescent-like shape associated with sickle cell disease.

### Processed candidate detection image

![Detected sickle-cell candidates](outputs/sickle_cell_candidates.png)

This processed image shows the result of the segmentation and measurement pipeline. Light blue boxes mark detected cell objects, while the red and orange boxes highlight cells that were flagged as possible sickle-cell candidates because they have a larger aspect ratio and more elongated shape.

The original image is useful for visual inspection because it preserves the color and natural appearance of the smear, but it does not clearly separate individual cells or quantify their shapes. The processed image simplifies the scene into measurable objects and adds labels to cells that match the notebook's sickle-cell criteria, making it easier to compare morphology across the smear. At the same time, the annotated result also shows one limitation of the method: some flagged regions may include overlapping cells or imperfect segmentations rather than true sickled erythrocytes. 
