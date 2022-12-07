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
