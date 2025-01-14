# Climate-Distance
## Global climate distance code
![lower res global map of interpolated climate distances](Lin_interp_1mill_world_map.jpg)
### Input Climate Data
Raw input climate files can be downloaded from CHELSA using the following links:\
[2011-2040 Temp](https://os.zhdk.cloud.switch.ch/chelsav2/GLOBAL/climatologies/2011-2040/GFDL-ESM4/ssp370/bio/CHELSA_bio1_2011-2040_gfdl-esm4_ssp370_V.2.1.tif)\
[2040-2070 Temp](https://os.zhdk.cloud.switch.ch/chelsav2/GLOBAL/climatologies/2041-2070/GFDL-ESM4/ssp370/bio/CHELSA_bio1_2041-2070_gfdl-esm4_ssp370_V.2.1.tif)\
[2011-2040 Rainfall](https://os.zhdk.cloud.switch.ch/chelsav2/GLOBAL/climatologies/2011-2040/GFDL-ESM4/ssp370/bio/CHELSA_bio12_2011-2040_gfdl-esm4_ssp370_V.2.1.tif)\
[2040-2070 Rainfall](https://os.zhdk.cloud.switch.ch/chelsav2/GLOBAL/climatologies/2041-2070/GFDL-ESM4/ssp370/bio/CHELSA_bio12_2041-2070_gfdl-esm4_ssp370_V.2.1.tif)\
Details of the CHELSA climatologies can be found [here.](https://chelsa-climate.org/wp-admin/download-page/CHELSA_tech_specification_V2.pdf)

**CHELSA Reference:** Karger, D.N., Conrad, O., Böhner, J., Kawohl, T., Kreft, H., Soria-Auza, R.W., Zimmermann, N.E., Linder, P., Kessler, M. (2017): Climatologies at high resolution for the Earth land surface areas. Scientific Data. 4 170122. https://doi.org/10.1038/sdata.2017.122

## 1). Pre-processing and sampling of Climate Data
[Sample and process CHELSA data script](Climate_input_sampling.R)\
Crops CHELSA climate data to land area and outputs each layer as a "full".tif, then randomly samples chosen % of cells from each input layer and export as "processed".tif. Requires decent RAM and high vector limit to run. 

## 2). Climate data rounding and conversion
[Rounding and conversion script](Rounded_climate_inputs.R)\
Rounds temperature and rainfall data to desired number of sig fig/decimals, then stacks the climate layers into a raster. Finally converts stacked raster into a large .csv file. Conversion from .tif raster to .csv requires large RAM and high vector limit so may need to be run separately using this [raster to csv script](Rast_to_CSV.R). 

## 3). Calculation of climate distances (to be run on cluster)
[Climate distance cluster script](Updated_cluster_code_EXACT.R)\
Takes the randomly sampled % of cells .csv and calculates climate distance for temperature and rainfall between time point 1 and time point 2. Set up to run in parallel over many cores to process the entire .csv input file. This version finds exact temperature and rainfall matches, but confidence boundaries can also be calculated using the following scripts:\
[Plus +0.5C, plus 5mm](Updated_cluster_code_PLUSPLUS.R)\
[Plus +0.5C, minus 5mm](Updated_cluster_code_PLUSMINUS.R)\
[Minus -0.5C, plus 5mm](Updated_cluster_code_MINUSPLUS.R)\
[Minus -0.5C, minus 5mm](Updated_cluster_code_MINUSMINUS.R)

## 4). Convert Climate Distance to KM
[Convert climate distance into KM](CD_in_m_to_KM.R)

## 5). Interpolate Climate Distances
[Linear interpolation script](CD_interpolate_Linear_script.R)\
[Akima interolation script](CD_interpolate_akima_script.R) 

## 6). Plot Global Map of Climate Distances
[Plot interpolated climate distances](Global_CD_MAP.R)
![lower res global map of interpolated climate distances](Lin_interp_1mill_world_map.jpg)

