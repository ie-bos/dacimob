# Dacimob

This is a research archive that contains the code to reproduce the results from my thesis project on traffic demand modeling. The expected traffic counts that were provided by CBS are a result of highly sensitive data. Get in touch with the infoservice, if you are an interested researcher that wants to work with this data (https://www.cbs.nl/en-gb/about-us/contact/infoservice).
</br> 
To reproduce my results without access to the data, I included a code chunk to generate synthetic data. Other data sources that I used are open source: Infrastructure data is directly loaded from OpenStreetMap with the osmnx package. Observed traffic counts are provided by the Nationaal Dataportaal (https://www.ndw.nu/). I used a reformatted version of this data that is stored on a CBS server. If you do not have access to CBS, you can load the preprocessed and aggregated data that is provided in the file "edges_intensities.csv".
</br>
</br> 

## Scripts
At the beginning of each script, I import all packages that are needed. If you do not have one of the packages, you can install them with !pip install PACKAGE. I worked in Jupyter notebook scripts with python v3.8.5.
</br>The scripts are structured as follows:
<ol>
  <li><b>load_preprocess_sensors.ipynb</b></li>
  <ol>
     This notebook contains the method that I used to load and preprocess the sensor data from CBS. This is not as trivial as you would expect, due to the size of this data set. If you do not have access to the internal CBS server, you cannot run this script.
    </ol>
  <li><b>link_obs_exp.ipynb</b></li>
   <ol>
  First, the sensor data, that resulted in the previous script, is aggregated. 
  If you do not have access to CBS, it is indicated at which point you can start using edges_intensites.csv
  I also load the road network data from OpenStreetMap. This takes a while (an hour or more), because it loads the entire Dutch road network.
  I inspect and visualize the observed traffic counts.
  Then, I load the expected counts that were provided by CBS. 
  If you do not have access to CBS data, you will find a chunk that you can uncomment to generate synthetic data.
  I inspect and visualize the expected counts and link them to the observed counts. 
  To make sure you don't have to reload the entire road network from OSM again for the next script, I included chunks that store the desired objects in the environment, which then can be called in another script.
     </ol>
  <li><b>inspect_model_c.ipynb</b></li>
   <ol>
     To make sure you don't have to load the entire road network from OSM again, I call the stored objects at the beginning of this script.
     After that, I inspect the calibration factor and the quality of the expected counts as an estimate for the observed counts visually and numerically.
     I then run multiple "calibration models" that I compare, to predict the calibration factor on road segments that do not have observed counts.
     Finally, I inspect whether the calibration on the basis of the calibration model improved the expected counts both visually and numerically.
     </ol>
</ol>
</br> 

## Data
The data set provided in this archive (<b>edges_intensities.csv</b>) contains preprocessed and aggregated traffic sensor data. 
</br> 
The road network data is directly loaded from OpenStreetMap using the package osmnx. Expected counts were obtained by CBS using administrative data (see [this paper by Gootzen et al. 2020](https://www.cbs.nl/-/media/innovatie/combining-data-sources-to-gain-new-insights-in-mobility-v2.pdf) for more details), 
and survey data from the ODiN survey (see [this paper by Boonstra et al. 2021](https://www.cbs.nl/-/media/_pdf/2021/44/mobility-trends-2021-report-v3.pdf) for more info on the ODiN survey). 
