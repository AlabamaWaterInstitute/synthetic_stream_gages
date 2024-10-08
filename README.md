# Synthetic Stream Gauges: Streamflow Prediction in Ungaged Basin Using LSTM Models Trained on Synthetic Data

Accurate streamflow predictions in ungaged basins are critical for water resource management, yet less than 10% of U.S. river segments are actively gaged. Addressing this, Ramirez Molina et al. (2024) proposed [an LSTM model](https://github.com/aarm1978/Synthetic_Stream_Gauges) trained on synthetic basin networks, utilizing a ["Leaky Bucket" model](https://github.com/NWC-CUAHSI-Summer-Institute/deep_bucket_lab) developed by Frame et al. (2023) and [signal separation techniques](http://arxiv.org/abs/1804.03619) developed by Ephrat et al. (2018) to generate and disaggregate streamflow data. This research aims to evaluate the robustness of this model by improving the synthetic hydrographs generated by the Leaky Bucket.

Features in this model include:
- Realistic probability distributions used to generate precipitation, evapotranspiration (ET), and infiltration
- Refined bucket dimension generation
- Transformation of ET values using a sine function to represent diurnal fluctuations
- Soil depth added as a parameter to calculate groundwater infiltration using Darcy's Law
- Calculations unified to ensure the timestep is an hour
- Prevented water from draining if it was below the spigot
- Discharge values normalized by basin area to simplify model evaluation
- Transformed outputs using the unit hydrograph method
- Simplified basin network structure to be two buckets to make model more generalizable

## Model replication

### Environment requirements

First, clone the repository or download the files.
The following packages are required to run the model:
- numpy
- pandas
- matplotlib
- scipy
- IPython
- os
- pickle
- torch
- scikit-learn
- tqdm
- pyflo

All of these packages can be installed using `pip install`. Note that a `data` folder is required to store pickle files and the `distributions` folder and `scs484.csv` file within are required to use pyflo functionality.

The model can run on a CPU, but runs much faster on a GPU (CUDA-enabled NVIDIA GPU or MPS for Apple machines). If for some reason torch is not recognizing your CUDA-enabled GPU after a `pip install` of torch, you can follow the instructions [here](https://pytorch.org/get-started/locally/) to make sure you are installing the CUDA-enabled version of torch.

### Running the model

Running the model is as simple as running the code cells in `SyntheticGauges_QYL.ipynb`. In this notebook, you can experiment with parameter ranges, random number generator seeds, model architecture, and more. An initial random seed has been set for replication of results.

## Probability distribution function generation

Code and data sources for PDF generation is given in the `param_est` folder. Hourly precipitation data was sourced from [NOAA](https://www.ncei.noaa.gov/access/metadata/landing-page/bin/iso?id=gov.noaa.ncdc:C00313). Evapotranspiration data was sourced from the [USGS](https://www.usgs.gov/data/historical-evapotranspiration-conterminous-us) (not included in repository because of size). Geological permeability data was sourced from [CAMELS](https://gdex.ucar.edu/dataset/camels.html).

## References and Acknowledgements
This work was based on the [initial Synthetic Stream Gauges research](https://github.com/aarm1978/Synthetic_Stream_Gauges) conducted by Andres Ramirez Molina. The framework for the buckets was developed from Jonathan Frame's [Deep Bucket Lab](https://github.com/NWC-CUAHSI-Summer-Institute/deep_bucket_lab). This research was completed during the Summer 2024 Research Experience for Undergraduates at The University of Alabama, Alabama Water Institute. Additional thanks to James Halgren and Manjiri Gunaji for their feedback and support. Funding for this project was provided by the National Oceanic and Atmospheric Administration (NOAA), awarded to the Cooperative Institute for Research on Hydrology (CIROH) through the NOAA Cooperative Agreement with The University of Alabama, NA22NWS4320003.
