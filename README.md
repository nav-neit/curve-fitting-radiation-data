# PHN-319 Technical Communication course -  Report

## Sensitivity Analysis of Calibration Methods and Factors Effecting the Statistical Nature of Radiation Measurement

1) Datasets:
	Processed 2058 files given for each detector: 
	-> Each text file contributed a single datapoint of format (Time,HV,LLD,AMP,COUNTS) , for 'COUNTS' mean of 
	  counts from each text file was taken.
	-> Thus for each detector a single csv file of 2058 data points was made.

2) Data Analysis:
	-> Plotted Histograms of each variables to find the range in which each variable lies.
	-> From the histograms it is clear that the data need to be scaled (using standard scaling technique) before fitting.
	-> KDE plot of COUNTS show that it has a right skewed distribution, so median is a suitable for analysis.
	-> Scatter Plots show that the entire data set is not an output of random observations in the 5-D space.
	-> Correlations:
		-> Used Spearman's correlation , since there is non-linearity in the data set and the distribution of
		   variables is not Gaussian, so Pearson correlation cannot be used.
		-> From correlation coeff and p value it is clear that 'TIME' has major contribution in radiation measurement.
		-> LLD has corr coeff close to 0 and p-value is very high , implies it has less contribution in 
		   radiation measurement.This is almost true since the power of LLD in the polynomial eqn in the article is
		   -13.5.
3) Models:
	-> There exists a nonlinear relationship between the variables and COUNTS as specified in the Article, based on this 
	   fact chosen 3 algorithms that accounts nonlinearity to build the model.
	
	1) Deep Learning Model:
	   -> Used Tensorflow , 4-neurons:input layer, (5-neurons) *2:Hidden layers, 1-neuron:output layer
	   -> activation fun:sigmoid,optimizer used:RMSprop , loss function:mean-absolute-error // combination of these
               were found to be optimum after testing with several other activation funs,optimisers,loss funs etc.
	   -> error of about 54% // Intutive reason: May be due to underfitting since the dataset is not very large.
	
	2) Curve fitting using multivariate polynomial regression
	   -> The final scatter plot shows that ther is a moderate overlap between predicted and origianl counts.
	
	3) Support vector Regression using Gaussian Radial Basis Function
	  -> Has a much better overlap between predicted and original counts than the MPR model.

Final Conclusion:
	Through data analysis we are able to conclude that the relationship btw the variables and COUNTS is in accordance
	with the model given in the paper , it obeys correlations.
	Also median is a suitable tool to work with.
	From the above 3 ML models SVR model has almost similar predictions compared to the other two models even though 
	the model is not a viable representation of process.