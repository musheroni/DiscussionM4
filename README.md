This code follows the procedure listed below:

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

## Image comparison

Original blood smear

![Original blood smear](BloodSmear.jpg)

This image is the raw microscope view of the blood smear. Most erythrocytes appear round or slightly oval, while a smaller number show the elongated crescent-like shape associated with sickle cell disease.

Processed candidate detection image

![Detected sickle-cell candidates](outputs/sickle_cell_candidates.png)

As you can see, this obviously has room for improvement, and other identification features can be addded, especially if you want to track polychromatophilic RBCs, target cells, or Howell-Jolly bodies.
