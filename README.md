## Support Vector Machines in Smile detection: A comparison of auto-tuning standard processes in Gaussian kernel

#### Order to run the scripts

*All the scrips made for the balanced have "-balanced" at the end, to run justa add it to the end of the filename.*

 1. createHoldOuts.ipynb
 2. trainSVM_holdouts.ipynb 
 3. trainSVM_holdouts-proba.ipynb
 4. trainSVM_proba_1holdout.ipynb

#### To prepare the sigest ranges:

Open R studio and run:

    require("reticulate")  
	require('kernlab')  
	source_python("read_pickle.py")  
	df <- data.frame(firstquantile=c(), median=c(), secondquantile=c())  
  
	for (i in 1:100){  
	a = paste("train_features_HOGShape_", i, ".pkl", sep="")  
	pickle_data <- read_pickle_file(a)  
	sig = sigest(pickle_data, frac = 0.5, scaled = TRUE, na.action = na.omit)  
	de <- c(sig[1][1], sig[2][1], sig[3][1])  
	df <- rbind(df, de)  
	}  
  
	colnames(df) <- c("01quantile", "median", "09quantile")  
	write.csv(df, "sigmas_frac0.5_mean.csv", row.names = FALSE)

#### To create image with the SVM's decision function run:

 - plot_rbf_parameters.ipynb
