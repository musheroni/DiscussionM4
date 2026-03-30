The blood smear has noticeable color variation inside many erythrocytes, especially pale centers, and that can confuse a simple intensity mask. To reduce that problem, the updated pipeline uses several new steps:

1. A color-aware mask is built from HSV saturation plus grayscale intensity.
   Saturation helps detect stained cell rims, while grayscale still helps recover darker cell interiors.

2. Morphological closing and hole filling are applied to the mask.
   This fills lighter erythrocyte centers so a single cell is less likely to be split apart just because its middle is brighter.

3. Marker locations are estimated from the distance transform of the filled mask.
   Larger connected regions can receive more than one marker, while smaller and rounder regions are constrained to reduce over-segmentation.

4. Marker-controlled watershed is run on a boundary map instead of only on the negative distance transform.
   The boundary map combines Sobel edge information from saturation, value, and grayscale channels, then blends that with the distance map. This makes the segmentation rely more on actual cell edges and less on center color variation.

5. Cell measurements are calculated after watershed labeling.
   The labeled regions are screened for possible sickle-cell morphology using aspect ratio, eccentricity, solidity, and axis-length differences.

This method was added specifically to improve cell separation when neighboring erythrocytes have different colors in the middle of the cell.

## Image comparison

### Original blood smear

![Original blood smear](BloodSmear.jpg)

This image is the raw microscope view of the blood smear. Most erythrocytes appear round or slightly oval, while a smaller number show the elongated crescent-like shape associated with sickle cell disease.

### Processed candidate detection image

![Detected sickle-cell candidates](outputs/sickle_cell_candidates.png)

This processed image shows the result of the updated segmentation and measurement pipeline. Light blue boxes mark detected cell objects, while the red and orange boxes highlight cells that were flagged as possible sickle-cell candidates because they have a larger aspect ratio and more elongated shape.

The original image is useful for visual inspection because it preserves the color and natural appearance of the smear, but it does not clearly separate individual cells or quantify their shapes. The processed image simplifies the scene into measurable objects and adds labels to cells that match the notebook's sickle-cell criteria, making it easier to compare morphology across the smear. The newer boundary-based watershed method also handles central color variation better than the earlier grayscale-only mask, although overlapping cells and imperfect boundaries can still cause some segmentation errors.
