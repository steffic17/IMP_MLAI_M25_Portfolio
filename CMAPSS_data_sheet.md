# Datasheet for CMPASS dataset

This datasheet has been created for the CMPASS Jet Engine Simulated dataset created by NASA.

## Motivation

This dataset was created to model damage propogation in a simulated aircraft engine run-to-failure.

The dataset was created by Abhinav Saxena, Kai Goebel, Don Simon and Neil Eklund.  This work was supported in part by the U.S. National Aeronautics and Space Administration (NASA) under the Integrated Vehicle Health Management (IVHM).
Abhinav Saxena is with Research Institute for Advanced Computer Science at NASA Ames Research Center.
Kai Goebel and Don Simon are with NASA Ames Research Center.
Neil Eklund is with GE Global Research.


 
## Composition

Data sets consists of multiple multivariate time series. Each data set is further divided into training and test subsets.

The data sets consist of 12 files: 4 training set data files, 4 test set data files and 4 RUL (test set "truth") data files. These each contain:
- file reference FD001, contains 20631 training instances, and 13096 test instances and 100 RUL instances.
- file reference FD002, contains 53759 training instances, 33991 test instances and 259 RUL instances.
- file reference FD003, contains 24720 training instances, 16596 test instances and 100 RUL instances.
- file reference FD004, contains 61249 training instances, 41214 test instances and 248 RUL instances.

Each training and test instance contains:
1) unit number
2) time, in cycles
3) operational setting 1
4) operational setting 2
5) operational setting 3
6) sensor measurement 1
7) sensor measurement 2
...
26) sensor measurement 26

Each RUL instance contains:
1) RUL, true remaining useful life

The sensors represent the following C-MAPSS output parameters:
- T2 Total temperature at fan inlet in °R
- T24 Total temperature at LPC outlet in °R
- T30 Total temperature at HPC outlet in °R
- T50 Total temperature at LPT outlet in °R
- P2 Pressure at fan inlet in psia
- P15 Total pressure in bypass-duct in psia
- P30 Total pressure at HPC outlet in psia
- Nf Physical fan speed in rpm
- Nc Physical core speed in rpm
- epr Engine pressure ratio (P50/P2) (no units)
- Ps30 Static pressure at HPC outlet in psia
- phi Ratio of fuel flow to Ps30 in pps/psi
- NRf Corrected fan speed in rpm
- NRc Corrected core speed in rpm
- BPR Bypass Ratio (no units)
- farB Burner fuel-air ratio (no units)
- htBleed Bleed Enthalpy (no units)
- Nf_dmd Demanded fan speed in rpm
- PCNfR_dmd Demanded corrected fan speed vrpm
- W31 HPT coolant bleed in lbm/s
- W32 LPT coolant bleed in lbm/s

Each time series is from a different engine i.e., the data can be considered to be from a fleet of engines of the same type. Each engine starts with different degrees of initial wear and manufacturing variation which is unknown to the user. This wear and variation is considered normal, i.e., it is not considered a fault condition. There are three operational settings that have a substantial effect on engine performance. These settings are also included in the data. The data is contaminated with sensor noise.

The engine is operating normally at the start of each time series, and develops a fault at some point during the series. In the training set, the fault grows in magnitude until system failure. In the test set, the time series ends some time prior to system failure.

A training/test split is provided for the dataset – there is no rationale described for this split.

The dataset is self-contained and there is no missing data.

The dataset does not contain data that might be considered confidential, offensive, insulting, threatening or might be considered sensitive in any way.



## Collection process

The aero-propulsion system simulator CMAPSS was used to simulate aircraft engine run-to-failure with damage propogation modelled in aircraft gas turbine engines.

This dataset is not part of a larger subset. 

The dataset was simulated prior to publication of the paper A Saxena et al., 2008 [1].



## Preprocessing/cleaning/labelling

There was no preprocessing or cleaning of the data done as it is simulated.  However, it is noted that the sensor data contains noise, the rationale for which is unknown to the authors of the datasheet.



## Uses

This data set could also be used to determine the probability of engine failure or probability of a specified level of RUL.

Due to the nature of the data set collection process, i.e. simulated, it should be used with caution as a proxy for real aircraft engines.

These data sets should not be used to predict RUL on any specific aircraft engine or fleet of aircraft engines.



## Distribution

The data sets are published by the Prognostics Center of Excellence (PCoE) via NASA's Open Data Portal [2] under a Public Domain License.  The data sets are also widely available through a number Kaggle projects.



## Maintenance

The data sets are maintained by Chris Teubert at NASA's Open Data Portal [2].



[1]  A Saxena, K Goebel, D Simon, N Eklund, "Propagation Modeling for Aircraft Engine Run-to-Failure Simulation", 2008
[2]  NASA, "NASA's Open Data Portal", https://data.nasa.gov/Aerospace/CMAPSS-Jet-Engine-Simulated-Data/ff5v-kuh6, last accessed on February 2023.
