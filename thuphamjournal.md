# Part 0: Acquiring data

> **12:00 pm Nov 6 2018**

We accquired 2 dataset from Kaggle. 
1. Google Store data: https://www.kaggle.com/lava18/google-play-store-apps
2. AppStore data: https://www.kaggle.com/ramamet4/app-store-apple-data-set-10k-apps

Two datasets include similar variables and can be very valuable to analyze the growth of applications from two most popular platform - Android vs Apple.
Zach and I started looking into the data to standardize what we have in common and could be useful from two dataset. 

> **3:00 pm Nov 7 2018**
Since we cannot not merge them together because the app ID/Name is not identical, we have to set some rules to make sure our workflow was consistent with the other’s:

1. Formulate the clean dataset. Looking at the data we got, think of how it is going to look like after cleaning, which variable will be useful, which variable we could not utilize will be eliminated.
2. Identify the area we do not want in our dataset.
3. Standardize our variable names. Each colum in each dataset will be renamed the same way. We all use lower case, underscore to separate to word. this is to make sure it’s easy to reference both datasets in a uniform fashion


# Part 1: Cleaning data

> **11:30 am Nov 8 2018**

I am responsible for the Google Play Store dataset. I work on this project entirely on jupyter notebook. I know that Zach prefers cleaning this datat with Excel but I find it more efficient for me to be consistent in my method.
I start by importing packages as one should do. Since we are working with CSV data, we will need pandas to read our data. Other packages will be helpful for visualization.

```
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
```
> **5:30 pm Nov 8 2018**

After reading my data from **pandas**, I renamed all the columns with lowercase characters.
```
googleStore.rename(columns={'App': 'app', 'Rating': 'rating', 'Reviews': 'reviews', 'Size': 'size', 'Price': 'price', 'Genres': 'genres'}, inplace=True)
```

By reading the data file, I also find some duplicate columns like Genres and Category are basically the same. I decided to drop Category columns. Those columns like "Last Update", "Current Ver", "Android Ver" are not necessarily useful to be included in the dataframe. I also drop them.

```
googleStore = googleStore.drop(columns=['Category', 'Installs', 'Type', 'Last Updated', 'Current Ver', 'Android Ver'])
```

> **11:30 am Nov 10 2018**

Zach and I communicate through email. I spend class time to work on our project together. Within an hour in-class work, we also check on each other's progress to make sure we are on the same page. If there are any changes or differences, we work on that. Then by the end of class, we set some guidelines for individual responsibility when we cannot meet in person.

We start standardizing our dataset. 
- Size column: Convert to pure bytes (M = 1000). Make sure there is no unit after every cell value
```
googleStore['size'] = googleStore['size'].replace({'M': ''}, regex=True)
```
- Price: Get rid of the '$'
```
googleStore['price'] = googleStore['price'].replace({'\$': ''}, regex=True)
```
- Rating: If Everyone 10+ then convert to use 10 so on so forth, 12+ is Teenager and 17+ is Adults
```
googleStore = googleStore.replace('Teen', 12)
googleStore = googleStore.replace('Everyone', 0)
googleStore = googleStore.replace('Mature 17+', 17)
```
- Genres: Try and either separate the genres with multiple answers or just grab the first one.
```
googleStore['genres'] = googleStore['genres'].apply(lambda x: x.split(',')[0])
```

> **5:30 pm Nov 10 2018**

I start working on creating repository on Github after our data processing are going. Our shared repository on Github includes 2 raw dataset from Apple App Store and Google Play Store. I include my journal in this repository while Zach keeps his on Google Drive.

But with Github, we can easily keep track each other's process and keep our data updated.

> **7:30 pm Nov 10 2018**

I finish cleaning my data at 7:30. The cleaned, processed dataset was save as **googleData.csv**
```
googleStore.to_csv('googleData.csv', encoding='utf-8', index=False)
```

# Part 2: Analyzing and Visualizing Data

> **11:30 am Nov 13 2018**

## 1. Create function to add data to plot

Before plotting any chart or graph, I find it be more efficient to create a function to handle plotting. The function uses **seaborn** package.
```
def plot(ax,w,h):
    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)
    for p in ax.patches:
        ax.annotate('{}'.format(p.get_height()), (p.get_x()+w, p.get_height()+h))
```

