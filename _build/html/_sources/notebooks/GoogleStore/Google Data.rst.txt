
.. code:: ipython2

    import pandas as pd
    import numpy as np
    import seaborn as sns
    import matplotlib.pyplot as plt

.. code:: ipython2

    googleStore = pd.read_csv('google-play-store-apps/googleplaystore.csv', encoding = "ISO-8859-1")
    googleStore.head(5)




.. raw:: html

    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }
    
        .dataframe tbody tr th {
            vertical-align: top;
        }
    
        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>App</th>
          <th>Category</th>
          <th>Rating</th>
          <th>Reviews</th>
          <th>Size</th>
          <th>Installs</th>
          <th>Type</th>
          <th>Price</th>
          <th>cont_rating</th>
          <th>Genres</th>
          <th>Last Updated</th>
          <th>Current Ver</th>
          <th>Android Ver</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>Photo Editor &amp; Candy Camera &amp; Grid &amp; ScrapBook</td>
          <td>ART_AND_DESIGN</td>
          <td>4.1</td>
          <td>159</td>
          <td>19M</td>
          <td>10,000+</td>
          <td>Free</td>
          <td>0</td>
          <td>Everyone</td>
          <td>Art &amp; Design</td>
          <td>7-Jan-18</td>
          <td>1.0.0</td>
          <td>4.0.3 and up</td>
        </tr>
        <tr>
          <th>1</th>
          <td>Coloring book moana</td>
          <td>ART_AND_DESIGN</td>
          <td>3.9</td>
          <td>967</td>
          <td>14M</td>
          <td>500,000+</td>
          <td>Free</td>
          <td>0</td>
          <td>Everyone</td>
          <td>Art &amp; Design;Pretend Play</td>
          <td>15-Jan-18</td>
          <td>2.0.0</td>
          <td>4.0.3 and up</td>
        </tr>
        <tr>
          <th>2</th>
          <td>U Launcher Lite äóñ FREE Live Cool Themes, Hid...</td>
          <td>ART_AND_DESIGN</td>
          <td>4.7</td>
          <td>87510</td>
          <td>8.7M</td>
          <td>5,000,000+</td>
          <td>Free</td>
          <td>0</td>
          <td>Everyone</td>
          <td>Art &amp; Design</td>
          <td>1-Aug-18</td>
          <td>1.2.4</td>
          <td>4.0.3 and up</td>
        </tr>
        <tr>
          <th>3</th>
          <td>Sketch - Draw &amp; Paint</td>
          <td>ART_AND_DESIGN</td>
          <td>4.5</td>
          <td>215644</td>
          <td>25M</td>
          <td>50,000,000+</td>
          <td>Free</td>
          <td>0</td>
          <td>Teen</td>
          <td>Art &amp; Design</td>
          <td>8-Jun-18</td>
          <td>Varies with device</td>
          <td>4.2 and up</td>
        </tr>
        <tr>
          <th>4</th>
          <td>Pixel Draw - Number Art Coloring Book</td>
          <td>ART_AND_DESIGN</td>
          <td>4.3</td>
          <td>967</td>
          <td>2.8M</td>
          <td>100,000+</td>
          <td>Free</td>
          <td>0</td>
          <td>Everyone</td>
          <td>Art &amp; Design;Creativity</td>
          <td>20-Jun-18</td>
          <td>1.1</td>
          <td>4.4 and up</td>
        </tr>
      </tbody>
    </table>
    </div>



.. code:: ipython2

    googleReview = pd.read_csv("google-play-store-apps/googleplaystore_user_reviews.csv", encoding = "ISO-8859-1")
    googleReview.head(5)




.. raw:: html

    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }
    
        .dataframe tbody tr th {
            vertical-align: top;
        }
    
        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>App</th>
          <th>Translated_Review</th>
          <th>Sentiment</th>
          <th>Sentiment_Polarity</th>
          <th>Sentiment_Subjectivity</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>10 Best Foods for You</td>
          <td>I like eat delicious food. That's I'm cooking ...</td>
          <td>Positive</td>
          <td>1.00</td>
          <td>0.533333</td>
        </tr>
        <tr>
          <th>1</th>
          <td>10 Best Foods for You</td>
          <td>This help eating healthy exercise regular basis</td>
          <td>Positive</td>
          <td>0.25</td>
          <td>0.288462</td>
        </tr>
        <tr>
          <th>2</th>
          <td>10 Best Foods for You</td>
          <td>NaN</td>
          <td>NaN</td>
          <td>NaN</td>
          <td>NaN</td>
        </tr>
        <tr>
          <th>3</th>
          <td>10 Best Foods for You</td>
          <td>Works great especially going grocery store</td>
          <td>Positive</td>
          <td>0.40</td>
          <td>0.875000</td>
        </tr>
        <tr>
          <th>4</th>
          <td>10 Best Foods for You</td>
          <td>Best idea us</td>
          <td>Positive</td>
          <td>1.00</td>
          <td>0.300000</td>
        </tr>
      </tbody>
    </table>
    </div>



.. code:: ipython2

    googleStore.rename(columns={'App': 'app', 'Rating': 'rating', 'Reviews': 'reviews', 'Size': 'size', 'Price': 'price', 'Genres': 'genres'}, inplace=True)

.. code:: ipython2

    googleStore.head(5)




