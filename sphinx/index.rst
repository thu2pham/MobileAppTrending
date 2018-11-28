.. Data Visualization Website documentation master file, created by
   sphinx-quickstart on Tue Nov 20 12:04:49 2018.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Data Visualization Website's by Thu & Zach!
======================================================

.. toctree::
   :maxdepth: 2
   :caption: Table of Contents:


The goal of this project is to practice the analytical skills we learn throughout this semester. We choose the datasets and ask ourselves what kind of question we can and want to answer from our sources.
We build this website to share what we have learned and discovered from that journey.
   
Data Acquisition
---------------------

We started by going to Kaggle and retreiving two datasets.
  * `Apple Store dataset <https://www.kaggle.com/ramamet4/app-store-apple-data-set-10k-apps>`_
  * `Google Store dataset <https://www.kaggle.com/lava18/google-play-store-apps>`_
These two datasets give us a big picture about mobile apps since Google Store and App Store are now two biggest sources in the market. Taken as a whole, the data shows some interesting correlations more than just a vast list of apps and prices. These two are extremely valuable to compare as a big picture. However, one disadvantage of these dataset is that we could not merge them together since the app ID is not identical. Hence, when working with the data, we have to go back and forth between two datasets.

Knowing the disadvantage of our data, each of us work with one dataset but we have some rules to make sure our workflow are consistent and on the same page:
#. Formulate the clean dataset. Looking at the data we got, think of how it is going to look like after cleaning, which variable will be useful, which variable we could not utilize will be eliminated.
#. Identify the area we do not want in our dataset.
#. Standardize our variable names. Each colum in each dataset will be renamed the same way. We all use lower case, underscore to separate to word.

Data Cleaning
---------------

Importing packages
++++++++++++++++++++
We start by importing packages. Since we are working with CSV data, we will need *pandas* to read our data. Other packages will be helpful for visualization.
.. code-block:: python

    import pandas as pd
    import numpy as np
    import seaborn as sns
    import matplotlib.pyplot as plt

Renaming and Dropping 
+++++++++++++++++++++++
As we talked earlier, in order to work with two separate dataset, we need to standardize each of the. So we started by renaming those columns that we believe is going to be used for further analysis and getting rid of unnecessary items. Zach made his changes directly on his CSV file from Excel while I used Python. We did not want to limit our tools when approaching data.
Note that I dropped some columns and renamed others in the following code
.. code-block:: python

    googleStore.rename(columns={'App': 'app', 'Rating': 'rating', 'Reviews': 'reviews', 'Size': 'size', 'Price': 'price', 'Genres': 'genres'}, inplace=True)
    googleStore = googleStore.drop(columns=['Category', 'Installs', 'Type', 'Last Updated', 'Current Ver', 'Android Ver'])

Bar Chart for count of price of apps for genres
-------------------------------------------------


Total price of paid apps in each genre
----------------------------------------


Bar Chart for count of content rating
---------------------------------------

Pie chart for free vs paid apps counts
------------------------------------------

pie chart for size comparison
-------------------------------

pie chart for reviews
-----------------------


most expensive apps by genres 
--------------------------------

bar chart for rating of free vs paid apps
--------------------------------------------

content rating by genres
--------------------------

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
