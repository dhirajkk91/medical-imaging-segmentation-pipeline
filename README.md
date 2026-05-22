# Img_proc_V1 Notebook Explanation

This notebook contains a complete pipeline for processing panoramic bone images and extracting regions of interest along the cortex. The focus is on image enhancement, edge-based cortex path detection, sampling points along the detected cortex, and generating fixed-size crop boxes around those points.

## What is being done

1. Preprocessing:
   - The input image is loaded in grayscale.
   - Contrast is enhanced using CLAHE to improve local detail.
   - A large morphological opening is used to estimate background illumination.
   - The background is subtracted and the result is normalized to a full intensity range.

2. Edge score computation:
   - A vertical Sobel filter is applied to a central search band in the image.
   - Absolute gradient magnitudes are computed to highlight cortex-like edges.
   - A small bias is added to favor lower rows, which helps keep the detected path on the lower cortex surface.

3. Path fitting with dynamic programming:
   - Two separate horizontal image regions are defined for the left and right cortical zones.
   - For each side, a dynamic programming routine selects a smooth path through the edge score volume.
   - The path is smoothed with a 1D filter to reduce jitter.

4. Sampling crop centers:
   - The fitted left and right cortex paths are sampled at evenly spaced column positions.
   - A configurable number of sample points is produced, balancing left and right sides.

5. Box generation and extraction:
   - Fixed-size boxes are centered on the sampled points.
   - A vertical shift parameter allows the box center to move relative to the detected cortex location.
   - Image crops are extracted from the processed panoramic image.

6. Visualization and debugging:
   - A debug overlay is created on the original grayscale image.
   - The overlay draws the search zones, the detected cortex paths, sampled points, and crop boxes.
   - This provides a visual check of how the cortex is being followed and where crops are selected.

7. Batch processing support:
   - The notebook includes a loop that iterates over an input image folder.
   - For each image, the cortex-following pipeline is applied and a debug image is saved.

## Parameters and control points

- `left_range` and `right_range` define the horizontal search windows for the left and right cortex.
- `search_y_ratio` defines the vertical band where the cortex edge score is computed.
- `smooth_penalty` and `max_step` control the smoothness of the dynamic programming path.
- `smooth_k` controls final path smoothing after dynamic programming.
- `max_points_total` sets how many crop centers are sampled from both sides.
- `box_w`, `box_h`, and `vertical_shift` determine the size and vertical position of the extracted patches.

## Key functions in the notebook

- `preprocess_panoramic`: prepares the grayscale panoramic image for edge-based detection.
- `build_edge_score`: computes the edge strength map and adds a row bias.
- `find_best_path_dp`: finds a smooth path through the score image using dynamic programming.
- `fit_cortex_paths`: applies path fitting to left and right search zones.
- `build_boxes_from_points`: converts sampled points into crop rectangles.
- `draw_debug_overlay`: creates the annotated visualization used for debugging.
- `process_one_image_follow_cortex`: orchestrates the full pipeline for a single image.

This explanation is intended to describe the notebook workflow and the role of each major stage without turning the document into a formal usage guide.