.. raw:: html

    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }
    
        .dataframe tbody tr th {
            vertical-align: top;
        }
    
        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>app</th>
          <th>Category</th>
          <th>rating</th>
          <th>reviews</th>
          <th>size</th>
          <th>Installs</th>
          <th>Type</th>
          <th>price</th>
          <th>cont_rating</th>
          <th>genres</th>
          <th>Last Updated</th>
          <th>Current Ver</th>
          <th>Android Ver</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>Photo Editor &amp; Candy Camera &amp; Grid &amp; ScrapBook</td>
          <td>ART_AND_DESIGN</td>
          <td>4.1</td>
          <td>159</td>
          <td>19M</td>
          <td>10,000+</td>
          <td>Free</td>
          <td>0</td>
          <td>Everyone</td>
          <td>Art &amp; Design</td>
          <td>7-Jan-18</td>
          <td>1.0.0</td>
          <td>4.0.3 and up</td>
        </tr>
        <tr>
          <th>1</th>
          <td>Coloring book moana</td>
          <td>ART_AND_DESIGN</td>
          <td>3.9</td>
          <td>967</td>
          <td>14M</td>
          <td>500,000+</td>
          <td>Free</td>
          <td>0</td>
          <td>Everyone</td>
          <td>Art &amp; Design;Pretend Play</td>
          <td>15-Jan-18</td>
          <td>2.0.0</td>
          <td>4.0.3 and up</td>
        </tr>
        <tr>
          <th>2</th>
          <td>U Launcher Lite äóñ FREE Live Cool Themes, Hid...</td>
          <td>ART_AND_DESIGN</td>
          <td>4.7</td>
          <td>87510</td>
          <td>8.7M</td>
          <td>5,000,000+</td>
          <td>Free</td>
          <td>0</td>
          <td>Everyone</td>
          <td>Art &amp; Design</td>
          <td>1-Aug-18</td>
          <td>1.2.4</td>
          <td>4.0.3 and up</td>
        </tr>
        <tr>
          <th>3</th>
          <td>Sketch - Draw &amp; Paint</td>
          <td>ART_AND_DESIGN</td>
          <td>4.5</td>
          <td>215644</td>
          <td>25M</td>
          <td>50,000,000+</td>
          <td>Free</td>
          <td>0</td>
          <td>Teen</td>
          <td>Art &amp; Design</td>
          <td>8-Jun-18</td>
          <td>Varies with device</td>
          <td>4.2 and up</td>
        </tr>
        <tr>
          <th>4</th>
          <td>Pixel Draw - Number Art Coloring Book</td>
          <td>ART_AND_DESIGN</td>
          <td>4.3</td>
          <td>967</td>
          <td>2.8M</td>
          <td>100,000+</td>
          <td>Free</td>
          <td>0</td>
          <td>Everyone</td>
          <td>Art &amp; Design;Creativity</td>
          <td>20-Jun-18</td>
          <td>1.1</td>
          <td>4.4 and up</td>
        </tr>
      </tbody>
    </table>
    </div>



.. code:: ipython2

    googleStore = googleStore.drop(columns=['Category', 'Installs', 'Type', 'Last Updated', 'Current Ver', 'Android Ver'])

**Remove '$' from price column**

.. code:: ipython2

    googleStore['price'] = googleStore['price'].replace({'\$': ''}, regex=True)

**Cleaning cont\_rating column**

.. code:: ipython2

    googleStore.cont_rating.unique()




.. parsed-literal::

    array(['Everyone', 'Teen', 'Everyone 10+', 'Mature 17+',
           'Adults only 18+', 'Unrated', nan], dtype=object)



.. code:: ipython2

    googleStore = googleStore.replace('Teen', 12)

.. code:: ipython2

    googleStore = googleStore.replace('Everyone', 0)

.. code:: ipython2

    googleStore = googleStore.replace('Everyone 10+', 0)

.. code:: ipython2

    googleStore = googleStore.replace('Mature 17+', 17)

.. code:: ipython2

    googleStore = googleStore.replace('Adults only 18+', 18)

.. code:: ipython2

    googleStore = googleStore.replace('Unrated', 0)

.. code:: ipython2

    googleStore = googleStore.replace(np.nan, 0)

.. code:: ipython2

    googleStore.cont_rating.unique()




.. parsed-literal::

    array([ 0., 12., 17., 18.])



.. code:: ipython2

    googleStore.head(5)




.. raw:: html

    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }
    
        .dataframe tbody tr th {
            vertical-align: top;
        }
    
        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>app</th>
          <th>rating</th>
          <th>reviews</th>
          <th>size</th>
          <th>price</th>
          <th>cont_rating</th>
          <th>genres</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>Photo Editor &amp; Candy Camera &amp; Grid &amp; ScrapBook</td>
          <td>4.1</td>
          <td>159</td>
          <td>19M</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art &amp; Design</td>
        </tr>
        <tr>
          <th>1</th>
          <td>Coloring book moana</td>
          <td>3.9</td>
          <td>967</td>
          <td>14M</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art &amp; Design;Pretend Play</td>
        </tr>
        <tr>
          <th>2</th>
          <td>U Launcher Lite äóñ FREE Live Cool Themes, Hid...</td>
          <td>4.7</td>
          <td>87510</td>
          <td>8.7M</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art &amp; Design</td>
        </tr>
        <tr>
          <th>3</th>
          <td>Sketch - Draw &amp; Paint</td>
          <td>4.5</td>
          <td>215644</td>
          <td>25M</td>
          <td>0</td>
          <td>12.0</td>
          <td>Art &amp; Design</td>
        </tr>
        <tr>
          <th>4</th>
          <td>Pixel Draw - Number Art Coloring Book</td>
          <td>4.3</td>
          <td>967</td>
          <td>2.8M</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art &amp; Design;Creativity</td>
        </tr>
      </tbody>
    </table>
    </div>



.. code:: ipython2

    googleStore['size'] = googleStore['size'].replace({'M': ''}, regex=True)

.. code:: ipython2

    googleStore.head(5)




