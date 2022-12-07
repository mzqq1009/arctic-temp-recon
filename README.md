# arctic-temp-recon
#The code was used to reconstruct the Arctic surface air temperature dataset.
#The overall process is divided into 3 parts: data preparation part, model building part and result output part

######################
#data preparation part
######################
1.buoy data
a.The raw buoy observations were downloaded from the official IABP website and the NCL program was used to do initial quality control on the raw buoy data, converting the minute resolution observations to daily observations. code :ncl-data preparation part.rar

b.From the raw buoy data obtained above, the temperature information was extracted using Python and saved in csv format. csv results consisted of five columns, namely buoy ID number, day, value, lat and lon, while the longitude range of the buoy was adjusted to -180 to 180, and the results were saved as separate files by year.
code: python-data preparation part.rar/zuixin_buoy.py

c.The above buoy t2m observations were again subjected to quality control by first removing buoys that were on land through the program, and in the next step plotting the path of each buoy and removing observations where the path was clearly unreasonable.
code: python-data preparation part.rar/buoy_panduan1.py  and /buoy_panduan2.py

d.Add time information such as year, month and day to the buoy data
code: python-data preparation part.rar/buoy_add_time.py

e.Quality control and correction on buoy observations
code：python-data preparation part.rar/qc_buoydata.py

2.GHCN-d
a.Download the original .dly data from the GHCN website, convert the data into a csv file, extract the temperature data and remove the missing values, and save the data separately by year.  code: GHCN.rar/GHCN_time.py

3.NP data
a.The downloaded NP observations were calculated as daily averages, the 1979 to 1991 portion of which was extracted, followed by rounding off the outliers from the NP data.  code: NP data.rar/NP.py

b.Processing of NP observations into csv format
code: NP data.rar/NP_new.py

######################
#model building part
######################
1.Download ERA5 and ERA-Interim reanalysis data for the Northern Hemisphere, with a spatial resolution of 1° and a temporal resolution of hourly. 
code: t_data.rar/download_era5_hourly_ta.py  and t_data.rar/download_ERAI-ta.py

2.The above hourly temperature data were converted to daily data using CDO (code:t_data.rar/hourly2daily.csh), after which they were placed on an equal area grid (code: t_data.rar/era_daily2ease.py) and normalised using ERA5 multi-year means and standard deviations (cdo ymonstd/ cdo ymonmean).

3.The deep learning model reference (Kadow et al., 2020), which was modified in this study, includes changing the input size of the neural network, changing the loss function, post-processing the output using Python, etc.
code： AI-north.rar

######################
#result output part
######################
The .h5 file output from the deep learning model was converted to an equal area grid nc file using python, (code: result output part.rar/h5_to_nc.py)

and the output equal area grid results were further converted to 1° latitude and longitude grid point format using Python.
(code: result output part.rar/output_1x1.py)









