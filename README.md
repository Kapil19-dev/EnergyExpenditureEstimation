# EnergyExpenditureEstimation
[![Build Status](https://travis-ci.com/pslade2/EnergyExpenditureEstimation.svg?token=4VLDzfdsFLSp6zXCt5rM&branch=master)](https://travis-ci.com/pslade2/EnergyExpenditureEstimation)
This is the repository for the "Rapid energy expenditure estimation for assisted and inclined loaded walking" research paper. Please cite this paper if you use a portion of our project. In this work we trained models using input features of muscle activity (EMG) and ground reaction forces to estimate energy expenditure during walking (1) with an ankle exoskeleton and (2) during various loaded and inclined walking conditions. These estimates were made every single gait cycle. We measure the performance of these models for cases where conditions or subjects data are not included in the training data to simulate real use cases. For research or clinical experiments where the accuracy of our models is sufficient these can be used to replace the standard indirect calormitery methods of estimating energy expenditure which require expensive equipment and provide slow, noisy measurements. This repository contains the relevant formatted datasets, code to train models, and final model parameters to recreate our reported results. This code base should offer a support to apply our techniques to new datasets or utilize our fully trained models.

CODE:

Linear Regression - The linear regression code is contained in LR.ipynb. This file can be used to train a single model or average the performance over all subjects by setting the variable "subject_test" to "True". The performance metrics and weights of the trained models are printed at the end of the script. In order to reproduce our results, select the corresponding data folder you would like to use with the "folder_name" variable and the type of data split you would like to test by setting the variable "data_type" to "conditions", "subjects", or "subjcond".

Neural Networks - The low-level implementation of the fully connected neural network model is in the "NNModel.py" file. The interactive neural network code for training, developement, and testing is contained in main.ipynb. The code in the file "main.py" is identical to "main.ipynb" but can be run without jupyter notebooks (see file for instructions). These files can be used to train a single model for development, perform a hyperparameter sweep to determine the best neural network paramters, or average performance over all subjects by changing the "sim_type" variable to "sm", "hps", or "subj", respectively. The specifications for any of these different use cases is defined in the ".json" files in the settings folder. The network parameters for the trained networks reported in our results are already given in the .json files that end with "subj". These can be run to reproduce our results. An additional .json file example for the single model (ending with "sm") and hyperparameter search (ending with "hps") has been added as an example. The low-level tensorflow code for the hyperparameter sweeping is in the "paramSearchHelper.py" file. Some additional tensorflow code for saving models used throughout the other scripts is saved in the "utils.py" file. 

Supporting files - Both programs rely on the "dataHelp.py" file which contains miscellaneous functions for segmenting the data for the different tests, normalization code, binning the input singals appropriately, and others. 

SOFTWARE: 

The files were written in Python 3 and require the following packages and dependencies: numpy, scipy, matplotlib, ipython & ipython-notebook (all 5 available at: https://www.scipy.org/install.html), scikit-learn (http://scikit-learn.org/stable/install.html), and tensorflow (https://www.tensorflow.org/install/). Please refer to Jupyter on how to install Jupyter notebooks (http://jupyter.org/install) for Python 3 in order to view open and run the given iPython notebooks.

DATA: 

The folders containing the filtered data are named for the corresponding "assisted" or "incline-load" datasets sorted by "subjects" or "conditions" for use in running the three different datasplits. The files entitled "x" contain the input signal data with each column representing a different input signal. The files entitled "y" contain the measured metabolic signals, averaged for each condition. There are four columns for different normalized and offset metabolics, only the unprocessed energy expenditure in the first column should be used. For the assisted dataset, the abbreviated input labels in order of the "x.csv" file are: "Fx_R", "Fy_R", "Fz_R", "Fx_L", "Fy_L", "Fz_L", "MGAS_R", "LGAS_R", "MSOL_R", "LSOL_R", "TA_R", "VASM_R", "RF_R", "BF_R", "MGAS_L", "LGAS_L", "MSOL_L", "LSOL_L", "TA_L", "VASM_L", "RF_L", "BF_L". The first 6 represent the different ground reaction forces, with the rest being EMG signals. The incline-load dataset input signal abbreviations are: "Fx_R", "Fy_R", "Fz_R", "Fx_L", "Fy_L", "Fz_L", "SOL", "GAS", "TA", "MH", "BF", "VM", "VL", "RF". Again, the first 6 are ground reaction forces and the rest are EMG signals.