.. raw:: html

    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }
    
        .dataframe tbody tr th {
            vertical-align: top;
        }
    
        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>app</th>
          <th>rating</th>
          <th>reviews</th>
          <th>size</th>
          <th>price</th>
          <th>cont_rating</th>
          <th>genres</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>Photo Editor &amp; Candy Camera &amp; Grid &amp; ScrapBook</td>
          <td>4.1</td>
          <td>159</td>
          <td>19</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art &amp; Design</td>
        </tr>
        <tr>
          <th>1</th>
          <td>Coloring book moana</td>
          <td>3.9</td>
          <td>967</td>
          <td>14</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art &amp; Design;Pretend Play</td>
        </tr>
        <tr>
          <th>2</th>
          <td>U Launcher Lite äóñ FREE Live Cool Themes, Hid...</td>
          <td>4.7</td>
          <td>87510</td>
          <td>8.7</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art &amp; Design</td>
        </tr>
        <tr>
          <th>3</th>
          <td>Sketch - Draw &amp; Paint</td>
          <td>4.5</td>
          <td>215644</td>
          <td>25</td>
          <td>0</td>
          <td>12.0</td>
          <td>Art &amp; Design</td>
        </tr>
        <tr>
          <th>4</th>
          <td>Pixel Draw - Number Art Coloring Book</td>
          <td>4.3</td>
          <td>967</td>
          <td>2.8</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art &amp; Design;Creativity</td>
        </tr>
      </tbody>
    </table>
    </div>



.. code:: ipython2

    googleStore.genres.unique()




.. parsed-literal::

    array(['Art & Design', 'Art & Design;Pretend Play',
           'Art & Design;Creativity', 'Art & Design;Action & Adventure',
           'Auto & Vehicles', 'Beauty', 'Books & Reference', 'Business',
           'Comics', 'Comics;Creativity', 'Communication', 'Dating',
           'Education;Education', 'Education', 'Education;Creativity',
           'Education;Music & Video', 'Education;Action & Adventure',
           'Education;Pretend Play', 'Education;Brain Games', 'Entertainment',
           'Entertainment;Music & Video', 'Entertainment;Brain Games',
           'Entertainment;Creativity', 'Events', 'Finance', 'Food & Drink',
           'Health & Fitness', 'House & Home', 'Libraries & Demo',
           'Lifestyle', 'Lifestyle;Pretend Play',
           'Adventure;Action & Adventure', 'Arcade', 'Casual', 'Card',
           'Casual;Pretend Play', 'Action', 'Strategy', 'Puzzle', 'Sports',
           'Music', 'Word', 'Racing', 'Casual;Creativity',
           'Casual;Action & Adventure', 'Simulation', 'Adventure', 'Board',
           'Trivia', 'Role Playing', 'Simulation;Education',
           'Action;Action & Adventure', 'Casual;Brain Games',
           'Simulation;Action & Adventure', 'Educational;Creativity',
           'Puzzle;Brain Games', 'Educational;Education', 'Card;Brain Games',
           'Educational;Brain Games', 'Educational;Pretend Play',
           'Entertainment;Education', 'Casual;Education',
           'Music;Music & Video', 'Racing;Action & Adventure',
           'Arcade;Pretend Play', 'Role Playing;Action & Adventure',
           'Simulation;Pretend Play', 'Puzzle;Creativity',
           'Sports;Action & Adventure', 'Educational;Action & Adventure',
           'Arcade;Action & Adventure', 'Entertainment;Action & Adventure',
           'Puzzle;Action & Adventure', 'Strategy;Action & Adventure',
           'Music & Audio;Music & Video', 'Health & Fitness;Education',
           'Adventure;Education', 'Board;Brain Games',
           'Board;Action & Adventure', 'Board;Pretend Play',
           'Casual;Music & Video', 'Role Playing;Pretend Play',
           'Entertainment;Pretend Play', 'Video Players & Editors;Creativity',
           'Card;Action & Adventure', 'Medical', 'Social', 'Shopping',
           'Photography', 'Travel & Local',
           'Travel & Local;Action & Adventure', 'Tools', 'Tools;Education',
           'Personalization', 'Productivity', 'Parenting',
           'Parenting;Music & Video', 'Parenting;Education',
           'Parenting;Brain Games', 'Weather', 'Video Players & Editors',
           'Video Players & Editors;Music & Video', 'News & Magazines',
           'Maps & Navigation', 'Health & Fitness;Action & Adventure',
           'Educational', 'Casino', 'Adventure;Brain Games',
           'Trivia;Education', 'Lifestyle;Education',
           'Books & Reference;Creativity', 'Books & Reference;Education',
           'Puzzle;Education', 'Role Playing;Education',
           'Role Playing;Brain Games', 'Strategy;Education',
           'Racing;Pretend Play', 'Communication;Creativity', '11-Feb-18',
           'Strategy;Creativity'], dtype=object)



.. code:: ipython2

    googleStore['genres'] = googleStore['genres'].replace({' &': ','}, regex=True)
    googleStore['genres'] = googleStore['genres'].replace({';': ' ,'}, regex=True)


.. code:: ipython2

    googleStore['genres'] = googleStore['genres'].replace({' ,': ', '}, regex=True)

.. code:: ipython2

    googleStore['genres']




.. parsed-literal::

    0                           Art, Design
    1             Art, Design, Pretend Play
    2                           Art, Design
    3                           Art, Design
    4               Art, Design, Creativity
    5                           Art, Design
    6                           Art, Design
    7                           Art, Design
    8                           Art, Design
    9               Art, Design, Creativity
    10                          Art, Design
    11                          Art, Design
    12                          Art, Design
    13                          Art, Design
    14                          Art, Design
    15                          Art, Design
    16                          Art, Design
    17                          Art, Design
    18                          Art, Design
    19                          Art, Design
    20                          Art, Design
    21                          Art, Design
    22                          Art, Design
    23       Art, Design, Action, Adventure
    24                          Art, Design
    25                          Art, Design
    26              Art, Design, Creativity
    27                          Art, Design
    28                          Art, Design
    29                          Art, Design
                          ...              
    10811                    Auto, Vehicles
    10812                         Education
    10813                          Business
    10814                     Entertainment
    10815                  Books, Reference
    10816                          Business
    10817                             Tools
    10818                           Finance
    10819                  Books, Reference
    10820                         Education
    10821                     Entertainment
    10822                      Productivity
    10823            Video Players, Editors
    10824                           Medical
    10825                            Social
    10826                            Social
    10827                         Education
    10828                            Comics
    10829                  Books, Reference
    10830                   News, Magazines
    10831                  Maps, Navigation
    10832                           Weather
    10833                  Books, Reference
    10834                         Education
    10835                          Business
    10836                         Education
    10837                         Education
    10838                           Medical
    10839                  Books, Reference
    10840                         Lifestyle
    Name: genres, Length: 10841, dtype: object



