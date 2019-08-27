# Data from the paper:  Optical Variability of AGNs in the PTF/iPTF Survey (2017ApJ...834..111C) 

*************************************************************************************************************
The time period covered by the dataset is until Feb 01 2015
*********************************************************************************************************

Data file: https://people.phys.ethz.ch/~caplarn/PTF/Data.tar.gz

When you un-tar the Data file, you will will presented with directories, contaning light-curves from each chip. Each chip directory contains *.csv files with the light curves of the individual objects. The name of each file is InternalIdentificationNumber_RA_DEC.csv.

Each file has a following structure:

	First line: 1. Redshift, 2. Luminosity, 3. Mass, 4. Ra, 5.Dec

	All subsequent lines: 1. PTF field, 2. number of the observation*, 3. date**, 4. re-calibrated magnitude***, 5. re-calibrated error***, 6. instrumental magnitude****, 7. error****, 8. zeropoint with which to correct instrumental magnitude****



*counted backwards (i.e., the latest observation is number 1) <br/>
**date in the restframe i.e., the observational date already divided by (1+z), where z is redshift. If interested in actual observational date multiply this value by (1+z) to get MJD date of the observation <br/>
*** Re-calibration from Caplar+ 2016  <br/>
**** From the initial PTF catalogue, Ofek+ 2012 <br/>

In order to import the light-curves from *.csv files I recommend something like 

        single_LC=[]
        with open(<path to the *.csv file>) as csvDataFile:
            csvReader = csv.reader(csvDataFile)
            for row in csvReader:
                if len(row)==5:
                    single_LC_physical_parameters=np.array(row).astype(float)
                if len(row)>5:
                    single_LC.append(np.array(row).astype(float))

        single_LC=np.array(single_LC)
	
	
This will then give you `single_LC array` containg all the observed data, while the physical parameters are contained in separate `single_LC_physical_parameters array`. As an example, in order to see the data, with the x-axis showing the observation dates we could do:


	single_LC_original_time=np.copy(single_LC)
	single_LC_original_time[:,2]=single_LC_original_time[:,2]*(1+single_LC_physical_parameters[0])

	plt.figure(figsize=(20,6))
	plt.errorbar(single_LC_original_time[:,2],single_LC_original_time[:,3],yerr=single_LC_original_time[:,4],ls='',fmt='o')
	plt.ylabel('magnitude',fontsize=18)
	plt.xlabel('MJD',fontsize=18)
	plt.xticks(fontsize=14)
	plt.yticks(fontsize=14)
	
![Example data](https://www.dropbox.com/s/ofthk04nfub6cxl/Example.png?raw=1)

