# Part 0: Acquiring data

**Nov 6 2018**

We accquired 2 dataset from Kaggle. 
1. Google Store data: https://www.kaggle.com/lava18/google-play-store-apps
2. AppStore data: https://www.kaggle.com/ramamet4/app-store-apple-data-set-10k-apps

Two datasets include similar variables and can be very valuable to analyze the growth of applications from two most popular platform - Android vs Apple.
Zach and I started looking into the data to standardize what we have in common and could be useful from two dataset. 

Since we cannot not merge them together because the app ID/Name is not identical, we have to set some rules to make sure our workflow was consistent with the other’s:

1. Formulate the clean dataset. Looking at the data we got, think of how it is going to look like after cleaning, which variable will be useful, which variable we could not utilize will be eliminated.
2. Identify the area we do not want in our dataset.
3. Standardize our variable names. Each colum in each dataset will be renamed the same way. We all use lower case, underscore to separate to word. this is to make sure it’s easy to reference both datasets in a uniform fashion


# Part 1: Cleaning data

**Nov 8 2018**

I am responsible for the Google Play Store dataset. I work on this project entirely on jupyter notebook. I know that Zach prefers cleaning this datat with Excel but I find it more efficient for me to be consistent in my method.
I start by importing packages as one should do. Since we are working with CSV data, we will need pandas to read our data. Other packages will be helpful for visualization.

```
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
```