.. code:: ipython2

    googleStore.genres.unique()




.. parsed-literal::

    array(['Art, Design', 'Art, Design, Pretend Play',
           'Art, Design, Creativity', 'Art, Design, Action, Adventure',
           'Auto, Vehicles', 'Beauty', 'Books, Reference', 'Business',
           'Comics', 'Comics, Creativity', 'Communication', 'Dating',
           'Education, Education', 'Education', 'Education, Creativity',
           'Education, Music, Video', 'Education, Action, Adventure',
           'Education, Pretend Play', 'Education, Brain Games',
           'Entertainment', 'Entertainment, Music, Video',
           'Entertainment, Brain Games', 'Entertainment, Creativity',
           'Events', 'Finance', 'Food, Drink', 'Health, Fitness',
           'House, Home', 'Libraries, Demo', 'Lifestyle',
           'Lifestyle, Pretend Play', 'Adventure, Action, Adventure',
           'Arcade', 'Casual', 'Card', 'Casual, Pretend Play', 'Action',
           'Strategy', 'Puzzle', 'Sports', 'Music', 'Word', 'Racing',
           'Casual, Creativity', 'Casual, Action, Adventure', 'Simulation',
           'Adventure', 'Board', 'Trivia', 'Role Playing',
           'Simulation, Education', 'Action, Action, Adventure',
           'Casual, Brain Games', 'Simulation, Action, Adventure',
           'Educational, Creativity', 'Puzzle, Brain Games',
           'Educational, Education', 'Card, Brain Games',
           'Educational, Brain Games', 'Educational, Pretend Play',
           'Entertainment, Education', 'Casual, Education',
           'Music, Music, Video', 'Racing, Action, Adventure',
           'Arcade, Pretend Play', 'Role Playing, Action, Adventure',
           'Simulation, Pretend Play', 'Puzzle, Creativity',
           'Sports, Action, Adventure', 'Educational, Action, Adventure',
           'Arcade, Action, Adventure', 'Entertainment, Action, Adventure',
           'Puzzle, Action, Adventure', 'Strategy, Action, Adventure',
           'Music, Audio, Music, Video', 'Health, Fitness, Education',
           'Adventure, Education', 'Board, Brain Games',
           'Board, Action, Adventure', 'Board, Pretend Play',
           'Casual, Music, Video', 'Role Playing, Pretend Play',
           'Entertainment, Pretend Play',
           'Video Players, Editors, Creativity', 'Card, Action, Adventure',
           'Medical', 'Social', 'Shopping', 'Photography', 'Travel, Local',
           'Travel, Local, Action, Adventure', 'Tools', 'Tools, Education',
           'Personalization', 'Productivity', 'Parenting',
           'Parenting, Music, Video', 'Parenting, Education',
           'Parenting, Brain Games', 'Weather', 'Video Players, Editors',
           'Video Players, Editors, Music, Video', 'News, Magazines',
           'Maps, Navigation', 'Health, Fitness, Action, Adventure',
           'Educational', 'Casino', 'Adventure, Brain Games',
           'Trivia, Education', 'Lifestyle, Education',
           'Books, Reference, Creativity', 'Books, Reference, Education',
           'Puzzle, Education', 'Role Playing, Education',
           'Role Playing, Brain Games', 'Strategy, Education',
           'Racing, Pretend Play', 'Communication, Creativity', '11-Feb-18',
           'Strategy, Creativity'], dtype=object)



.. code:: ipython2

    googleStore['genres'] = googleStore['genres'].replace('11-Feb-18', '')

.. code:: ipython2

    googleStore.genres.unique()




.. parsed-literal::

    array(['Art, Design', 'Art, Design, Pretend Play',
           'Art, Design, Creativity', 'Art, Design, Action, Adventure',
           'Auto, Vehicles', 'Beauty', 'Books, Reference', 'Business',
           'Comics', 'Comics, Creativity', 'Communication', 'Dating',
           'Education, Education', 'Education', 'Education, Creativity',
           'Education, Music, Video', 'Education, Action, Adventure',
           'Education, Pretend Play', 'Education, Brain Games',
           'Entertainment', 'Entertainment, Music, Video',
           'Entertainment, Brain Games', 'Entertainment, Creativity',
           'Events', 'Finance', 'Food, Drink', 'Health, Fitness',
           'House, Home', 'Libraries, Demo', 'Lifestyle',
           'Lifestyle, Pretend Play', 'Adventure, Action, Adventure',
           'Arcade', 'Casual', 'Card', 'Casual, Pretend Play', 'Action',
           'Strategy', 'Puzzle', 'Sports', 'Music', 'Word', 'Racing',
           'Casual, Creativity', 'Casual, Action, Adventure', 'Simulation',
           'Adventure', 'Board', 'Trivia', 'Role Playing',
           'Simulation, Education', 'Action, Action, Adventure',
           'Casual, Brain Games', 'Simulation, Action, Adventure',
           'Educational, Creativity', 'Puzzle, Brain Games',
           'Educational, Education', 'Card, Brain Games',
           'Educational, Brain Games', 'Educational, Pretend Play',
           'Entertainment, Education', 'Casual, Education',
           'Music, Music, Video', 'Racing, Action, Adventure',
           'Arcade, Pretend Play', 'Role Playing, Action, Adventure',
           'Simulation, Pretend Play', 'Puzzle, Creativity',
           'Sports, Action, Adventure', 'Educational, Action, Adventure',
           'Arcade, Action, Adventure', 'Entertainment, Action, Adventure',
           'Puzzle, Action, Adventure', 'Strategy, Action, Adventure',
           'Music, Audio, Music, Video', 'Health, Fitness, Education',
           'Adventure, Education', 'Board, Brain Games',
           'Board, Action, Adventure', 'Board, Pretend Play',
           'Casual, Music, Video', 'Role Playing, Pretend Play',
           'Entertainment, Pretend Play',
           'Video Players, Editors, Creativity', 'Card, Action, Adventure',
           'Medical', 'Social', 'Shopping', 'Photography', 'Travel, Local',
           'Travel, Local, Action, Adventure', 'Tools', 'Tools, Education',
           'Personalization', 'Productivity', 'Parenting',
           'Parenting, Music, Video', 'Parenting, Education',
           'Parenting, Brain Games', 'Weather', 'Video Players, Editors',
           'Video Players, Editors, Music, Video', 'News, Magazines',
           'Maps, Navigation', 'Health, Fitness, Action, Adventure',
           'Educational', 'Casino', 'Adventure, Brain Games',
           'Trivia, Education', 'Lifestyle, Education',
           'Books, Reference, Creativity', 'Books, Reference, Education',
           'Puzzle, Education', 'Role Playing, Education',
           'Role Playing, Brain Games', 'Strategy, Education',
           'Racing, Pretend Play', 'Communication, Creativity', '',
           'Strategy, Creativity'], dtype=object)



