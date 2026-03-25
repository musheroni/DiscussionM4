This is the accompanying notebook for the discussion. It loads the blood-smear image, converts it to grayscale, builds a binary mask to separate cells from the background, and then uses watershed segmentation to split touching red blood cells into likely individual objects.

After the cells are separated, the notebook measures features such as area, major-axis length, minor-axis length, aspect ratio, eccentricity, and solidity. Those measurements are used to flag cells that look unusually elongated or irregular, which makes them possible sickle-cell candidates. The final result is both visual and numerical: the notebook saves an annotated overlay image and a table of erythrocyte measurements.

Although it is not entirely accurate, a framework similar to this could be used in the future to create a more accurate assessment of blood cell images.