## 2. Compare apps with more review - popular or well-received apps vs less popular apps

Values from *Review* are stored as string data. Hence, to use them to plot, I have to change their data type to numerical. This task can be easily done with **pandas**.

There are two categories I care in the graph: popular apps with more than 250,000 reviews, and less popular app with less than 250,000 reviews. Pie chart would work best in this case. We have not gone through pie chart in class, but it is not complicated to be done with **matplotlib** package.

```
# Plot
plt.pie(sizes, labels=labels, colors=colors,
        autopct='%1.1f%%', shadow=True,startangle=90)

plt.title('Pie Chart of App Popularity')
plt.axis('equal')
plt.show()
```

> **7:30 pm Nov 13 2018**

## 3. Compare size of Apps

Continue with pie chart, I want to plot a similar chart like I did with popular apps but this time with large size apps instead.

Zach came up with this idea because in his dataset from Apple App Store, the majority of apps are quite big in memory occupation. We categorize those apps with more than 20MB in size are large.

```
large_apps = googleStore[googleStore['size'] > 20000000]
small_apps = googleStore[googleStore['size'] < 20000000]
labels=['Large Apps','Small Apps']
sizes = [large_apps.shape[0],small_apps.shape[0]]
colors = ['blue','orange']

# Plot
plt.pie(sizes, labels=labels, colors=colors,
        autopct='%1.1f%%', shadow=True,startangle=90)

plt.title('Pie Chart of App Size')
plt.axis('equal')
plt.show()
```
Interestingly, 68% of apps from Google Play Store are small app (<20MB). This can be explained by the fact that Apple has more comprehensive and strict guideline to approve an app which leads to more usable, atrractive user interface and sophisticated programming. 

> **11:30 am Nov 15 2018**

## 4. Compare free vs paid Apps

Price is one of our most concerned variable. To answer our big question, analyzing how free and paid apps are doing in the market is essential. We compare free vs paid app in several categories. This gives us an insight to put in our analysis conclusion. 

> **5:30 am Nov 15 2018**

###### Number of Free vs Paid apps

The first thing I have to do is to change the Price data type in to numeric. Then identify free apps are those whose prices equal 0. Pie charts continue working best in this case.

Compare my result to Zach's, there is a large difference between the “Pay-To-Play” scene on the two separate app stores. As we can see the Apple Store has 43.6% of their apps with a price tag on them while the Google Store only has about 7.4% of their apps with a price tag on them.

> **3:00 pm Nov 16 2018**

###### Compare user rating between free and paid apps

This chart took me an hour to create because I want to put them sibe by side for comparision. I found out that *subplot* is the function I was looking for. Afther that, use **seaborn countplot** to collect the number of user ratings for each app.

I encountered an app with a rating of 19.0 in the free apps, we truly aren’t sure what made this app so good that it broke the 0.0-5.0 system but it’s there, named “Life Made WI-Fi Touchscreen Photo Frame”. But overall, the distribution between free vs paid app are quite similar. Rating 0 is likely an outlier. The app distributions are left-skewed with one peek at around 4.5.

> **10:00 am Nov 17 2018**

###### App Distribution by Genres

As I am more familiar to plotting charts and graphs, this process move quickly. Zach and I continue updating our Githun so we know who is doing what and keep each other on the same page. We complement each other so at this state, we are comfortable to present on the first day. 

Here is how I plot app distribution by genres:
```
plt.figure(figsize=(10,12))
ax=sns.countplot('genres',data=googleStore,palette="Set1",order=googleStore['genres'].value_counts().index)
plt.xlabel('GENRES')
plt.ylabel('APPS')
plt.xticks(rotation=80)
plot(ax,1,2)
```

> **3:00 pm Nov 18 2018**

###### Top 20 most expensive apps on Google Store by Genre

Interesting thing comes along when I found out the top expensive apps by genre. Thinking how much one person pays for one install, it must be worth it. Or not? In my daya, the most expensive app worths $400 and it is **I'm Rich - Trump Edition** category Lifestyle. When I told Zach my discovery, we both thought it could make some good laughs during our presentation. 