.. code:: ipython2

    googleStore['genres'] = googleStore['genres'].apply(lambda x: x.split(',')[0])

.. code:: ipython2

    googleStore['size'] = pd.to_numeric(googleStore['size'], errors='coerce')
    googleStore['size'] *= 1000000

.. code:: ipython2

    googleStore['size'].fillna(0, inplace=True)

.. code:: ipython2

    googleStore.to_csv('googleData.csv', encoding='utf-8', index=False)

.. code:: ipython2

    googleStore




.. raw:: html

    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }
    
        .dataframe tbody tr th {
            vertical-align: top;
        }
    
        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>app</th>
          <th>rating</th>
          <th>reviews</th>
          <th>size</th>
          <th>price</th>
          <th>cont_rating</th>
          <th>genres</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>Photo Editor &amp; Candy Camera &amp; Grid &amp; ScrapBook</td>
          <td>4.1</td>
          <td>159</td>
          <td>19000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>1</th>
          <td>Coloring book moana</td>
          <td>3.9</td>
          <td>967</td>
          <td>14000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>2</th>
          <td>U Launcher Lite äóñ FREE Live Cool Themes, Hid...</td>
          <td>4.7</td>
          <td>87510</td>
          <td>8700000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>3</th>
          <td>Sketch - Draw &amp; Paint</td>
          <td>4.5</td>
          <td>215644</td>
          <td>25000000.0</td>
          <td>0</td>
          <td>12.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>4</th>
          <td>Pixel Draw - Number Art Coloring Book</td>
          <td>4.3</td>
          <td>967</td>
          <td>2800000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>5</th>
          <td>Paper flowers instructions</td>
          <td>4.4</td>
          <td>167</td>
          <td>5600000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>6</th>
          <td>Smoke Effect Photo Maker - Smoke Editor</td>
          <td>3.8</td>
          <td>178</td>
          <td>19000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>7</th>
          <td>Infinite Painter</td>
          <td>4.1</td>
          <td>36815</td>
          <td>29000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>8</th>
          <td>Garden Coloring Book</td>
          <td>4.4</td>
          <td>13791</td>
          <td>33000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>9</th>
          <td>Kids Paint Free - Drawing Fun</td>
          <td>4.7</td>
          <td>121</td>
          <td>3100000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>10</th>
          <td>Text on Photo - Fonteee</td>
          <td>4.4</td>
          <td>13880</td>
          <td>28000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>11</th>
          <td>Name Art Photo Editor - Focus n Filters</td>
          <td>4.4</td>
          <td>8788</td>
          <td>12000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>12</th>
          <td>Tattoo Name On My Photo Editor</td>
          <td>4.2</td>
          <td>44829</td>
          <td>20000000.0</td>
          <td>0</td>
          <td>12.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>13</th>
          <td>Mandala Coloring Book</td>
          <td>4.6</td>
          <td>4326</td>
          <td>21000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>14</th>
          <td>3D Color Pixel by Number - Sandbox Art Coloring</td>
          <td>4.4</td>
          <td>1518</td>
          <td>37000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>15</th>
          <td>Learn To Draw Kawaii Characters</td>
          <td>3.2</td>
          <td>55</td>
          <td>2700000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>16</th>
          <td>Photo Designer - Write your name with shapes</td>
          <td>4.7</td>
          <td>3632</td>
          <td>5500000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>17</th>
          <td>350 Diy Room Decor Ideas</td>
          <td>4.5</td>
          <td>27</td>
          <td>17000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>18</th>
          <td>FlipaClip - Cartoon animation</td>
          <td>4.3</td>
          <td>194216</td>
          <td>39000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>19</th>
          <td>ibis Paint X</td>
          <td>4.6</td>
          <td>224399</td>
          <td>31000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>20</th>
          <td>Logo Maker - Small Business</td>
          <td>4.0</td>
          <td>450</td>
          <td>14000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>21</th>
          <td>Boys Photo Editor - Six Pack &amp; Men's Suit</td>
          <td>4.1</td>
          <td>654</td>
          <td>12000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>22</th>
          <td>Superheroes Wallpapers | 4K Backgrounds</td>
          <td>4.7</td>
          <td>7699</td>
          <td>4200000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>23</th>
          <td>Mcqueen Coloring pages</td>
          <td>0.0</td>
          <td>61</td>
          <td>7000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>24</th>
          <td>HD Mickey Minnie Wallpapers</td>
          <td>4.7</td>
          <td>118</td>
          <td>23000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>25</th>
          <td>Harley Quinn wallpapers HD</td>
          <td>4.8</td>
          <td>192</td>
          <td>6000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>26</th>
          <td>Colorfit - Drawing &amp; Coloring</td>
          <td>4.7</td>
          <td>20260</td>
          <td>25000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>27</th>
          <td>Animated Photo Editor</td>
          <td>4.1</td>
          <td>203</td>
          <td>6100000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>28</th>
          <td>Pencil Sketch Drawing</td>
          <td>3.9</td>
          <td>136</td>
          <td>4600000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>29</th>
          <td>Easy Realistic Drawing Tutorial</td>
          <td>4.1</td>
          <td>223</td>
          <td>4200000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Art</td>
        </tr>
        <tr>
          <th>...</th>
          <td>...</td>
          <td>...</td>
          <td>...</td>
          <td>...</td>
          <td>...</td>
          <td>...</td>
          <td>...</td>
        </tr>
        <tr>
          <th>10811</th>
          <td>FR Plus 1.6</td>
          <td>0.0</td>
          <td>4</td>
          <td>3900000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Auto</td>
        </tr>
        <tr>
          <th>10812</th>
          <td>Fr Agnel Pune</td>
          <td>4.1</td>
          <td>80</td>
          <td>13000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Education</td>
        </tr>
        <tr>
          <th>10813</th>
          <td>DICT.fr Mobile</td>
          <td>0.0</td>
          <td>20</td>
          <td>2700000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Business</td>
        </tr>
        <tr>
          <th>10814</th>
          <td>FR: My Secret Pets!</td>
          <td>4.0</td>
          <td>785</td>
          <td>31000000.0</td>
          <td>0</td>
          <td>12.0</td>
          <td>Entertainment</td>
        </tr>
        <tr>
          <th>10815</th>
          <td>Golden Dictionary (FR-AR)</td>
          <td>4.2</td>
          <td>5775</td>
          <td>4900000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Books</td>
        </tr>
        <tr>
          <th>10816</th>
          <td>FieldBi FR Offline</td>
          <td>0.0</td>
          <td>2</td>
          <td>6800000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Business</td>
        </tr>
        <tr>
          <th>10817</th>
          <td>HTC Sense Input - FR</td>
          <td>4.0</td>
          <td>885</td>
          <td>8000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Tools</td>
        </tr>
        <tr>
          <th>10818</th>
          <td>Gold Quote - Gold.fr</td>
          <td>0.0</td>
          <td>96</td>
          <td>1500000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Finance</td>
        </tr>
        <tr>
          <th>10819</th>
          <td>Fanfic-FR</td>
          <td>3.3</td>
          <td>52</td>
          <td>3600000.0</td>
          <td>0</td>
          <td>12.0</td>
          <td>Books</td>
        </tr>
        <tr>
          <th>10820</th>
          <td>Fr. Daoud Lamei</td>
          <td>5.0</td>
          <td>22</td>
          <td>8600000.0</td>
          <td>0</td>
          <td>12.0</td>
          <td>Education</td>
        </tr>
        <tr>
          <th>10821</th>
          <td>Poop FR</td>
          <td>0.0</td>
          <td>6</td>
          <td>2500000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Entertainment</td>
        </tr>
        <tr>
          <th>10822</th>
          <td>PLMGSS FR</td>
          <td>0.0</td>
          <td>0</td>
          <td>3100000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Productivity</td>
        </tr>
        <tr>
          <th>10823</th>
          <td>List iptv FR</td>
          <td>0.0</td>
          <td>1</td>
          <td>2900000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Video Players</td>
        </tr>
        <tr>
          <th>10824</th>
          <td>Cardio-FR</td>
          <td>0.0</td>
          <td>67</td>
          <td>82000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Medical</td>
        </tr>
        <tr>
          <th>10825</th>
          <td>Naruto &amp; Boruto FR</td>
          <td>0.0</td>
          <td>7</td>
          <td>7700000.0</td>
          <td>0</td>
          <td>12.0</td>
          <td>Social</td>
        </tr>
        <tr>
          <th>10826</th>
          <td>Frim: get new friends on local chat rooms</td>
          <td>4.0</td>
          <td>88486</td>
          <td>0.0</td>
          <td>0</td>
          <td>17.0</td>
          <td>Social</td>
        </tr>
        <tr>
          <th>10827</th>
          <td>Fr Agnel Ambarnath</td>
          <td>4.2</td>
          <td>117</td>
          <td>13000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Education</td>
        </tr>
        <tr>
          <th>10828</th>
          <td>Manga-FR - Anime Vostfr</td>
          <td>3.4</td>
          <td>291</td>
          <td>13000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Comics</td>
        </tr>
        <tr>
          <th>10829</th>
          <td>Bulgarian French Dictionary Fr</td>
          <td>4.6</td>
          <td>603</td>
          <td>7400000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Books</td>
        </tr>
        <tr>
          <th>10830</th>
          <td>News Minecraft.fr</td>
          <td>3.8</td>
          <td>881</td>
          <td>2300000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>News</td>
        </tr>
        <tr>
          <th>10831</th>
          <td>payermonstationnement.fr</td>
          <td>0.0</td>
          <td>38</td>
          <td>9800000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Maps</td>
        </tr>
        <tr>
          <th>10832</th>
          <td>FR Tides</td>
          <td>3.8</td>
          <td>1195</td>
          <td>0.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Weather</td>
        </tr>
        <tr>
          <th>10833</th>
          <td>Chemin (fr)</td>
          <td>4.8</td>
          <td>44</td>
          <td>0.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Books</td>
        </tr>
        <tr>
          <th>10834</th>
          <td>FR Calculator</td>
          <td>4.0</td>
          <td>7</td>
          <td>2600000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Education</td>
        </tr>
        <tr>
          <th>10835</th>
          <td>FR Forms</td>
          <td>0.0</td>
          <td>0</td>
          <td>9600000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Business</td>
        </tr>
        <tr>
          <th>10836</th>
          <td>Sya9a Maroc - FR</td>
          <td>4.5</td>
          <td>38</td>
          <td>53000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Education</td>
        </tr>
        <tr>
          <th>10837</th>
          <td>Fr. Mike Schmitz Audio Teachings</td>
          <td>5.0</td>
          <td>4</td>
          <td>3600000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Education</td>
        </tr>
        <tr>
          <th>10838</th>
          <td>Parkinson Exercices FR</td>
          <td>0.0</td>
          <td>3</td>
          <td>9500000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Medical</td>
        </tr>
        <tr>
          <th>10839</th>
          <td>The SCP Foundation DB fr nn5n</td>
          <td>4.5</td>
          <td>114</td>
          <td>0.0</td>
          <td>0</td>
          <td>17.0</td>
          <td>Books</td>
        </tr>
        <tr>
          <th>10840</th>
          <td>iHoroscope - 2018 Daily Horoscope &amp; Astrology</td>
          <td>4.5</td>
          <td>398307</td>
          <td>19000000.0</td>
          <td>0</td>
          <td>0.0</td>
          <td>Lifestyle</td>
        </tr>
      </tbody>
    </table>
    <p>10841 rows × 7 columns</p>
    </div>



