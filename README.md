# Yeo_synapse_LLM

## Xenium Prime 5k Experiment Data Analysis

This repository houses a series of Jupyter notebooks developed for the comprehensive analysis of Xenium Prime 5k experimental data. Each notebook in this project addresses a specific stage of the analysis pipeline—from converting raw data into efficient formats to performing advanced downstream analyses. The goal is to streamline the workflow and provide clarity at every step of the process.

---

### Notebook 1: Xenium to Zarr Conversion Notebook

- **Purpose:**  
  This notebook converts all the Xenium datasets into the Zarr format. The Zarr format offers a condensed version of the spatial dataset that is optimal for efficiently loading `SpatialData` objects during analysis.

- **Key Functions and Processes:**  
  - **Input/Output:**  
    - **Input:** Xenium dataset directory.  
    - **Output:** A Zarr file storing the converted data.
  - **Steps Involved:**  
    1. **Dataset Reading:** Loads the Xenium dataset using the `spatialdata_io.xenium` function.
    2. **Directory Management:** Checks if the target Zarr directory exists and removes it if necessary.
    3. **Data Conversion:** Writes the loaded `SpatialData` object to the specified Zarr file.
    4. **Iteration:** Loops through directories in the input path to process multiple datasets by dynamically generating output file paths.

- **Notebook Location:** [Xenium to Zarr Conversion Notebook](./analysis/Dylan/preprocess/xenium_to_sdata.ipynb)

- **Yeo group**:
  - Use `module load scverse/1.0.0_spatialdata0.2.6`
---

### Notebook 2: Feature and Localization Analysis

- **Purpose:**  
  These notebooks demonstrate how to use the `SpatialData` and `Bento` packages to analyze spatial transcriptomics data from the Xenium dataset. They focus on calculating key shape and transcript features, as well as performing localization analysis.

- **Key Components and Analysis:**  
  - **Load Data:**  
    - Loads a Xenium dataset from a pre-converted Zarr file into a `SpatialData` object.
    - Prepares the data for downstream analysis with Bento.
  - **Shape and Point Features:**  
    - Computes metrics such as soma and nuclear area, aspect ratio, and transcript density to assess data quality and cellular morphology.
  - **Localization Analysis:**  
    - Classifies gene transcripts into distinct localization patterns (Cell Edge, Cytoplasmic, Nuclear, Nuclear Edge, and None) using the RNAForest model.
    - Visualizes these patterns with an UpSet plot and a radar plot to compare gene-specific localization strengths.

- **Notebook Location:** [Coronal 1 Cortex: Feature and Localization Analysis Notebook](./analysis/Dylan/bento_analysis/coronal1_cortex_localization_analysis.ipynb)

- **Yeo group**:
  - Use `module load scverse/1.0.0_spatialdata0.2.6`
---

### Notebook 3: Synaptic Immunofluorescence Alignment

- **Purpose:**  
  These notebooks align Xenium imaging data to synaptic immunofluorescence (IF) images. The objective is to align DAPI, presynaptic, and postsynaptic images using transformation matrices, crop the data to the region-of-interest, and visualize the quality of the alignment.

- **Key Components and Analysis:**  
  - **Create SpatialData Object:**  
    - Loads a SpatialData object from a pre-converted Zarr file that contains imaging and morphological data.
  - **Align Images:**  
    - Uses an alignment matrix to transform and parse the DAPI, presynaptic, and postsynaptic IF images into `Image2DModel` objects.
  - **Visualization:**  
    - Overlays the DAPI image with aligned IF images to verify correct registration.
  - **ROI Cropping:**  
    - Determines the region-of-interest using bounding box calculations and crops the SpatialData object accordingly.
  - **Saving Results:**  
    - The processed SpatialData object is saved as a new Zarr file for downstream analysis.

- **Notebook Location:** [Coronal 1 Cortex: Synaptic Immunofluorescence Alignment Notebook](./analysis/Dylan/alignment/coronal1_cortex_alignment.ipynb)

- **Yeo group**:
  - Use `module load scverse/1.0.0_spatialdata0.2.6`
---

### Notebook 4: Synaptic Compartment Analysis

- **Purpose:**  
  These notebooks perform an in-depth analysis of transcripts in multiple subcellular compartments. They focus on segmenting immunofluorescence images to extract presynaptic and postsynaptic regions, mapping transcript points to these compartments, and calculating quantitative metrics.

- **Key Components and Analysis:**  
  - **Data Loading:**  
    - Loads an aligned SpatialData object from a pre-converted Zarr file containing IF imaging data.
  - **Utility Functions:**  
    - Defines custom plotting functions to render images and transcript point scatterplots.
  - **Segmentation:**  
    - Implements segmentation of the presynaptic and postsynaptic regions using preprocessing steps (gamma adjustment, Gaussian filtering, erosion) followed by multi-Otsu thresholding.
  - **Labeling and Mapping:**  
    - Converts segmentation outputs into label elements.
    - Extracts pixel coordinates and maps transcript points (both unassigned and soma-inclusive) to synaptic compartments.
  - **Counts Calculation:**  
    - Computes transcript counts across different compartments (e.g., exclusive presynaptic, postsynaptic, overlapping areas, nucleus, and soma) and calculates derived metrics by excluding synaptic signals.
    - Saves the calculated counts to a CSV file for downstream analysis.
  - **Visualization:**  
    - Provides extensive visualizations including raw IF images, segmentation overlays, combined segmentation masks, and gene-specific transcript plots (e.g., for Dlg4) with scale bars and integrated visual elements.

- **Notebook Location:** [Coronal 1 Cortex: Synaptic Compartment Analysis Notebook](./analysis/Dylan/analysis/coronal1_cortex_analysis.ipynb)

- **Yeo group**:
  - Use `module load scverse/1.0.0_spatialdata0.2.6`
 
### Notebook 5: Bento QC

- **Purpose:**  
  These notebooks use bento to perform basic QC plotting (eg. cell size, localization etc.)

- **Yeo group**:
  - Use `module load bento/3e82209`