> **11:30 pm Nov 20 2018**

Zach and I meet in class to check on each other's progess. I think we are doing well. In term of progress, I guess we make to 75% completion of our data analysis. We both will complete this step during Thanksgiving break while keep each other updated. The next step when we get back after break is working on the website and our presentation. Zach and I agree that we can do our presentation on the first day with this rate.

## 5. Content Rating

For content rating, I have 4 categories: 0 for everyone/unrated, 12 for teenagers, 17 for mature, and somehow Google Play has 18 for adults. I plot the bar chart for content rating distribution 

```
plt.figure(figsize=(8,8))
ax=sns.countplot('cont_rating',data=googleStore,palette="Set1",order=googleStore['cont_rating'].value_counts().index)
plt.xlabel('Content Rating')
plt.ylabel('Apps')
plot(ax,0.2,1)
```

There is one big thing we need to work on during break is to graph content rating by genre. It will takes time because we have different rating criterion.

> **11:00 am Nov 24 2018**
###### Content rating by Genre

Turn out that it does not take too much time as I expected. In the end, I have 4 bar charts for each content rating criterion. Another fun thing to point out is that the Google Play Rated R is mainly “Dating” apps, interesting.

Here is the summary on my dataset:
- Finance category make the most revenue from app store.
- Genres distributions vary between each content rating age. Tool apps lead the content for everyone while entertainment are most popular among teenagers. Interestingly, there is a tremendous amount of dating apps for adults.
- Free apps and Paid apps have significant difference in numbers.
- However, rating distribution between free and paid apps are nearly the same.
- 2/3 of apps from Google Play Store are small apps which takes less than 20MB in your device memory.

> **7:00 pm Nov 26 2018**

We met in the library at 7 pm on that day to work on the website. Since I own the repository, I am responsible fore generating an SSH Key then create the website. Zach takes care of writing the content, description for our analysis. 
None of us has prior experience with **Sphinx**. So we both learn together. It took me an hour to get around and have everything ready to edit. I successfully generated a **Sphinx** website and what we need to do is to put up our analysis and notebook on the web.

> **7:00 pm Nov 27 2018**

# Part 2: Creating Sphinx Website

While Zach was writing the description for our graph, I outlined the website so we could organize our presentation the day after. 

Reading the presentation rubric, I started out with a general goal of this project is to practice the skills we learn in class while broadening our knowledge. Then I move onto our dataset and stated our big question to answer. Each stage of this data analysis is clearly pointed out based on my journal. I find it extremely helpful to have a journal. So it did not take me too long to have a well-orgainzed website. 

> **10:00 pm Nov 27 2018**

# Part 3: Conclusion

Zach and I wrote this part together. After 3 weeks of exploring and constantly learning, I feel that we have grown so much knowing all the things we learn could come to use.

> With all the commotion around Phones and more specifically, Apps, there is little to dispute when we bring up the fact that it is an ever growing business with a nearly limitless audience as well as potential to become bigger every second. It is also very important to point out that there is a large difference when it comes to getting your app into these two separate stores; it is a fairly easy process to get your app into the Google Store while it is quite difficult to get past Apple’s standards for apps on their store. This can skew the data as we have a very diluted store as opposed to a store that has a set of standards to even attempt to get in. This analysis is just the tip of the iceberg when it comes to the online entertainment industry since the internet is an ever-growing industry, there needs be constant analysis of the trends that prove to make certain platforms successful and we hope to have intrigued your thought process of the App Industry.

> **7:30 pm Nov 28 2018**

We met one last time at the library to run through the presentation together. To make the presentation intrigued, I suggestes we should start out with a question like: How many time in a day do you pick up your phone and not use an app? I will have people raise hand if it is less than 5 times.

And then Zach and I will alternate going through each main points in our analysis. We want everybody to have fun and learn something from our presentation as well.


> **1:00 pm Nov 29 2018**

After the presentation, we believed that we did our best. This is the last entry in this journal. I thank Zach for being a great partner and our professor who has always been a great help.
Even though we felt proud of our performance, there are spaces to improve. We could have state our conclusion clearer to answer the question from the begining. We should also have shorten some parts so I did not run out of time.
 