.. code:: ipython2

    # Convert data into numeric
    googleStore['price'] = pd.to_numeric(googleStore['price'], errors='coerce')

Bar Chart for Count of each amount of Price
===========================================

.. code:: ipython2

    criteria1 = googleStore.price > 0
    paidapps = googleStore[criteria1]
    paidapps.index




.. parsed-literal::

    Int64Index([  234,   235,   290,   291,   427,   476,   477,   478,   479,
                  480,
                ...
                10675, 10679, 10682, 10690, 10697, 10735, 10760, 10782, 10785,
                10798],
               dtype='int64', length=800)



.. code:: ipython2

    paidappcount = googleStore["price"].value_counts()
    paidappcount.head()




.. parsed-literal::

    0.00    10041
    0.99      148
    2.99      129
    1.99       73
    4.99       72
    Name: price, dtype: int64



.. code:: ipython2

    multiapp = paidappcount[paidappcount.values > 10]
    multiapp.index




.. parsed-literal::

    Float64Index([0.0, 0.99, 2.99, 1.99, 4.99, 3.99, 1.49, 5.99, 2.49, 9.99, 6.99,
                  399.99, 14.99],
                 dtype='float64')



Create function to add data to plot
===================================

.. code:: ipython2

    
    def plot(ax,w,h):
        ax.spines['top'].set_visible(False)
        ax.spines['right'].set_visible(False)
        for p in ax.patches:
            ax.annotate('{}'.format(p.get_height()), (p.get_x()+w, p.get_height()+h))

