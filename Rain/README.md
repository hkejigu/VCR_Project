#Rain

This directory contains all of the codes used to process the NOAA daily precipitation data at the woreda or kebele level. The
user only needs to call 'sh processRainData.sh Woreda' or 'sh processRainData.sh Kebele' from the command line.

processRainData.sh will call downloadRainData.py to download the data. It will then call convert_rfe_bin2asc.f to convert the 
binary rainfall data files to text files. Next, it will call makeRainDBF.py to calculate area-weighted average precipitation
data in each woreda or kebele.

makeRainDBF.py first calls intersectGrid.py to determine the percentage of each woreda's or kebele's area occupied by each NOAA
grid cell. Next, it calls readRainData.py to read in all of the data from the points in Ethiopia and stores it in the matrix
allData. makeRainDBF.py then calls findRainWeightMatrix.py to determine the weights of each grid cell to apply to each woreda or
kebele when calculating area-weighted average precipitation and stores them in WeightMatrix. Finally, it finds the dot product 
of allData and WeightMatrix to determine these area-weighted averages.

The output is either WoredaRainDBF.csv or KebeleRainDBF.csv, depending on which level was chosen. The weight matrix will also be
written to RainWoredaWeightMatrix.csv or RainKebeleWeightMatrix.csv.
