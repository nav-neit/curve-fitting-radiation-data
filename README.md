# PHN-319 Technical Communication course -  Report

## Data Analysis and curve fitting on scintillation detector data

* Datasets used:
	- Processed 2058 files given for each detector: 
	- Each text file contributed a single datapoint of format (Time,HV, LLD,AMP,COUNTS) , for 'COUNTS' mean of counts from each text file was taken.
	- Time, HV (High Voltage), LLD (lower limit discriminant), AMP(amplifier value) are the independent variables and COUNTS is the dependent variable.
	- for each detector a single csv file of 2058 data points was made.

* Data Analysis performed:
	1. Visualizations
		- Plotted Histograms of each variables to find the range in which each variable lies.
		- From the histograms it is clear that the data needs to be scaled (using standard scaling techniques) before fitting.
		- KDE plot of COUNTS show that it has a right skewed distribution, so median is a suitable for analysis.
		- Scatter Plots show that the entire data set is not an output of random observations in the 5-D space.
	2. Correlations
		- Used Spearman's correlation , since there is non-linearity in the data set and the distribution of variables is not Gaussian, so Pearson correlation cannot be used.
		- From correlation coeff and p value it is clear that 'TIME' has major contribution in radiation measurement.
		- LLD has corr coeff close to 0 and p-value is very high,implies it has less contribution in radiation measurement.
* Models:
	- There exists a nonlinear relationship between the variables and COUNTS as specified in the Article, based on this fact chosen 3 algorithms that accounts nonlinearity to build the model.
	
	1. Deep Learning Model:
		* Used Tensorflow , 4-neurons:input layer,5-neurons*2:Hidden layers, 1-neuron:output layer
	   	* Activation function:sigmoid,optimizer used:RMSprop ,loss function:mean-absolute-error // combination of these were found to be optimum after testing with several other activation functions,optimisers,loss funs etc.
	    * Error of about 54% // Intutive reason: May be due to underfitting since the dataset is not very large.
	
	2. Curve fitting using multivariate polynomial regression
	   * The final scatter plot shows that ther is a moderate overlap between predicted and origianl counts.
	
	3. Support vector Regression using Gaussian Radial Basis Function
	  * Has a much better overlap between predicted and original counts than the MPR model. R_squared value > 90%.

#### Final Conclusion:
##### Through data analysis we are able to conclude that the relationship btw the variables and COUNTS is in accordance with the model given in the paper , it obeys correlations. Also median is a suitable tool to work with.From the above 3 ML models SVR model has almost similar predictions compared to the other two models even though the model is not a viable representation of process.