*************************************************************************************************************
The time period covered by the dataset is until Feb 01 2015
*********************************************************************************************************

Data file: https://people.phys.ethz.ch/~ caplarn/PTF/Data.tar.gz

Each chip *.tar.gz file contains *.csv files with the light curves of the individual objects. The name of each file is InternalIdentificationNumber_RA_DEC.csv.

Each file has a following structure:

	First line: 1. Redshift, 2. Mass, 3. Luminosity, 4. Ra, 5.Dec

	All subsequent lines: 1. PTF field, 2. number of the observation*, 3. date**, 4. re-calibrated magnitude***, 5. re-calibrated error***, 6. instrumental magnitude****, 7. error****, 8. zeropoint with which to correct instrumental magnitude****



*counted backwards (i.e. latest observation has number 1.)
**date in the restframe i.e. observational date already divided by (1+z), where z is redshift. If interested in actual observational date multiply this value by (1+z) to get MJD date of the observation.
*** Re-calibration from Caplar+ 2016 
**** From the initial PTF catalogue, Ofek+ 2012 
