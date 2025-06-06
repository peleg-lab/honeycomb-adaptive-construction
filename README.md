# Honeycomb analysis
A repository to _analyze adaptive strategies that honeybees use in building honeycomb under varying cell size initiations_ at the Peleg lab @ CU Boulder.

## Setup

Firstly, clone this repository.

### Dependencies
It is highly recommended that you set up a python virtual environment before running the following package installation commands. To do so, follow the instructions outlined [here](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/#create-and-use-virtual-environments). Once you have created a python virtual environment for this project and activated it, run the following package installation commands **from within the virtual environment**.

Install the necessary python packages by running the following command from the root of the repository.
```
pip install -r requirements.txt
```
This project uses [OpenCV](https://opencv.org/) to perform some image processing operations on the data. To use OpenCV on python, the `cv2` package has to be installed. Install this package as follows:
```
pip install opencv-contrib-python
```
For more details about installing OpenCV for `python`, go [here](https://github.com/opencv/opencv-python).

In case OpenCV fails to install properly using this method, there is an alternative way to install OpenCV for python by compiling it from the source. Although this is a time-consuming procedure, it is the officially recommended way to install OpenCV for python. Instructions to do this can be found here - [Windows](https://pyimagesearch.com/2022/04/25/installing-opencv-on-windows/), [Ubuntu](https://pyimagesearch.com/2018/08/15/how-to-install-opencv-4-on-ubuntu/), [MacOS](https://pyimagesearch.com/2018/08/17/install-opencv-4-on-macos/).

## Image data preprocessing
Run this only if you intend to inspect the X-ray data in a 3D image processing software like [Dragonfly](https://dragonfly.comet.tech/). Otherwise, it is **highly recommended** to skip this section and move directly to the statistical analysis as the image processing pipeline takes a considerable amount of time to run per dataset. The processed data is also available in the [dryad depository](https://doi.org/10.5061/dryad.z8w9ghxmw) associated with this work.

### Data
Download the raw data from the [dryad depository](https://doi.org/10.5061/dryad.z8w9ghxmw) associated with this work. The raw data files are named `s_xxx_xrm_data.zip`, `xxx` indicating the construction mode. E.g., `s_1_raw_xrm_data.zip`.

Once downloaded, extract the contents of the compressed `.zip` archive. The archive should contain a set of `.tiff` images. Move these images into the corresponding directory under `data-processing/input/`. For instance, for the `S=1` construction mode, you would extract the contents of `s_1_raw_xrm_data.zip` and place the extracted `.tiff` files in  `data-processing/input/wax_1`.

### Running the processing code
Once the data has been extracted and placed into its corresponding input directory, run the cells of the notebook `data-processing/notebooks/honeycomb-analysis.ipynb`.

The results of data processing for each dataset are stored within subdirectories under the main input directory for that dataset. These subdirectories are named after the step of the image processing pipeline they are a result of. For instance, if you run the histogram thresholding step of the image processing pipeline on the `S=1` data stored under `data-processing/input/wax_1/`, the results of this operation are stored in the subdirectory `data-processing/input/wax_1/hist_threshold/`.

Once the entire notebook is run, you will find the fully processed data under the `plastic_segmented` subdirectory under the main input directory for each dataset that the notebook is run on. For instance, once the entire notebook is run for the `S=1` data stored under `data-processing/input/wax_1/`, the final processed images for this data are stored in the subdirectory `data-processing/input/wax_1/plastic_segmented/`.

## Statistical analysis

### Data

#### S=0.75 covered cell data
This data contains the covered cell data for the `S=0.75` construction mode and is found as `s_o75_covered_cell_data.zip` on our [dryad depository](https://doi.org/10.5061/dryad.z8w9ghxmw). Download this `.zip` file and extract its contents into `statistical-analysis/input/o75-covered-cells-data/`.

After the contents of the `.zip` file have been extracted, the directory `statistical-analysis/input/o75-covered-cells-data/` should contain the following `CSV` files:
- `covered_cells_o75_1.csv`
- `covered_cells_o75_2.csv`
- `covered_cells_o75_3.csv`

where, each `CSV` file contains data about the covered/non-covered cell count for one replicate of this construction mode.

#### Cell-size data
The cell-size data for each construction mode is a set of `CSV` files, where each `CSV` file stores the cell-size data for one replicate (frame) of that construction mode. In our data, we have 3-4 replicates per construction mode. Download `cell-size-data.zip` from the [dryad depository](https://doi.org/10.5061/dryad.z8w9ghxmw) and unzip this archive under `statistical-analysis/input/cell-size-data`.

To verify that the files are placed into the correct hierarchy of directories, check that `statistical-analysis/input/cell-size-data/cell-size-data` has 7 subdirectories:
- `S_1`
- `S_1o25`
- `S_1o5`
- `S_1o75`
- `S_2`
- `S_3`
- `S_o75`

Each of these subdirectories should have multiple `CSV` files. For instance, `statistical-analysis/input/cell-size-data/cell-size-data/S_1` should have 4 `CSV` files:
- `S_1`
    - `s_1_cell_sizes_1.csv`
    - `s_1_cell_sizes_2.csv`
    - `s_1_cell_sizes_3.csv`
    - `s_1_cell_sizes_4.csv`
    
where, each `CSV` file contains the cell-size data for each replicate of the `S=1` construction mode.

#### Angle-of-tilt data
The angle-of-tilt data can be found in the `angle_data.zip` archive in our [dryad depository](https://doi.org/10.5061/dryad.z8w9ghxmw). Download this archive and extract it under `statistical-analysis/input/`.

To validate that the files are present in the intended directory structure, check that the subdirectory `statistical-analysis/input/angle-data/` is present, with it containing the following files:
- `1o25x_single_cell_tilts.csv`
- `1o5x_single_cell_tilts.csv`
- `1o75x_single_cell_tilts.csv`
- `1x_single_cell_tilts.csv`
- `2x_single_cell_tilts.csv`
- `natural_drone_cell_tilts.csv`.

### Running statistical analysis
The code for statistical analysis is present in the notebook `statistical-analysis/notebooks/statistical-analysis.ipynb`. Once the data has been organized as outlined in the [previous subsection](#data-1), run this notebook to reproduce our statistical analysis.