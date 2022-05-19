# Research Archive

This is a research archive that contains the code to reproduce the results from my thesis project on traffic demand modeling. The research project was done in collaboration with [CBS](https://www.cbs.nl/en-gb), the Dutch Central Agency for Statistics.
</br> 
</br>
In this repository, there are three jupyter notebook scripts, two csv files and one pdf. The pdf is the thesis that describes the background and the research project, shows and discusses the results. I highly recommend reading this pdf before diving into the scripts. 
Following, I explain the structure of the scripts and the csv files, as well as other data that was used in this project and cannot be published openly. I describe alternatives to generate synthetic data. 
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
<ol>
  <li><b>edges_intensities.csv</b></li>
  <ol>
This csv contains preprocessed and aggregated traffic sensor data. Observed traffic counts are provided by the [Nationaal Dataportaal](https://www.ndw.nu/). I used a reformatted version of this data that is stored on a CBS server. If you do not have access to CBS, you can load the preprocessed and aggregated data that is provided in this csv.
  </ol>
  <li><b>inspect_model_c.ipynb</b></li>
   <ol>
     To make sure you don't have to load the entire road network from OSM again, I call the stored objects at the beginning of this script.
     After that, I inspect the calibration factor and the quality of the expected counts as an estimate for the observed counts visually and numerically.
     I then run multiple "calibration models" that I compare, to predict the calibration factor on road segments that do not have observed counts.
     Finally, I inspect whether the calibration on the basis of the calibration model improved the expected counts both visually and numerically.
     </ol>
  <li><b>Regionale_kerncijfers_Nederland_03022022_140149.csv</b></li>
  <ol>
    This file is a csv that contains the population density of each municipality in 2019. The source of this data is the open data portal of CBS, you can directly access it [here](https://opendata.cbs.nl/statline/#CBS/nl/dataset/70072ned/table?dl=5A35F) . The population density is used as a predictor to model the calibration factor in script 3. Unfortunately, you also need to get the municipality that the sensor is located in. I did this using a shapefile from CBS, which I cannot upload publically because it is not mine. If you do not have access to the internal CBS server, you can either discard the population density as a predictor, which will not have a large effect on the result. Or you can look for other public shapefiles for the Netherlands, which should be available. 
  </ol>
  <li><b>Infrastructure data</b></li>
  <ol>
    Infrastructure data on the road network is directly loaded from OpenStreetMap using the package osmnx as a graph with nodes and edges. 
  </ol>
  <li><b>Expected traffic counts</b></li>
  <ol>
  Expected counts were obtained by CBS using administrative data (see [this paper by Gootzen et al. 2020](https://www.cbs.nl/-/media/innovatie/combining-data-sources-to-gain-new-insights-in-mobility-v2.pdf) for more details), 
and survey data from the ODiN survey (see [this paper by Boonstra et al. 2021](https://www.cbs.nl/-/media/_pdf/2021/44/mobility-trends-2021-report-v3.pdf) for more info on the ODiN survey). CBS provided me with the resulting expected count for each road segment. These data sources are sensitive, and therefore I can neither publish them, nor the resulting expected counts, in this repository. Get in touch with the [CBS infoservice](https://www.cbs.nl/en-gb/about-us/contact/infoservice) if you are an interested researcher that wants to work with this data. To reproduce my results without access to the data, I included a code chunk to generate synthetic data. This creates a data frame with edges and an expected count for each edge that was randomly sampled from a gamma distribution.  
  </ol>
  </ol>
</br> 