Compare apps with more review - popular or well-received apps vs less popular apps
==================================================================================

.. code:: ipython2

    googleStore['reviews'] = googleStore['reviews'].replace('3.0M', '3000000')

.. code:: ipython2

    googleStore['reviews'] = pd.to_numeric(googleStore['reviews'])

.. code:: ipython2

    googleStore['reviews'].describe()




.. parsed-literal::

    count    1.084100e+04
    mean     4.443887e+05
    std      2.927728e+06
    min      0.000000e+00
    25%      3.800000e+01
    50%      2.094000e+03
    75%      5.479800e+04
    max      7.815831e+07
    Name: reviews, dtype: float64



.. code:: ipython2

    popular_apps = googleStore[googleStore['reviews'] > 250000]
    less_popular_apps = googleStore[googleStore['size'] < 250000]
    labels=['Popular Apps','Less Poplular Apps']
    sizes = [popular_apps.shape[0],less_popular_apps.shape[0]]
    colors = ['blue','orange']
    
    # Plot
    plt.pie(sizes, labels=labels, colors=colors,
            autopct='%1.1f%%', shadow=True,startangle=90)
    
    plt.title('Pie Chart of App Size')
    plt.axis('equal')
    plt.show()



.. image:: output_44_0.png


Compare size of Apps
====================

.. code:: ipython2

    avg = googleStore['size'].mean()

.. code:: ipython2

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



.. image:: output_47_0.png


Compare free vs paid Apps
=========================

.. code:: ipython2

    googleStore['price'] = pd.to_numeric(googleStore['price'], errors='coerce')

.. code:: ipython2

    free_apps = googleStore[googleStore['price']==0]
    paid_apps = googleStore[googleStore['price']>0]
    
    labels=['Free Apps','Paid Apps']
    sizes = [free_apps.shape[0],paid_apps.shape[0]]
    colors = ['blue','orange']
    
    # Plot
    plt.pie(sizes, labels=labels, colors=colors,
            autopct='%1.1f%%', shadow=True,startangle=90)
    
    plt.title('Pie Chart of App Price')
    plt.axis('equal')
    plt.show()



.. image:: output_50_0.png


Compare user rating between free and paid apps
==============================================

.. code:: ipython2

    plt.figure(figsize=(18,9))
    plt.subplot(1,2,1)
    ax1=sns.countplot('rating',data=free_apps,palette="Set1")
    plt.title('Free Apps Rating')
    plt.xlabel('User Rating')
    plt.ylabel('Free Apps')
    plt.xticks(rotation=80)
    plot(ax1,0.05,1)
    
    plt.subplot(1,2,2)
    ax2=sns.countplot('rating',data=paid_apps,palette="Set1")
    plt.title('Paid Apps Rating')
    plt.xlabel('User Rating')
    plt.ylabel('Paid Apps')
    plt.xticks(rotation=80)
    plot(ax2,0.05,1)



.. image:: output_52_0.png


App Distribution by Genres
==========================

.. code:: ipython2

    plt.figure(figsize=(10,12))
    ax=sns.countplot('genres',data=googleStore,palette="Set1",order=googleStore['genres'].value_counts().index)
    plt.xlabel('GENRES')
    plt.ylabel('APPS')
    plt.xticks(rotation=80)
    plot(ax,1,2)



.. image:: output_54_0.png


Top 20 most expensive apps on Google Store by Genre
===================================================

.. code:: ipython2

    genre_expens_app = googleStore.groupby(['genres'])['price'].max().reset_index()
    expens_app = genre_expens_app.merge(googleStore,on=['genres','price'],how='left')
    expens_app[['genres','app','price']].sort_values('price',ascending=False).head(20)




.. raw:: html

    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }
    
        .dataframe tbody tr th {
            vertical-align: top;
        }
    
        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>genres</th>
          <th>app</th>
          <th>price</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>236</th>
          <td>Lifestyle</td>
          <td>I'm Rich - Trump Edition</td>
          <td>400.00</td>
        </tr>
        <tr>
          <th>135</th>
          <td>Entertainment</td>
          <td>most expensive app (H)</td>
          <td>399.99</td>
        </tr>
        <tr>
          <th>144</th>
          <td>Finance</td>
          <td>I AM RICH PRO PLUS</td>
          <td>399.99</td>
        </tr>
        <tr>
          <th>136</th>
          <td>Entertainment</td>
          <td>I am Rich Plus</td>
          <td>399.99</td>
        </tr>
        <tr>
          <th>137</th>
          <td>Entertainment</td>
          <td>I Am Rich Pro</td>
          <td>399.99</td>
        </tr>
        <tr>
          <th>139</th>
          <td>Finance</td>
          <td>I Am Rich Premium</td>
          <td>399.99</td>
        </tr>
        <tr>
          <th>140</th>
          <td>Finance</td>
          <td>I am Rich!</td>
          <td>399.99</td>
        </tr>
        <tr>
          <th>141</th>
          <td>Finance</td>
          <td>I am rich(premium)</td>
          <td>399.99</td>
        </tr>
        <tr>
          <th>142</th>
          <td>Finance</td>
          <td>I am rich (Most expensive app)</td>
          <td>399.99</td>
        </tr>
        <tr>
          <th>143</th>
          <td>Finance</td>
          <td>I am Rich</td>
          <td>399.99</td>
        </tr>
        <tr>
          <th>238</th>
          <td>Medical</td>
          <td>EP Cook Book</td>
          <td>200.00</td>
        </tr>
        <tr>
          <th>245</th>
          <td>Productivity</td>
          <td>cronometra-br</td>
          <td>154.99</td>
        </tr>
        <tr>
          <th>138</th>
          <td>Events</td>
          <td>BP Fitness Lead Scanner</td>
          <td>109.99</td>
        </tr>
        <tr>
          <th>67</th>
          <td>Business</td>
          <td>Lean EQ</td>
          <td>89.99</td>
        </tr>
        <tr>
          <th>133</th>
          <td>Education</td>
          <td>Norwegian For Kids &amp; Babies F</td>
          <td>39.99</td>
        </tr>
        <tr>
          <th>244</th>
          <td>Photography</td>
          <td>Guide to Nikon Df</td>
          <td>29.99</td>
        </tr>
        <tr>
          <th>253</th>
          <td>Sports</td>
          <td>Golfshot Plus: Golf GPS</td>
          <td>29.99</td>
        </tr>
        <tr>
          <th>255</th>
          <td>Tools</td>
          <td>G-NetReport Pro</td>
          <td>25.99</td>
        </tr>
        <tr>
          <th>248</th>
          <td>Role Playing</td>
          <td>DRAGON QUEST VIII</td>
          <td>19.99</td>
        </tr>
        <tr>
          <th>131</th>
          <td>Communication</td>
          <td>Z PIVOT</td>
          <td>19.99</td>
        </tr>
      </tbody>
    </table>
    </div>



Content Rating
==============

.. code:: ipython2

    plt.figure(figsize=(8,8))
    ax=sns.countplot('cont_rating',data=googleStore,palette="Set1",order=googleStore['cont_rating'].value_counts().index)
    plt.xlabel('Content Rating')
    plt.ylabel('Apps')
    plot(ax,0.2,1)



.. image:: output_58_0.png


Content rating by Genre
=======================

.. code:: ipython2

    for i in googleStore['cont_rating'].unique():
        plt.figure(figsize=(12,6))
        ax=sns.countplot('genres',data=googleStore[googleStore['cont_rating']==i],palette="Set1",order=googleStore['genres'].value_counts().index)
        plt.xlabel('Genres')
        plt.ylabel('Apps')
        plt.title(str(int(i)) + '+' + ' Apps')
        plt.xticks(rotation=80)



.. image:: output_60_0.png



.. image:: output_60_1.png



.. image:: output_60_2.png



.. image:: output_60_3.png


.. code:: ipython2

    googleStore = pd.read_csv('googleData.csv')

.. code:: ipython2

    storeprod = googleStore[["genres","price"]]
    TotalPriceByGenre = storeprod.groupby(["genres"]).sum().sort_values("price", ascending=False).head(10)
    TotalPriceByGenre.plot(kind="barh", width=0.8, figsize=(10,10))




.. parsed-literal::

    <matplotlib.axes._subplots.AxesSubplot at 0x112f0e550>




.. image:: output_62_1.png


.. code:: ipython2

    TotalPriceByGenre




.. raw:: html

    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }
    
        .dataframe tbody tr th {
            vertical-align: top;
        }
    
        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>price</th>
        </tr>
        <tr>
          <th>genres</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>Finance</th>
          <td>2900.83</td>
        </tr>
        <tr>
          <th>Lifestyle</th>
          <td>2360.87</td>
        </tr>
        <tr>
          <th>Entertainment</th>
          <td>1665.08</td>
        </tr>
        <tr>
          <th>Medical</th>
          <td>1439.96</td>
        </tr>
        <tr>
          <th>Education</th>
          <td>288.22</td>
        </tr>
        <tr>
          <th>Tools</th>
          <td>267.25</td>
        </tr>
        <tr>
          <th>Productivity</th>
          <td>250.93</td>
        </tr>
        <tr>
          <th>Role Playing</th>
          <td>187.04</td>
        </tr>
        <tr>
          <th>Business</th>
          <td>185.27</td>
        </tr>
        <tr>
          <th>Personalization</th>
          <td>153.96</td>
        </tr>
      </tbody>
    </table>
    </div>


