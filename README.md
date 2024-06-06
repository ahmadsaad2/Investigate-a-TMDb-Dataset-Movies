 # Investigate-a-TMDb-Dataset-Movies

The primary goal of the project is to go through the dataset and the general data analysis process using numpy, pandas and matplotlib.
This data set contains information about 10,000 movies collected from The Movie Database (TMDb), including user ratings and revenue.

## Project Overview
In this project, you will analyze a dataset and then communicate your findings about it. You will use the Python libraries NumPy, pandas, and Matplotlib to make your analysis easier.

## What do you need to install?
You will need an installation of Python, plus the following libraries:

* pandas
* NumPy
* Matplotlib
* csv

## Why this Project?
In this project, you'll go through the data analysis process and see how everything fits together. Later Nanodegree projects will focus on individual pieces of the data analysis process.

You'll use the Python libraries NumPy, pandas, and Matplotlib, which make writing data analysis code in Python a lot easier! Not only that, these are sought-after skills by employers!

## What will you learn?
After completing the project, you will:

- Know all the steps involved in a typical data analysis process
- Be comfortable posing questions that can be answered with a given dataset and then answering those questions
- Know how to investigate problems in a dataset and wrangle the data into a format you can use
- Have practice communicating the results of your analysis
- Be able to use vectorized operations in NumPy and pandas to speed up your data analysis code
- Be familiar with pandas' Series and DataFrame objects, which let you access your data more conveniently
- Know how to use Matplotlib to produce plots showing your findings

## Exploratory Data Analysis
Tip: Now that you've trimmed and cleaned your data, you're ready to move on to exploration. Compute statistics and create visualizations with the goal of addressing the research questions that you posed in the Introduction section. It is recommended that you be systematic with your approach. Look at one variable at a time, and then follow it up by looking at relationships between variables.

## Research Questions
1.Which year Has the highest Profit Rate ?

2.Which Movie got the highest Ratings ?

3.What are the movies with the highest and the lowest revenues ?

4.Do movies with higher budgets receive higher ratings?

5.Movie with highest and lowest budget?

## Conclusions

-.Highest Profit Year: The analysis revealed that the year 2015 had the highest profit rate in the dataset.
-.Highest Rated Movie: The movie titled "The Story of Film: An Odyssey" obtained the highest rating of 9.2.
-.Highest and Lowest Revenues: The movie "Avatar" had the highest revenue, while "Wild Card" had the lowest revenue.
-.Budget vs. Ratings: There was a weak positive correlation (correlation coefficient ≈ 0.08) between movie budgets and ratings.
-.Highest and Lowest Budget Movies: "The Warrior's Way" had the highest budget, while "Mr. Holmes" had the lowest budget.
-.Release Trends: The year 2014 saw the highest number of movie releases, while 1961 had the lowest.

{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {
    "tags": []
   },
   "source": [
    "\n",
    "# Project: Investigate a Dataset - [TMDB Movies Exploratory]\n",
    "\n",
    "## Table of Contents\n",
    "<ul>\n",
    "<li><a href=\"#intro\">Introduction</a></li>\n",
    "<li><a href=\"#wrangling\">Data Wrangling</a></li>\n",
    "<li><a href=\"#eda\">Exploratory Data Analysis</a></li>\n",
    "<li><a href=\"#conclusions\">Conclusions</a></li>\n",
    "</ul>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<a id='intro'></a>\n",
    "## Introduction\n",
    "\n",
    "### Dataset Description \n",
    "\n",
    "These dataset contain data for 10,000 Movie collected From Movie Database (TMDb),consist of 21 columns and 10866 Rows.The dataset used for this project is sourced from Kaggle.\n",
    "\n",
    "### Question(s) for Analysis\n",
    "In this analysis, the following 6 research questions will be explored:\n",
    "\n",
    "1.Which year Has the highest Profit Rate ?\n",
    "\n",
    "2.Which Movie got the highest Ratings ?\n",
    "\n",
    "3.What are the movies with the highest and the lowest revenues ?\n",
    "\n",
    "4.Do movies with higher budgets receive higher ratings?\n",
    "\n",
    "5.Movie with highest and lowest budget?\n",
    "\n",
    "6.Which year has the highest and lowest release of movies ?\n",
    "\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 641,
   "metadata": {
    "tags": []
   },
   "outputs": [],
   "source": [
    "import pandas as pd\n",
    "import numpy as np"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<a id='wrangling'></a>\n",
    "## Data Wrangling\n",
    "\n",
    "### General Properties\n",
    "After reviewing the dataset and analyzing the questions associated with it, then we will do some Operations to prepare the data for futher exploration and analysis."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 642,
   "metadata": {
    "tags": []
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>id</th>\n",
       "      <th>imdb_id</th>\n",
       "      <th>popularity</th>\n",
       "      <th>budget</th>\n",
       "      <th>revenue</th>\n",
       "      <th>original_title</th>\n",
       "      <th>cast</th>\n",
       "      <th>homepage</th>\n",
       "      <th>director</th>\n",
       "      <th>tagline</th>\n",
       "      <th>...</th>\n",
       "      <th>overview</th>\n",
       "      <th>runtime</th>\n",
       "      <th>genres</th>\n",
       "      <th>production_companies</th>\n",
       "      <th>release_date</th>\n",
       "      <th>vote_count</th>\n",
       "      <th>vote_average</th>\n",
       "      <th>release_year</th>\n",
       "      <th>budget_adj</th>\n",
       "      <th>revenue_adj</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>135397</td>\n",
       "      <td>tt0369610</td>\n",
       "      <td>32.985763</td>\n",
       "      <td>150000000</td>\n",
       "      <td>1513528810</td>\n",
       "      <td>Jurassic World</td>\n",
       "      <td>Chris Pratt|Bryce Dallas Howard|Irrfan Khan|Vi...</td>\n",
       "      <td>http://www.jurassicworld.com/</td>\n",
       "      <td>Colin Trevorrow</td>\n",
       "      <td>The park is open.</td>\n",
       "      <td>...</td>\n",
       "      <td>Twenty-two years after the events of Jurassic ...</td>\n",
       "      <td>124</td>\n",
       "      <td>Action|Adventure|Science Fiction|Thriller</td>\n",
       "      <td>Universal Studios|Amblin Entertainment|Legenda...</td>\n",
       "      <td>6/9/15</td>\n",
       "      <td>5562</td>\n",
       "      <td>6.5</td>\n",
       "      <td>2015</td>\n",
       "      <td>1.379999e+08</td>\n",
       "      <td>1.392446e+09</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>76341</td>\n",
       "      <td>tt1392190</td>\n",
       "      <td>28.419936</td>\n",
       "      <td>150000000</td>\n",
       "      <td>378436354</td>\n",
       "      <td>Mad Max: Fury Road</td>\n",
       "      <td>Tom Hardy|Charlize Theron|Hugh Keays-Byrne|Nic...</td>\n",
       "      <td>http://www.madmaxmovie.com/</td>\n",
       "      <td>George Miller</td>\n",
       "      <td>What a Lovely Day.</td>\n",
       "      <td>...</td>\n",
       "      <td>An apocalyptic story set in the furthest reach...</td>\n",
       "      <td>120</td>\n",
       "      <td>Action|Adventure|Science Fiction|Thriller</td>\n",
       "      <td>Village Roadshow Pictures|Kennedy Miller Produ...</td>\n",
       "      <td>5/13/15</td>\n",
       "      <td>6185</td>\n",
       "      <td>7.1</td>\n",
       "      <td>2015</td>\n",
       "      <td>1.379999e+08</td>\n",
       "      <td>3.481613e+08</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>262500</td>\n",
       "      <td>tt2908446</td>\n",
       "      <td>13.112507</td>\n",
       "      <td>110000000</td>\n",
       "      <td>295238201</td>\n",
       "      <td>Insurgent</td>\n",
       "      <td>Shailene Woodley|Theo James|Kate Winslet|Ansel...</td>\n",
       "      <td>http://www.thedivergentseries.movie/#insurgent</td>\n",
       "      <td>Robert Schwentke</td>\n",
       "      <td>One Choice Can Destroy You</td>\n",
       "      <td>...</td>\n",
       "      <td>Beatrice Prior must confront her inner demons ...</td>\n",
       "      <td>119</td>\n",
       "      <td>Adventure|Science Fiction|Thriller</td>\n",
       "      <td>Summit Entertainment|Mandeville Films|Red Wago...</td>\n",
       "      <td>3/18/15</td>\n",
       "      <td>2480</td>\n",
       "      <td>6.3</td>\n",
       "      <td>2015</td>\n",
       "      <td>1.012000e+08</td>\n",
       "      <td>2.716190e+08</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>140607</td>\n",
       "      <td>tt2488496</td>\n",
       "      <td>11.173104</td>\n",
       "      <td>200000000</td>\n",
       "      <td>2068178225</td>\n",
       "      <td>Star Wars: The Force Awakens</td>\n",
       "      <td>Harrison Ford|Mark Hamill|Carrie Fisher|Adam D...</td>\n",
       "      <td>http://www.starwars.com/films/star-wars-episod...</td>\n",
       "      <td>J.J. Abrams</td>\n",
       "      <td>Every generation has a story.</td>\n",
       "      <td>...</td>\n",
       "      <td>Thirty years after defeating the Galactic Empi...</td>\n",
       "      <td>136</td>\n",
       "      <td>Action|Adventure|Science Fiction|Fantasy</td>\n",
       "      <td>Lucasfilm|Truenorth Productions|Bad Robot</td>\n",
       "      <td>12/15/15</td>\n",
       "      <td>5292</td>\n",
       "      <td>7.5</td>\n",
       "      <td>2015</td>\n",
       "      <td>1.839999e+08</td>\n",
       "      <td>1.902723e+09</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>168259</td>\n",
       "      <td>tt2820852</td>\n",
       "      <td>9.335014</td>\n",
       "      <td>190000000</td>\n",
       "      <td>1506249360</td>\n",
       "      <td>Furious 7</td>\n",
       "      <td>Vin Diesel|Paul Walker|Jason Statham|Michelle ...</td>\n",
       "      <td>http://www.furious7.com/</td>\n",
       "      <td>James Wan</td>\n",
       "      <td>Vengeance Hits Home</td>\n",
       "      <td>...</td>\n",
       "      <td>Deckard Shaw seeks revenge against Dominic Tor...</td>\n",
       "      <td>137</td>\n",
       "      <td>Action|Crime|Thriller</td>\n",
       "      <td>Universal Pictures|Original Film|Media Rights ...</td>\n",
       "      <td>4/1/15</td>\n",
       "      <td>2947</td>\n",
       "      <td>7.3</td>\n",
       "      <td>2015</td>\n",
       "      <td>1.747999e+08</td>\n",
       "      <td>1.385749e+09</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>5 rows × 21 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "       id    imdb_id  popularity     budget     revenue  \\\n",
       "0  135397  tt0369610   32.985763  150000000  1513528810   \n",
       "1   76341  tt1392190   28.419936  150000000   378436354   \n",
       "2  262500  tt2908446   13.112507  110000000   295238201   \n",
       "3  140607  tt2488496   11.173104  200000000  2068178225   \n",
       "4  168259  tt2820852    9.335014  190000000  1506249360   \n",
       "\n",
       "                 original_title  \\\n",
       "0                Jurassic World   \n",
       "1            Mad Max: Fury Road   \n",
       "2                     Insurgent   \n",
       "3  Star Wars: The Force Awakens   \n",
       "4                     Furious 7   \n",
       "\n",
       "                                                cast  \\\n",
       "0  Chris Pratt|Bryce Dallas Howard|Irrfan Khan|Vi...   \n",
       "1  Tom Hardy|Charlize Theron|Hugh Keays-Byrne|Nic...   \n",
       "2  Shailene Woodley|Theo James|Kate Winslet|Ansel...   \n",
       "3  Harrison Ford|Mark Hamill|Carrie Fisher|Adam D...   \n",
       "4  Vin Diesel|Paul Walker|Jason Statham|Michelle ...   \n",
       "\n",
       "                                            homepage          director  \\\n",
       "0                      http://www.jurassicworld.com/   Colin Trevorrow   \n",
       "1                        http://www.madmaxmovie.com/     George Miller   \n",
       "2     http://www.thedivergentseries.movie/#insurgent  Robert Schwentke   \n",
       "3  http://www.starwars.com/films/star-wars-episod...       J.J. Abrams   \n",
       "4                           http://www.furious7.com/         James Wan   \n",
       "\n",
       "                         tagline  ...  \\\n",
       "0              The park is open.  ...   \n",
       "1             What a Lovely Day.  ...   \n",
       "2     One Choice Can Destroy You  ...   \n",
       "3  Every generation has a story.  ...   \n",
       "4            Vengeance Hits Home  ...   \n",
       "\n",
       "                                            overview runtime  \\\n",
       "0  Twenty-two years after the events of Jurassic ...     124   \n",
       "1  An apocalyptic story set in the furthest reach...     120   \n",
       "2  Beatrice Prior must confront her inner demons ...     119   \n",
       "3  Thirty years after defeating the Galactic Empi...     136   \n",
       "4  Deckard Shaw seeks revenge against Dominic Tor...     137   \n",
       "\n",
       "                                      genres  \\\n",
       "0  Action|Adventure|Science Fiction|Thriller   \n",
       "1  Action|Adventure|Science Fiction|Thriller   \n",
       "2         Adventure|Science Fiction|Thriller   \n",
       "3   Action|Adventure|Science Fiction|Fantasy   \n",
       "4                      Action|Crime|Thriller   \n",
       "\n",
       "                                production_companies release_date vote_count  \\\n",
       "0  Universal Studios|Amblin Entertainment|Legenda...       6/9/15       5562   \n",
       "1  Village Roadshow Pictures|Kennedy Miller Produ...      5/13/15       6185   \n",
       "2  Summit Entertainment|Mandeville Films|Red Wago...      3/18/15       2480   \n",
       "3          Lucasfilm|Truenorth Productions|Bad Robot     12/15/15       5292   \n",
       "4  Universal Pictures|Original Film|Media Rights ...       4/1/15       2947   \n",
       "\n",
       "   vote_average  release_year    budget_adj   revenue_adj  \n",
       "0           6.5          2015  1.379999e+08  1.392446e+09  \n",
       "1           7.1          2015  1.379999e+08  3.481613e+08  \n",
       "2           6.3          2015  1.012000e+08  2.716190e+08  \n",
       "3           7.5          2015  1.839999e+08  1.902723e+09  \n",
       "4           7.3          2015  1.747999e+08  1.385749e+09  \n",
       "\n",
       "[5 rows x 21 columns]"
      ]
     },
     "execution_count": 642,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "\n",
    "df=pd.read_csv('Database_TMDb_movie_data/tmdb-movies.csv')\n",
    "df.head()\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 643,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(10866, 21)"
      ]
     },
     "execution_count": 643,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.shape\n",
    "\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 644,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "id                        int64\n",
       "imdb_id                  object\n",
       "popularity              float64\n",
       "budget                    int64\n",
       "revenue                   int64\n",
       "original_title           object\n",
       "cast                     object\n",
       "homepage                 object\n",
       "director                 object\n",
       "tagline                  object\n",
       "keywords                 object\n",
       "overview                 object\n",
       "runtime                   int64\n",
       "genres                   object\n",
       "production_companies     object\n",
       "release_date             object\n",
       "vote_count                int64\n",
       "vote_average            float64\n",
       "release_year              int64\n",
       "budget_adj              float64\n",
       "revenue_adj             float64\n",
       "dtype: object"
      ]
     },
     "execution_count": 644,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "\n",
    "df.dtypes\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 645,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "RangeIndex: 10866 entries, 0 to 10865\n",
      "Data columns (total 21 columns):\n",
      " #   Column                Non-Null Count  Dtype  \n",
      "---  ------                --------------  -----  \n",
      " 0   id                    10866 non-null  int64  \n",
      " 1   imdb_id               10856 non-null  object \n",
      " 2   popularity            10866 non-null  float64\n",
      " 3   budget                10866 non-null  int64  \n",
      " 4   revenue               10866 non-null  int64  \n",
      " 5   original_title        10866 non-null  object \n",
      " 6   cast                  10790 non-null  object \n",
      " 7   homepage              2936 non-null   object \n",
      " 8   director              10822 non-null  object \n",
      " 9   tagline               8042 non-null   object \n",
      " 10  keywords              9373 non-null   object \n",
      " 11  overview              10862 non-null  object \n",
      " 12  runtime               10866 non-null  int64  \n",
      " 13  genres                10843 non-null  object \n",
      " 14  production_companies  9836 non-null   object \n",
      " 15  release_date          10866 non-null  object \n",
      " 16  vote_count            10866 non-null  int64  \n",
      " 17  vote_average          10866 non-null  float64\n",
      " 18  release_year          10866 non-null  int64  \n",
      " 19  budget_adj            10866 non-null  float64\n",
      " 20  revenue_adj           10866 non-null  float64\n",
      "dtypes: float64(4), int64(6), object(11)\n",
      "memory usage: 1.7+ MB\n"
     ]
    }
   ],
   "source": [
    "\n",
    "df.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 646,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "id                         0\n",
      "imdb_id                   10\n",
      "popularity                 0\n",
      "budget                     0\n",
      "revenue                    0\n",
      "original_title             0\n",
      "cast                      76\n",
      "homepage                7930\n",
      "director                  44\n",
      "tagline                 2824\n",
      "keywords                1493\n",
      "overview                   4\n",
      "runtime                    0\n",
      "genres                    23\n",
      "production_companies    1030\n",
      "release_date               0\n",
      "vote_count                 0\n",
      "vote_average               0\n",
      "release_year               0\n",
      "budget_adj                 0\n",
      "revenue_adj                0\n",
      "dtype: int64\n"
     ]
    }
   ],
   "source": [
    "print(df.isnull().sum())"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 647,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>id</th>\n",
       "      <th>popularity</th>\n",
       "      <th>budget</th>\n",
       "      <th>revenue</th>\n",
       "      <th>runtime</th>\n",
       "      <th>vote_count</th>\n",
       "      <th>vote_average</th>\n",
       "      <th>release_year</th>\n",
       "      <th>budget_adj</th>\n",
       "      <th>revenue_adj</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>10866.000000</td>\n",
       "      <td>10866.000000</td>\n",
       "      <td>1.086600e+04</td>\n",
       "      <td>1.086600e+04</td>\n",
       "      <td>10866.000000</td>\n",
       "      <td>10866.000000</td>\n",
       "      <td>10866.000000</td>\n",
       "      <td>10866.000000</td>\n",
       "      <td>1.086600e+04</td>\n",
       "      <td>1.086600e+04</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>66064.177434</td>\n",
       "      <td>0.646441</td>\n",
       "      <td>1.462570e+07</td>\n",
       "      <td>3.982332e+07</td>\n",
       "      <td>102.070863</td>\n",
       "      <td>217.389748</td>\n",
       "      <td>5.974922</td>\n",
       "      <td>2001.322658</td>\n",
       "      <td>1.755104e+07</td>\n",
       "      <td>5.136436e+07</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>92130.136561</td>\n",
       "      <td>1.000185</td>\n",
       "      <td>3.091321e+07</td>\n",
       "      <td>1.170035e+08</td>\n",
       "      <td>31.381405</td>\n",
       "      <td>575.619058</td>\n",
       "      <td>0.935142</td>\n",
       "      <td>12.812941</td>\n",
       "      <td>3.430616e+07</td>\n",
       "      <td>1.446325e+08</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>5.000000</td>\n",
       "      <td>0.000065</td>\n",
       "      <td>0.000000e+00</td>\n",
       "      <td>0.000000e+00</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>10.000000</td>\n",
       "      <td>1.500000</td>\n",
       "      <td>1960.000000</td>\n",
       "      <td>0.000000e+00</td>\n",
       "      <td>0.000000e+00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>10596.250000</td>\n",
       "      <td>0.207583</td>\n",
       "      <td>0.000000e+00</td>\n",
       "      <td>0.000000e+00</td>\n",
       "      <td>90.000000</td>\n",
       "      <td>17.000000</td>\n",
       "      <td>5.400000</td>\n",
       "      <td>1995.000000</td>\n",
       "      <td>0.000000e+00</td>\n",
       "      <td>0.000000e+00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>20669.000000</td>\n",
       "      <td>0.383856</td>\n",
       "      <td>0.000000e+00</td>\n",
       "      <td>0.000000e+00</td>\n",
       "      <td>99.000000</td>\n",
       "      <td>38.000000</td>\n",
       "      <td>6.000000</td>\n",
       "      <td>2006.000000</td>\n",
       "      <td>0.000000e+00</td>\n",
       "      <td>0.000000e+00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>75610.000000</td>\n",
       "      <td>0.713817</td>\n",
       "      <td>1.500000e+07</td>\n",
       "      <td>2.400000e+07</td>\n",
       "      <td>111.000000</td>\n",
       "      <td>145.750000</td>\n",
       "      <td>6.600000</td>\n",
       "      <td>2011.000000</td>\n",
       "      <td>2.085325e+07</td>\n",
       "      <td>3.369710e+07</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>417859.000000</td>\n",
       "      <td>32.985763</td>\n",
       "      <td>4.250000e+08</td>\n",
       "      <td>2.781506e+09</td>\n",
       "      <td>900.000000</td>\n",
       "      <td>9767.000000</td>\n",
       "      <td>9.200000</td>\n",
       "      <td>2015.000000</td>\n",
       "      <td>4.250000e+08</td>\n",
       "      <td>2.827124e+09</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                  id    popularity        budget       revenue       runtime  \\\n",
       "count   10866.000000  10866.000000  1.086600e+04  1.086600e+04  10866.000000   \n",
       "mean    66064.177434      0.646441  1.462570e+07  3.982332e+07    102.070863   \n",
       "std     92130.136561      1.000185  3.091321e+07  1.170035e+08     31.381405   \n",
       "min         5.000000      0.000065  0.000000e+00  0.000000e+00      0.000000   \n",
       "25%     10596.250000      0.207583  0.000000e+00  0.000000e+00     90.000000   \n",
       "50%     20669.000000      0.383856  0.000000e+00  0.000000e+00     99.000000   \n",
       "75%     75610.000000      0.713817  1.500000e+07  2.400000e+07    111.000000   \n",
       "max    417859.000000     32.985763  4.250000e+08  2.781506e+09    900.000000   \n",
       "\n",
       "         vote_count  vote_average  release_year    budget_adj   revenue_adj  \n",
       "count  10866.000000  10866.000000  10866.000000  1.086600e+04  1.086600e+04  \n",
       "mean     217.389748      5.974922   2001.322658  1.755104e+07  5.136436e+07  \n",
       "std      575.619058      0.935142     12.812941  3.430616e+07  1.446325e+08  \n",
       "min       10.000000      1.500000   1960.000000  0.000000e+00  0.000000e+00  \n",
       "25%       17.000000      5.400000   1995.000000  0.000000e+00  0.000000e+00  \n",
       "50%       38.000000      6.000000   2006.000000  0.000000e+00  0.000000e+00  \n",
       "75%      145.750000      6.600000   2011.000000  2.085325e+07  3.369710e+07  \n",
       "max     9767.000000      9.200000   2015.000000  4.250000e+08  2.827124e+09  "
      ]
     },
     "execution_count": 647,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.describe()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "\n",
    "### Data Cleaning\n",
    "These following operations were performed to enhance the dataset,ensuring its \n",
    "cleanliness and suitability for analysis:\n",
    "\n",
    "1.Drop the columns that are not essential for the analysis.\n",
    "\n",
    "2.remove the duplicate rows from the dataset.\n",
    "\n",
    "3.Handle with missing values.\n",
    "\n",
    "4.convert data types for release_data,budget and revenue.\n",
    " "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### 1.Drop the columns that are not essential for the analysis.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "drop the columns which are not usable in the data analysis proocess such as homepage,tagline,imdb_id,budget_adj,revenue_adj,and overview.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 648,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "after the drop the columns that not usable the shape= 15\n"
     ]
    }
   ],
   "source": [
    "columnsdrop = ['imdb_id', 'budget_adj', 'homepage', 'tagline', 'revenue_adj', 'overview']\n",
    "df = df.drop(columns=columnsdrop)\n",
    "num_col_afterdrop = df.shape[1]\n",
    "print(\"after the drop the columns that not usable the shape=\",num_col_afterdrop)\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### 2.remove the duplicate rows from the dataset."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "removed duplicate rows from the dataset before proceeding with further analysis."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 649,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "after removing duplicates value the number of rows is= 10865\n"
     ]
    }
   ],
   "source": [
    "df.drop_duplicates(inplace=True)\n",
    "num_row_remove = df.shape[0]\n",
    "print('after removing duplicates value the number of rows is=',num_row_remove)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### 3.Handle with missing values."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Check for missing values, then handle them accordingly, such as replacing missing values in numerical columns with the mean."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 650,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "id                         0\n",
      "popularity                 0\n",
      "budget                     0\n",
      "revenue                    0\n",
      "original_title             0\n",
      "cast                      76\n",
      "director                  44\n",
      "keywords                1493\n",
      "runtime                    0\n",
      "genres                    23\n",
      "production_companies    1030\n",
      "release_date               0\n",
      "vote_count                 0\n",
      "vote_average               0\n",
      "release_year               0\n",
      "dtype: int64\n"
     ]
    }
   ],
   "source": [
    "#check for missing values for all columns\n",
    "missvalue=df.isnull().sum()\n",
    "print(missvalue)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 651,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "after handle with missing value:\n",
      " id                      0\n",
      "popularity              0\n",
      "budget                  0\n",
      "revenue                 0\n",
      "original_title          0\n",
      "cast                    0\n",
      "director                0\n",
      "keywords                0\n",
      "runtime                 0\n",
      "genres                  0\n",
      "production_companies    0\n",
      "release_date            0\n",
      "vote_count              0\n",
      "vote_average            0\n",
      "release_year            0\n",
      "dtype: int64\n"
     ]
    }
   ],
   "source": [
    "#handle missing value with cast,director,genres,keywords,and production companiesby replacing them with 'unknown'.\n",
    "categorical_col=['cast','director','genres','production_companies','keywords']\n",
    "for col in categorical_col:\n",
    "    df[col].fillna('Unknown', inplace=True)\n",
    "    \n",
    "missvalue=df.isnull().sum()\n",
    "print(\"after handle with missing value:\\n\",missvalue)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### 4.convert data types for release_data , and revenue"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "To ensure consistency in our analysis, we need to convert the data types for the 'release_date' and 'revenue' columns as follows: \n",
    "\n",
    "    1.release date: convert to datetime format,to allow perform \n",
    "    data-based operations.\n",
    "    \n",
    "    2.revenue: convert to numeric format, to enable us to do mathematical operations."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 652,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "id                               int64\n",
       "popularity                     float64\n",
       "budget                           int64\n",
       "revenue                          int64\n",
       "original_title                  object\n",
       "cast                            object\n",
       "director                        object\n",
       "keywords                        object\n",
       "runtime                          int64\n",
       "genres                          object\n",
       "production_companies            object\n",
       "release_date            datetime64[ns]\n",
       "vote_count                       int64\n",
       "vote_average                   float64\n",
       "release_year                     int64\n",
       "dtype: object"
      ]
     },
     "execution_count": 652,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "\n",
    "df['release_date'] = pd.to_datetime(df['release_date'])\n",
    "df['revenue'] = pd.to_numeric(df['revenue'])\n",
    "df.dtypes\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<a id='eda'></a>\n",
    "## Exploratory Data Analysis\n",
    "In the EDA section, we'll dive into the data to uncover patterns and insights. By crunching numbers and making charts, we'll answer our research questions.\n",
    "\n",
    "### Research Question 1 (Which year Has the highest Profit Rate ?)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 653,
   "metadata": {
    "tags": []
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "year with the highest profit rate : 2015\n"
     ]
    }
   ],
   "source": [
    "# calculate profit for each movie\n",
    "df['profit'] = df['revenue'] - df['budget']\n",
    "# group data by release year and sum up profits for each year\n",
    "profit_by_year = df.groupby('release_year')['profit'].sum()\n",
    "#find year with highest profit\n",
    "highest_profit_year = profit_by_year.idxmax()\n",
    "\n",
    "print(\"year with the highest profit rate :\",highest_profit_year)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 654,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAA2EAAAMfCAYAAABfJN+OAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjYuMywgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy/P9b71AAAACXBIWXMAAA9hAAAPYQGoP6dpAACujUlEQVR4nOzdeXxTZdr/8W+SlpZ9Ky2UHYoolB1BBAWlCug44Ib40wFRcXlkVCoy4AIiCriw6Igyior46IgbOI86OFApjmyKUAEBlX0pLS2lFAqUtrl/f9QcmiYpKbSntn7er1de0Dtnua7cd05y5T45cRhjjAAAAAAAtnCWdwAAAAAA8EdCEQYAAAAANqIIAwAAAAAbUYQBAAAAgI0owgAAAADARhRhAAAAAGAjijAAAAAAsBFFGAAAAADYiCIMAAAAAGxEEQYAlVRiYqIcDocSExPLOxRLXl6exo0bp6ZNm8rpdGrIkCGSJIfDoaeeeqpM9+1wODR69Ogy3UdZ2L17txwOh+bPn1/eoQAASglFGACUIofDEdQtmMJo6tSpWrx4cZnHPH/+fK/YwsPDdcEFF2j06NFKTU0t1X299dZbeuGFF3TTTTfpnXfe0ZgxY/wut2rVKj311FPKzMws1f2XNU/h67m5XC5FRkbqpptu0tatW8s7vHKxevVqOZ1OTZgwwe/9zz33nBwOh7744gubIwOA8hNS3gEAQGXy7rvvev29YMECLV261Kf9oosuOuu2pk6dqptuusmaLSprTz/9tFq2bKlTp07p22+/1WuvvaYvv/xSmzdvVrVq1UplH19//bUaN26sWbNmebWfPHlSISFnXpJWrVqlyZMn64477lCdOnVKZd92evDBB3XxxRcrNzdXGzdu1Ny5c5WYmKjNmzerYcOG5R2erXr16qV7771XM2bM0O2336727dtb9+3Zs0dPP/20br75Zl177bXlGCUA2IsiDABK0e233+7195o1a7R06VKf9t+jQYMGqXv37pKku+++W/Xr19fMmTP12Wef6dZbb/W7TnZ2tqpXrx70Pg4dOuS3qAoPDz+nmH+vLrvsMt10003W323bttX999+vBQsWaNy4ceUYWfmYPn26PvvsM917773673//K4fDIUn661//qtDQUL300ku2xHHixIlS+0ABAM4HpyMCgM2ys7P1yCOPqGnTpgoLC1Pbtm314osvyhhjLeNwOJSdna133nnHOrXtjjvukFQwe/A///M/atu2rapWrar69evr5ptv1u7du0s1ziuvvFKStGvXLknSHXfcoRo1amjHjh265pprVLNmTd12221B5eT5XtPy5cv1008/+ZyWWfg7YU899ZQeffRRSVLLli2tZT35LV26VH369FGdOnVUo0YNtW3bVo899ljQeb333ntq27atwsPD1a1bN33zzTfWfcuXL5fD4dCiRYt81nv//fflcDi0evXq4B/E31x22WWSpB07dni1HzhwQHfeeaeioqIUFham9u3b66233gpqm9u2bdNNN92kevXqKTw8XN27d9e//vUvr2UyMjI0duxYdejQQTVq1FCtWrU0aNAg/fjjjz7b+/vf/6727durWrVqqlu3rrp3767333+/VOKtXbu2XnrpJa1cuVLz5s2TJC1atEj/93//p+nTp6tRo0Zyu92aPXu22rdvr/DwcEVFRenee+/VkSNHvLb12Wef6dprr1V0dLTCwsLUunVrTZkyRfn5+V7L9evXT7Gxsfrhhx90+eWXq1q1aiUaJwBQlpgJAwAbGWP05z//WcuXL9ddd92lzp0766uvvtKjjz6qAwcOWKfpvfvuu7r77rvVo0cP3XPPPZKk1q1bS5K+//57rVq1SsOGDVOTJk20e/duvfbaa+rXr5+2bNlSap/0ewqG+vXrW215eXkaMGCA+vTpoxdffFHVqlULKqcGDRro3Xff1bPPPqvjx49r2rRpkvyflnnDDTfol19+0T//+U/NmjVLERERkqQGDRrop59+0p/+9Cd17NhRTz/9tMLCwrR9+3atXLkyqJxWrFihhQsX6sEHH1RYWJheffVVDRw4UN99951iY2PVr18/NW3aVO+9956uv/56r3Xfe+89tW7dWr169SrxY+kpIOvWrWu1paam6pJLLrEuGNKgQQP9+9//1l133aWsrCw9/PDDAbf3008/qXfv3mrcuLHGjx+v6tWr68MPP9SQIUP0ySefWLHv3LlTixcv1s0336yWLVsqNTVV//jHP9S3b19t2bJF0dHRkqQ33nhDDz74oG666SY99NBDOnXqlDZu3Ki1a9fq//2//3fe8UqyTjn829/+pv79++uhhx7SpZdeqnvvvVeSdO+992r+/PkaOXKkHnzwQe3atUuvvPKKNmzYoJUrVyo0NFRSwXcYa9Soofj4eNWoUUNff/21Jk6cqKysLL3wwgte+zx8+LAGDRqkYcOG6fbbb1dUVFTQfQYAZcoAAMrMAw88YAofahcvXmwkmWeeecZruZtuusk4HA6zfft2q6169epmxIgRPts8ceKET9vq1auNJLNgwQKrbfny5UaSWb58ebExvv3220aSWbZsmUlLSzP79u0zH3zwgalfv76pWrWq2b9/vzHGmBEjRhhJZvz48V7rlySnvn37mvbt2/vEIMlMmjTJ+vuFF14wksyuXbu8lps1a5aRZNLS0orNyR9JRpJZt26d1bZnzx4THh5urr/+eqttwoQJJiwszGRmZlpthw4dMiEhIV4x+uN5zN966y2TlpZmkpOTzZIlS0xMTIxxOBzmu+++s5a96667TKNGjUx6errXNoYNG2Zq165t9fOuXbuMJPP2229by/Tv39906NDBnDp1ympzu93m0ksvNW3atLHaTp06ZfLz8722v2vXLhMWFmaefvppq23w4MF++6WwYOMtzu7du0316tVNvXr1TGhoqNm0aZMxxpj//ve/RpJ57733vJZfsmSJT7u//dx7772mWrVqXo9H3759jSQzd+7cs8YFAHbjdEQAsNGXX34pl8ulBx980Kv9kUcekTFG//73v8+6japVq1r/z83N1eHDhxUTE6M6depo/fr15xxbXFycGjRooKZNm2rYsGGqUaOGFi1apMaNG3std//995d6TsHyfJ/ss88+k9vtLvH6vXr1Urdu3ay/mzVrpsGDB+urr76yTmcbPny4cnJy9PHHH1vLLVy4UHl5eUF/t+/OO+9UgwYNFB0drYEDB+ro0aN69913dfHFF0sqmBH95JNPdN1118kYo/T0dOs2YMAAHT16NGBfZmRk6Ouvv9bQoUN17Ngxa73Dhw9rwIAB+vXXX3XgwAFJUlhYmJzOgpf6/Px8HT582DqFs/D269Spo/379+v777/3u8/zibew5s2ba9KkScrIyFB8fLxiY2MlSR999JFq166tq666ymvb3bp1U40aNbR8+XJrG4XHvyf/yy67TCdOnNC2bdu89hcWFqaRI0eeNS4AsBtF2Fl88803uu666xQdHS2Hw1Hiy0WfOnVKd9xxhzp06KCQkJCAVzlLTExU165dFRYWppiYGH4PBqik9uzZo+joaNWsWdOr3XNa3p49e866jZMnT2rixInW968iIiLUoEEDZWZm6ujRo+cc25w5c7R06VItX75cW7Zs0c6dOzVgwACvZUJCQtSkSZNSzylYt9xyi3r37q27775bUVFRGjZsmD788MOgC7I2bdr4tF1wwQU6ceKE0tLSJEkXXnihLr74Yr333nvWMu+9954uueQSxcTEBLWfiRMnaunSpVq0aJGGDx+uo0ePWsWQJKWlpSkzM1Ovv/66GjRo4HXzFA2HDh3yu+3t27fLGKMnn3zSZ91JkyZ5ret2uzVr1iy1adPGa6xs3LjRa6z87W9/U40aNdSjRw+1adNGDzzwgNcpnucTb1GeQtRzERhJ+vXXX3X06FFFRkb6bP/48eNe2/7pp590/fXXq3bt2qpVq5YaNGhgFcdFx3/jxo1VpUqVoOICADvxnbCzyM7OVqdOnXTnnXfqhhtuKPH6+fn5qlq1qh588EF98sknfpfZtWuXrr32Wt1333167733lJCQoLvvvluNGjXyeQMEAH/961/19ttv6+GHH1avXr1Uu3ZtORwODRs27Jxmhzx69Ojh9cbYn8IzK+WhatWq+uabb7R8+XJ98cUXWrJkiRYuXKgrr7xS//nPf+RyuUplP8OHD9dDDz2k/fv3KycnR2vWrNErr7wS9PodOnRQXFycJGnIkCE6ceKERo0apT59+qhp06ZWP91+++0aMWKE32107NjRb7tn3bFjxwZ8jfAUi1OnTtWTTz6pO++8U1OmTFG9evXkdDr18MMPe42Viy66SD///LM+//xzLVmyRJ988oleffVVTZw4UZMnTz6veIPhdrsVGRnpVfgW1qBBA0lSZmam+vbtq1q1aunpp59W69atFR4ervXr1+tvf/ubz/gvPGsGAL8nFGFnMWjQIA0aNCjg/Tk5OXr88cf1z3/+U5mZmYqNjdVzzz2nfv36SZKqV6+u1157TZK0cuVKvz88OnfuXLVs2VIzZsyQVPBi+O2332rWrFkUYUAl07x5cy1btkzHjh3zmjnynEbVvHlzq81zGe+iPv74Y40YMcI6ZkgFs+7l9cPGJckpWIFylySn06n+/furf//+mjlzpqZOnarHH39cy5cvtwqfQH799Veftl9++UXVqlWz3uhL0rBhwxQfH69//vOfOnnypEJDQ3XLLbeUOA+P6dOna9GiRXr22Wc1d+5cNWjQQDVr1lR+fv5ZYy6qVatWkqTQ0NCzrvvxxx/riiuu0JtvvunVnpmZaV3wxKN69eq65ZZbdMstt+j06dO64YYb9Oyzz2rChAnnFW8wWrdurWXLlql3797FFk6JiYk6fPiwPv30U11++eVWu+cKngBQUXA64nkaPXq0Vq9erQ8++EAbN27UzTffrIEDB/p9oQ9k9erVPi9qAwYMOKfLIAP4fbvmmmuUn5/vM6sya9YsORwOrw99qlev7rewcrlcXpezlwouL170Et12KUlOwfL89ljR/DMyMnyW7dy5s6SCD8XOZvXq1V7fXdq3b58+++wzXX311V6zaBERERo0aJD+93//V++9954GDhzoU7SUROvWrXXjjTdq/vz5SklJkcvl0o033qhPPvlEmzdv9lnec2qkP5GRkerXr5/+8Y9/6ODBg8Wu62+sfPTRR9Z3xjwOHz7s9XeVKlXUrl07GWOUm5t7XvEGY+jQocrPz9eUKVN87svLy7PGgaePCud0+vRpvfrqq+e1fwCwGzNh52Hv3r16++23tXfvXusyv2PHjtWSJUv09ttva+rUqUFtJyUlxeeyuVFRUcrKytLJkyc5nQKoRK677jpdccUVevzxx7V792516tRJ//nPf/TZZ5/p4Ycfti5DL0ndunXTsmXLNHPmTEVHR6tly5bq2bOn/vSnP+ndd99V7dq11a5dO61evVrLli3zupT87zWnYHkunvH4449r2LBhCg0N1XXXXaenn35a33zzja699lo1b95chw4d0quvvqomTZqoT58+Z91ubGysBgwY4HWJekmaPHmyz7LDhw+3fnDZX3FQUo8++qg+/PBDzZ49W9OnT9f06dO1fPly9ezZU6NGjVK7du2UkZGh9evXa9myZX4LTo85c+aoT58+6tChg0aNGqVWrVopNTVVq1ev1v79+63fAfvTn/6kp59+WiNHjtSll16qTZs26b333rNm0zyuvvpqNWzYUL1791ZUVJS2bt2qV155Rddee601u3k+8Z5N3759de+992ratGlKSkrS1VdfrdDQUP3666/66KOP9NJLL+mmm27SpZdeqrp162rEiBF68MEH5XA49O677/oUmgDwu1c+F2WsmCSZRYsWWX9//vnnRpKpXr261y0kJMQMHTrUZ/0RI0aYwYMH+7S3adPGTJ061avtiy++MJKCuuQvgN+vopeoN8aYY8eOmTFjxpjo6GgTGhpq2rRpY1544QXjdru9ltu2bZu5/PLLTdWqVY0k63L1R44cMSNHjjQRERGmRo0aZsCAAWbbtm2mefPmXpe0L+kl6r///vtilxsxYoSpXr263/uCzSnYS9QbY8yUKVNM48aNjdPptC5Xn5CQYAYPHmyio6NNlSpVTHR0tLn11lvNL7/8Umzsnn088MAD5n//939NmzZtTFhYmOnSpUvAxycnJ8fUrVvX1K5d25w8efKs2zfmzGP+0Ucf+b2/X79+platWtbl71NTU80DDzxgmjZtakJDQ03Dhg1N//79zeuvv26t4+8S9cYYs2PHDjN8+HDTsGFDExoaaho3bmz+9Kc/mY8//tha5tSpU+aRRx4xjRo1MlWrVjW9e/c2q1evNn379jV9+/a1lvvHP/5hLr/8clO/fn0TFhZmWrdubR599FFz9OhRr30GE+/5PEavv/666datm6lataqpWbOm6dChgxk3bpxJTk62llm5cqW55JJLTNWqVU10dLQZN26c+eqrr3zGeqCxBgC/Bw5j+PgoWA6HQ4sWLbKucLhw4ULddttt+umnn3y+DF6jRg01bNjQq+2OO+5QZmamzxUWL7/8cnXt2lWzZ8+22jxfuj+fK50BAM5dXl6eoqOjdd111/l8pwoAgPPB6YjnoUuXLsrPz9ehQ4d02WWXnfN2evXqpS+//NKrbenSperVq9f5hggAOEeLFy9WWlqahg8fXt6hAAAqGYqwszh+/Li2b99u/b1r1y4lJSWpXr16uuCCC3Tbbbdp+PDhmjFjhrp06aK0tDQlJCSoY8eOuvbaayVJW7Zs0enTp5WRkaFjx44pKSlJ0pkvk99333165ZVXNG7cON155536+uuv9eGHH+qLL76wO10A+MNbu3atNm7cqClTpqhLly7q27dveYcEAKhkOB3xLBITE3XFFVf4tI8YMULz589Xbm6unnnmGS1YsEAHDhxQRESELrnkEk2ePFkdOnSQJLVo0cLvj5UWfugTExM1ZswYbdmyRU2aNNGTTz6pO+64o8zyAgD4d8cdd+h///d/1blzZ82fP1+xsbHlHRIAoJKhCAMAAAAAG/E7YQAAAABgI4owAAAAALARF+bww+12Kzk5WTVr1pTD4SjvcAAAAACUE2OMjh07pujoaDmdpTSHVX4/UWbM1KlTTffu3U2NGjVMgwYNzODBg822bdvOut6HH35o2rZta8LCwkxsbKz54osvvO53u93mySefNA0bNjTh4eGmf//+Qf2Qp8e+ffuMJG7cuHHjxo0bN27cuHEzksy+fftKXO8EUq4X5hg4cKCGDRumiy++WHl5eXrssce0efNmbdmyRdWrV/e7zqpVq3T55Zdr2rRp+tOf/qT3339fzz33nNavX29dweq5557TtGnT9M4776hly5Z68skntWnTJm3ZskXh4eFnjevo0aOqU6eO9u3bp1q1apVqzgAAAAAqjqysLDVt2lSZmZmqXbt2qWzzd3V1xLS0NEVGRmrFihW6/PLL/S5zyy23KDs7W59//rnVdskll6hz586aO3eujDGKjo7WI488orFjx0oqKKqioqI0f/58DRs27KxxZGVlqXbt2jp69ChFGAAAAPAHVha1we/qO2FHjx6VJNWrVy/gMqtXr1Z8fLxX24ABA7R48WJJBT+mnJKSori4OOv+2rVrq2fPnlq9erXfIiwnJ0c5OTnW31lZWZKk3Nxc5ebmSpKcTqdcLpfy8/PldrutZV0ul5xOp/Ly8rx+9+ts7Z7teoSEFHRFXl5eUO2hoaFyu93Kz8+32hwOh0JCQoJuJydyIidyIidyIidyIidyIqficyp6f2n43RRhbrdbDz/8sHr37l3sD2OmpKQoKirKqy0qKkopKSnW/Z62QMsUNW3aNE2ePNmnPTEx0TotskmTJoqNjdXWrVu1f/9+a5mYmBjFxMQoKSlJ6enpVntsbKyaNGmiNWvW6Pjx41Z79+7dFRERoRUrVngNyt69eys8PFwJCQleMfTv31+nTp3SypUrrbaQkBDFxcUpIyND69ats9pr1KihPn36KDk5WZs3b7baIyIi1L17d+3cuVPbt2+32smJnMiJnMiJnMiJnMiJnMip+Jyys7NV2n43pyPef//9+ve//61vv/1WTZo0CbhclSpV9M477+jWW2+12l599VVNnjxZqampWrVqlXr37q3k5GQ1atTIWmbo0KFyOBxauHChzzb9zYQ1bdpU6enp1pQjnyKQEzmREzmREzmREzmREzn98XLKyspSRERE5TsdcfTo0fr888/1zTffFFuASVLDhg2Vmprq1ZaamqqGDRta93vaChdhqamp6ty5s99thoWFKSwszKc9NDRUoaGhXm0ul0sul8tnWU9nBdtedLvn0u50Ov1eJrOk7eRETiVtJydy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T54M+Lhs2rTJ1K1b19x5551m8ODBZuDAgaZu3bpmyZIlxe5r69atplatWmbEiBHmxhtvNFdddZUJCwszCxYsKHa9bdu2maioKHPxxReb//73v0Hl5YmzQYMGZujQoaZXr17m4osvNvfdd585fvx4sett3LjR1K1b19x7773m/vvvNwMGDDAjR440p0+fPutYWbVqlWnatKlp06aNGTBggNV+trFSrVq1Eo+VYFCEnaeDBw+aVq1amccee8z8+OOP5vvvvzdxcXGmUaNGZt68edYb56J27txpvcB069bNejE82xvsrVu3mvr165tx48aZpUuXmnnz5pkOHTqYl19+OeA6W7ZsMfXr1zePPfaY2bp1q/nvf/9roqKizLfffhtUjvfff78ZNWqUqVatmvnrX//q8wJfdNBv2rTJVKtWzTzxxBNWW1ZWljl06FCx+zl9+rS57bbbzL333mttd926deaTTz4xhw4dMidPnvS7nucJMmnSJJOdnW1atGhhHnroobPmtX//fhMTE2OmTJli5dS6dWvz3nvvBVxnz549plmzZuapp54yv/76qzlw4IC56qqrTGRkpHnxxRdNenq63/X27dtnoqOjzfjx401iYqL56KOPTLdu3UyzZs3MsmXLAvb79u3bTePGjU14eLi58cYbgy7EtmzZYurVq2fGjBljFi5caB5//HFz8cUXm88++6zY9TwH/PHjx5vvvvvOLFiwwLRq1cr89NNP1jLFHeRuuOEGM3LkSBMaGmqmT59e7L42btxoqlev7lUcnjp1ymt8+Tswnjhxwvz5z382o0ePtuL5+eefTWJiYrFv1DzjZMqUKebQoUOmZs2aZurUqcXGaMyZPvest2/fPtOkSZOzvqDt3LnTNGrUyDzxxBNm3bp1ZuXKlaZr166mbdu25qOPPgo4ns/lmGLn8cSYyn1MsfN4Ysy5H1MqwmuPMec3Vn7P48SYijFW8vLyzO233+5VMG/YsMHcddddxuVymc8//9wY43usPXDggLn00ktNp06dTI8ePcxdd91lNm3adNbcdu/ebdq0aWMee+wxc/r0aWOMMePHjzcxMTEBH8cdO3aY5s2bm8cff9xqu+uuu8yDDz5ojDn7hwRffvmlueCCC8z06dNNhw4drH40xphjx475LL9161YTEhJinn76aSv3hIQE849//MOsXLmy2GL4gw8+MP369bPWe/zxx82wYcPMDTfcYBISEvyus2HDBlOlShUzfvx4Y4wxX3/9tWnevLn54IMPis3r5MmT5vrrrzf333+/1fbmm2+a2267zZw+fdqkpaX5rHP8+HEzYMAArw8hfvjhB1O3bl0TFhZmPvzwQyv2ov7nf/7HDBkyxPo7NTXVPPHEE8blcplXX33VGOP7nDt48KDp16+f6d27txk0aJC5+uqrzTfffFNsXsYUFLPt2rWzHhNjjJkzZ45p1aqVOXDgQMD1du7caVq3bu01Vp566ilz5513WvkHys/tdpvVq1ebiy66yLz//vvmggsuMNdcc411v7/9esaKJ063220++eQTM3XqVPPPf/7T/Pzzz2fNtTgUYedp3bp1JiYmxmzbts2rfeTIkaZZs2bm/fff9xm02dnZ5sEHHzQ33nijWbhwobnkkktMx44dz/piePToUTN48GDzwAMPWG2nTp0yN954o/nLX/7id53Dhw+bSy65xOtTm9zcXHPllVeahQsXmrffftscPHjQ77qeQXz77bebmTNnmmXLlpnQ0FBrW/PmzTP79u3zWic1NdXUrl3bXHHFFVbbfffdZ3r16mUuvPBCc+2111oviEUfl5MnT5qLL77YfPLJJ8YYY/r37286duxoatSoYZo1a2aeffZZk5qa6rXOL7/8YhwOh9cTcu7cuSYiIsKsXbvWb14eX331lenatavXAfe6664zzzzzjBk9erT58ssvffb3ySefmH79+pljx45Z/bR48WITHh5u2rZta+bNm+c3t6+//tq0a9fOJCcnW215eXlm0KBBplGjRmb16tXGGO8DR1ZWlrntttvMTTfdZGbPnm0uueQSM3jw4LMWYhkZGWbAgAHWC5hnWz169DDx8fEBH4+0tDTTvXt3r7Fy+PBh069fP7N06VKzZMmSgLM/nnyvueYa8/LLL5vXX3/dOBwOM3PmTOsxKvwG4cCBA8bhcJibbrrJahszZozp37+/ueyyy7xeRIseTDMzM03nzp3N8uXLjTHGDBo0yMTGxpoaNWqYli1bmvfff9/nk7StW7cah8NhHnvsMatt4sSJpm3btuaXX34J+JgYY8zChQvNpZdeajIzM622q666yrz22mvm6aefNj/++KPfmYd58+aZP//5z15vIF566SXjcDhM8+bNzddff+03v5IeU+w8nhhTuY8pdh9PjDn3Y8rv/bXHmHMfK7/3cWJMxRkrp0+fNn379vV6s2uMMYcOHTL333+/CQ8Pt15/CktISDADBgwwSUlJZv78+aZr165nLcTy8vLMSy+9ZIYOHWoOHjxoxZiSkmKaNWtmNm7c6HeduXPnmjvvvNNkZGRYsY8ePdpceeWVpm/fvub22283K1euDLjfffv2mVtvvdWkp6ebmTNnmo4dO5r4+HgzcuRIM3fuXKsYNKZgbE2ePNk4HA7rTIgrr7zSdOrUydSuXdu0bt3a9O/f3/z4449+9/XCCy+YwYMHG2OM6dWrlzULc+ONNxqHw2HefPNNY8yZPjh8+LDp3r271+OflpZmunTpUuxzx5iC513Hjh3NK6+8YrU99thjplmzZqZTp06mRYsW5u233/baX3p6umnXrp35+OOPvdpvvPFG069fP1OlShWzZs0av/u74YYbzF133eXTPnXqVONwOMwXX3zhtU1jjPn+++9N//79zcqVK82///3voAoxt9tt3nnnHTNkyBCze/du6/l+6tQp06pVK2s22Z+FCxea4cOHez0/4uPjTceOHU2PHj1Mnz59rA9I/X1gnJ2dbW688UZz4MABs2jRIhMTE2Ouv/56M3LkSOvDlMLmzp1rHA6H+fzzz01+fr7p27evufjii02zZs1Mhw4dTOvWrc2qVasCxns2FGHnafny5SYiIsI6JapwB956662mUaNGfg/8//jHP8z7779vjDHm22+/DerFMDU11YwcOdJazzNw33jjDdO3b1/jdru9Djae/b344oteT4gpU6aYKlWqmIsvvti0adPGREVFWQe4wjF6/v/+++9bB5DPP//cVKlSxTrFwN/pdDfddJPp2rWrmTdvnunZs6eJi4szM2fONHPmzDEdOnQwF110kfUmufD+Tp06Za666irz6aefmscff9wMGDDA/PTTTyY7O9tMmDDBxMbGmrfeessr9zVr1lif0Hj8+OOPpl27dubFF18M+FgaY8yCBQtMzZo1rReGF1980YSGhprbb7/d9O7d28TExJjnn3/ea/3nn3/eREdHe23nP//5j7nzzjvNn//8Z9OwYUO/U+kffvihqVOnjlXEFJ6x6d+/v7nooov8HjCmTp1q3n33XZOXl2fefffdoAqx7du3m9tuu806YHqWmTJlivVpaOH1PPs9duyYmTp1qvn++++t+55++mkT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",
      "text/plain": [
       "<Figure size 1000x900 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "import matplotlib.pyplot as plt\n",
    "\n",
    "\n",
    "plt.figure(figsize=(10, 9))\n",
    "profit_by_year.plot(kind='bar', color='skyblue')\n",
    "plt.title('Total Profits by Release Year')\n",
    "plt.xlabel('Release Year')\n",
    "plt.ylabel('Total Profit (in billions)')\n",
    "plt.xticks(rotation=45)\n",
    "plt.grid(axis='y', linestyle='--', alpha=0.9)\n",
    "plt.show()\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Research Question 2  (Which Movie got the highest Ratings ?)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 655,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Title</th>\n",
       "      <th>Rating</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>The Story of Film: An Odyssey</td>\n",
       "      <td>9.2</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                           Title  Rating\n",
       "0  The Story of Film: An Odyssey     9.2"
      ]
     },
     "execution_count": 655,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# Find the movie with the highest rating\n",
    "highest_rated_movie = df.loc[df['vote_average'].idxmax()]\n",
    "\n",
    "# Create a DataFrame for the highest rated movie\n",
    "highest_rated_movie_df = pd.DataFrame({\n",
    "    'Title': [highest_rated_movie['original_title']],\n",
    "    'Rating': [highest_rated_movie['vote_average']]\n",
    "})\n",
    "\n",
    "# Display the table\n",
    "highest_rated_movie_df\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Research Question 3 (What are the movies with the highest and the lowest revenues ?)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 656,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Movie with the Highest revenue: Avatar\n",
      "Movie with the Lowest revenue: Wild Card\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>1386</th>\n",
       "      <th>48</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>id</th>\n",
       "      <td>19995</td>\n",
       "      <td>265208</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>popularity</th>\n",
       "      <td>9.432768</td>\n",
       "      <td>2.93234</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>budget</th>\n",
       "      <td>237000000</td>\n",
       "      <td>30000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>revenue</th>\n",
       "      <td>2781505847</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>original_title</th>\n",
       "      <td>Avatar</td>\n",
       "      <td>Wild Card</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>cast</th>\n",
       "      <td>Sam Worthington|Zoe Saldana|Sigourney Weaver|S...</td>\n",
       "      <td>Jason Statham|Michael Angarano|Milo Ventimigli...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>director</th>\n",
       "      <td>James Cameron</td>\n",
       "      <td>Simon West</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>keywords</th>\n",
       "      <td>culture clash|future|space war|space colony|so...</td>\n",
       "      <td>gambling|bodyguard|remake</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>runtime</th>\n",
       "      <td>162</td>\n",
       "      <td>92</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>genres</th>\n",
       "      <td>Action|Adventure|Fantasy|Science Fiction</td>\n",
       "      <td>Thriller|Crime|Drama</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>production_companies</th>\n",
       "      <td>Ingenious Film Partners|Twentieth Century Fox ...</td>\n",
       "      <td>Current Entertainment|Lionsgate|Sierra / Affin...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>release_date</th>\n",
       "      <td>2009-12-10 00:00:00</td>\n",
       "      <td>2015-01-14 00:00:00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>vote_count</th>\n",
       "      <td>8458</td>\n",
       "      <td>481</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>vote_average</th>\n",
       "      <td>7.1</td>\n",
       "      <td>5.3</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>release_year</th>\n",
       "      <td>2009</td>\n",
       "      <td>2015</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>profit</th>\n",
       "      <td>2544505847</td>\n",
       "      <td>-30000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                                                                   1386  \\\n",
       "id                                                                19995   \n",
       "popularity                                                     9.432768   \n",
       "budget                                                        237000000   \n",
       "revenue                                                      2781505847   \n",
       "original_title                                                   Avatar   \n",
       "cast                  Sam Worthington|Zoe Saldana|Sigourney Weaver|S...   \n",
       "director                                                  James Cameron   \n",
       "keywords              culture clash|future|space war|space colony|so...   \n",
       "runtime                                                             162   \n",
       "genres                         Action|Adventure|Fantasy|Science Fiction   \n",
       "production_companies  Ingenious Film Partners|Twentieth Century Fox ...   \n",
       "release_date                                        2009-12-10 00:00:00   \n",
       "vote_count                                                         8458   \n",
       "vote_average                                                        7.1   \n",
       "release_year                                                       2009   \n",
       "profit                                                       2544505847   \n",
       "\n",
       "                                                                   48    \n",
       "id                                                               265208  \n",
       "popularity                                                      2.93234  \n",
       "budget                                                         30000000  \n",
       "revenue                                                               0  \n",
       "original_title                                                Wild Card  \n",
       "cast                  Jason Statham|Michael Angarano|Milo Ventimigli...  \n",
       "director                                                     Simon West  \n",
       "keywords                                      gambling|bodyguard|remake  \n",
       "runtime                                                              92  \n",
       "genres                                             Thriller|Crime|Drama  \n",
       "production_companies  Current Entertainment|Lionsgate|Sierra / Affin...  \n",
       "release_date                                        2015-01-14 00:00:00  \n",
       "vote_count                                                          481  \n",
       "vote_average                                                        5.3  \n",
       "release_year                                                       2015  \n",
       "profit                                                        -30000000  "
      ]
     },
     "execution_count": 656,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "def find_minmax(x):\n",
    "    min_index = df[x].idxmin()\n",
    "    max_index = df[x].idxmax()\n",
    "    \n",
    "    # Create DataFrames for the movies with highest and lowest revenue\n",
    "    highest_revenue_movie = pd.DataFrame(df.loc[max_index, :])\n",
    "    lowest_revenue_movie = pd.DataFrame(df.loc[min_index, :])\n",
    "    \n",
    "    # Print the movies with high and low revenue\n",
    "    print(\"Movie with the Highest \" + x + \":\", df['original_title'][max_index])\n",
    "    print(\"Movie with the Lowest \" + x + \":\", df['original_title'][min_index])\n",
    "    \n",
    "    revenue_movies_df = pd.concat([highest_revenue_movie, lowest_revenue_movie], axis=1)\n",
    "    return revenue_movies_df\n",
    "\n",
    "find_minmax('revenue')\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Research Question 4 (Do movies with higher budgets receive higher ratings?)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 657,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Correlation coefficient between budget and ratings: 0.08106672575599058\n"
     ]
    }
   ],
   "source": [
    "# Calculate the correlation coefficient between budget and ratings\n",
    "correlation = df['budget'].corr(df['vote_average'])\n",
    "\n",
    "# Print the correlation coefficient\n",
    "print(\"Correlation coefficient between budget and ratings:\", correlation)\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 658,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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MUPV1dVyuVwOVnhu4JmgU+T1etWtWzetXLkyts+yLK1cuZIxxQBwDNu2NXbsWC1evFgffvih2rVr53RJQC2WZam6utrpMpDErrzySm3atElFRUWxj+7du2v48OEqKioiAJ0m9ASdBuPGjdPIkSPVvXt39ezZU88995zKy8t1yy23OF0aklRZWZm++eab2Pa2bdtUVFSkZs2aqXXr1g5WhmQ2ZswYLViwQO+9957S09O1e/duSVIgEFBKSorD1SEZPfDAAxo0aJBat26t0tJSLViwQKtWrdKyZcucLg1JLD09vdazkmlpacrIyOAZytOIEHQaDBs2THv37tXEiRO1e/dudenSRUuXLq01WQJwtmzcuFGXX355bHvcuHGSpJEjR2r+/PkOVYVkN2vWLElSv379auyfN2+eRo0adfYLQtIrLi7WiBEjtGvXLgUCAXXq1EnLli3TgAEDnC4NwBnGOkEAAAAAkgrPBAEAAABIKoQgAAAAAEmFEAQAAAAgqRCCAAAAACQVQhAAAACApEIIAgAAAJBUCEEAAAAAkgohCAAAAMAZt2bNGg0ePFitWrWSYRh69913G/way5YtU+/evZWenq7mzZvrN7/5jb777rsGvw4hCABwQvPnz1eTJk0crWHChAn6/e9/H9vu16+f7r777lN6zfq8Rtu2bfXcc8/Fto/9of3dd9/JMAwVFRVJklatWiXDMHTo0KFTqqu+gsGg2rZtq40bN56V9wOAU1VeXq7OnTtr5syZcX3+tm3bNGTIEF1xxRUqKirSsmXLtG/fPv36179u8GsRggDgHDBq1CgZhhH7yMjI0MCBA/X55587XVqdfhggTmT37t2aPn26/vznP8f2vfPOO3r00UfPYIVRBQUFNcLXiVx88cXatWuXAoHAGa4qyuv1avz48brvvvvOyvsBwKkaNGiQpkyZouuuu67O49XV1Ro/frx+8pOfKC0tTb169dKqVatixwsLCxWJRDRlyhSdd9556tq1q8aPH6+ioiKFQqEG1UIIAoBzxMCBA7Vr1y7t2rVLK1eulNvt1i9/+Uunyzplc+fO1cUXX6w2bdrE9jVr1kzp6eln/L2bN2+u1NTUep3r9XqVnZ0twzDOcFXfGz58uNauXasvv/zyrL0nAJwpY8eO1bp167Rw4UJ9/vnn+u1vf6uBAwdq69atkqRu3brJNE3NmzdPkUhEJSUleuWVV9S/f395PJ4GvRchCADOET6fT9nZ2crOzlaXLl10//33a8eOHdq7d6+kuodrFRUVyTCMGuOp58+fr9atWys1NVXXXXed9u/fX+u9pkyZoqysLKWnp+vWW2/V/fffry5dutQ4Z+7cuTr//PPl9/v1s5/9TC+++GLsWLt27SRJ+fn5MgxD/fr1O+7XtXDhQg0ePLjGvh8OZWvbtq0ef/xx/e53v1N6erpat26tl1566SRXTAqHwxo7dqwCgYAyMzM1YcIE2bZd43WPHQ53InVd37fffls///nP5fP51LZtW02dOrXG55ys7mAwqLFjx6ply5by+/1q06aNnnjiidjxpk2bqm/fvlq4cGG9agSARLV9+3bNmzdPb775pn7xi1/ovPPO0/jx43XJJZdo3rx5kqI/O5YvX64HH3xQPp9PTZo00c6dO/XGG280+P0IQQBwDiorK9Orr76q9u3bKyMjo96f98knn2j06NEaO3asioqKdPnll2vKlCk1znnttdf02GOP6amnnlJhYaFat26tWbNm1Tpn4sSJeuyxx/TVV1/p8ccf14QJE/Tyyy9LkjZs2CBJ+uCDD7Rr1y698847ddZz4MABbd68Wd27dz9p7VOnTlX37t312Wef6fbbb9cf//hHbdmy5YSf8/LLL8vtdmvDhg2aPn26nn32Wc2dO/ek71UfhYWFuuGGG3TjjTdq06ZNmjRpkiZMmKD58+fXu+7nn39ef//73/XGG29oy5Yteu2119S2bdsan9+zZ0999NFHp6VmAHDKpk2bFIlE1LFjRzVq1Cj2sXr1an377beSosOjb7vtNo0cOVIFBQVavXq1vF6vrr/++hq/wKoP95n4IgAAZ9+SJUvUqFEjSdGHT1u2bKklS5bINOv/+67p06dr4MCB+tOf/iRJ6tixo/71r39p6dKlsXNeeOEFjR49WrfccoskaeLEiVq+fLnKyspi5zz88MOaOnVq7GHVdu3aafPmzZo9e7ZGjhyp5s2bS5IyMjKUnZ193Hq2b98u27bVqlWrk9Z+zTXX6Pbbb5ck3XfffZo2bZr++c9/Ki8v77ifk5ubq2nTpskwDOXl5WnTpk2aNm2abrvttpO+38k8++yzuvLKKzVhwgRJ0Wu5efNmPfPMMxo1alS96t6+fbs6dOigSy65RIZh1BgSeFSrVq303//+95TrBQAnlZWVyeVyqbCwUC6Xq8axoz/bZs6cqUAgoKeffjp27NVXX1Vubq4++eQT9e7du97vR08QAJwjLr/8chUVFamoqEgbNmzQ1VdfrUGDBjXoBvmrr75Sr169auzr06dPje0tW7aoZ8+eNfYdu11eXq5vv/1Wo0ePrvHbvClTpsR+m1dflZWVkiS/33/Sczt16hT7u2EYys7OVnFx8Qk/p3fv3jWe4enTp4+2bt2qSCTSoDrr8tVXX6lv37419vXt27fW65+o7lGjRqmoqEh5eXm68847tXz58lrvk5KSooqKilOuFwCclJ+fr0gkouLiYrVv377Gx9FfllVUVNT6xd7RwGRZVoPej54gADhHpKWlqX379rHtuXPnKhAIaM6cOZoyZUrsB8exQwYaOptOfRztEZozZ06tQPXD3+6dTGZmpiTp4MGDsd6j4/nhQ7GGYTT4h6ITTlR3165dtW3bNr3//vv64IMPdMMNN6h///566623YucfOHDgpNcGABJBWVmZvvnmm9j2tm3bVFRUpGbNmqljx44aPny4RowYoalTpyo/P1979+7VypUr1alTJ1177bW69tprNW3aND3yyCO66aabVFpaqgcffFBt2rRRfn5+g2qhJwgAzlGGYcg0zVhvytEb5V27dsXO+eEU1eeff74++eSTGvvWr19fYzsvL08FBQU19h273aJFC7Vq1Ur/+c9/av027+iECF6vV5JO2uNy3nnnqXHjxtq8efPJvty41PW1dujQocFhrS7nn3++Pv744xr7Pv74Y3Xs2LFBr9+4cWMNGzZMc+bM0aJFi/T222/rwIEDseNffPFFg3/4A4ATNm7cqPz8/Nj/WePGjVN+fr4mTpwoSZo3b55GjBihe++9V3l5eRo6dKgKCgrUunVrSdIVV1yhBQsW6N1331V+fr4GDhwon8+npUuXKiUlpUG10BMEAOeI6upq7d69W1K052TGjBkqKyuLzazWvn175ebmatKkSXrsscf073//u9ZsZXfeeaf69u2rv/zlLxoyZIiWLVtW43kgSbrjjjt02223qXv37rr44ou1aNEiff755/rpT38aO2fy5Mm68847FQgENHDgQFVXV2vjxo06ePCgxo0bp6ysLKWkpGjp0qXKycmR3++vc30d0zTVv39/rV27VkOHDj3NVyz6zNG4ceP0hz/8QZ9++qleeOGFWtckXvfee6969OihRx99VMOGDdO6des0Y8aMGrPkncyzzz6rli1bKj8/X6Zp6s0331R2dnaNxWs/+uijs7JmEgCcqn79+p1wAgOPx6PJkydr8uTJxz3nxhtv1I033njKtdATBADniKVLl6ply5Zq2bKlevXqpYKCAr355pux6ac9Ho9ef/11ff311+rUqZOeeuqpWjO/9e7dW3PmzNH06dPVuXNnLV++XA899FCNc4YPH64HHnhA48ePjw3XGjVqVI3ndm699VbNnTtX8+bN00UXXaTLLrtM8+fPj/UEud1uPf/885o9e7ZatWqlIUOGHPfruvXWW7Vw4cIzMrRtxIgRqqysVM+ePTVmzBjddddd9V4c9WS6du2qN954QwsXLtSFF16oiRMn6pFHHqkxKcLJpKen6+mnn1b37t3Vo0cPfffdd/rHP/4RG9q4bt06lZSU6Prrrz8tNQNAsjDshs4nBwDADwwYMEDZ2dl65ZVXTvtr27atXr166Z577tFNN9102l//x2zYsGHq3LmzHnzwQadLAYAfFYbDAQAapKKiQn/961919dVXy+Vy6fXXX9cHH3ygFStWnJH3MwxDL730kjZt2nRGXv/HKhgM6qKLLtI999zjdCkA8KNDTxAAoEEqKys1ePBgffbZZ6qqqlJeXp4eeuih2JpAAAAkOkIQAAAAgKTCxAgAAAAAkgohCAAAAEBSIQQBAAAASCqEIAAAAABJhRAEAAAAIKkQggAAAAAkFUIQAAAAgKRCCAIAAACQVP4fl7rwlah/nt0AAAAASUVORK5CYII=",
      "text/plain": [
       "<Figure size 1000x600 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "import matplotlib.pyplot as plt\n",
    "\n",
    "# Plotting budget vs. ratings\n",
    "plt.figure(figsize=(10, 6))\n",
    "plt.scatter(df['budget'], df['vote_average'], color='skyblue', alpha=0.5)\n",
    "plt.title('Budget vs. Ratings')\n",
    "plt.xlabel('Budget (in billions)')\n",
    "plt.ylabel('Rating')\n",
    "plt.grid(True)\n",
    "plt.show()\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Research Question 5 (Movie with highest and lowest budget?)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 659,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Movie with the Highest budget: The Warrior's Way\n",
      "Movie with the Lowest budget: Mr. Holmes\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>2244</th>\n",
       "      <th>30</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>id</th>\n",
       "      <td>46528</td>\n",
       "      <td>280996</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>popularity</th>\n",
       "      <td>0.25054</td>\n",
       "      <td>3.927333</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>budget</th>\n",
       "      <td>425000000</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>revenue</th>\n",
       "      <td>11087569</td>\n",
       "      <td>29355203</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>original_title</th>\n",
       "      <td>The Warrior's Way</td>\n",
       "      <td>Mr. Holmes</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>cast</th>\n",
       "      <td>Kate Bosworth|Jang Dong-gun|Geoffrey Rush|Dann...</td>\n",
       "      <td>Ian McKellen|Milo Parker|Laura Linney|Hattie M...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>director</th>\n",
       "      <td>Sngmoo Lee</td>\n",
       "      <td>Bill Condon</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>keywords</th>\n",
       "      <td>assassin|small town|revenge|deception|super speed</td>\n",
       "      <td>london|detective|sherlock holmes</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>runtime</th>\n",
       "      <td>100</td>\n",
       "      <td>103</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>genres</th>\n",
       "      <td>Adventure|Fantasy|Action|Western|Thriller</td>\n",
       "      <td>Mystery|Drama</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>production_companies</th>\n",
       "      <td>Boram Entertainment Inc.</td>\n",
       "      <td>BBC Films|See-Saw Films|FilmNation Entertainme...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>release_date</th>\n",
       "      <td>2010-12-02 00:00:00</td>\n",
       "      <td>2015-06-19 00:00:00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>vote_count</th>\n",
       "      <td>74</td>\n",
       "      <td>425</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>vote_average</th>\n",
       "      <td>6.4</td>\n",
       "      <td>6.4</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>release_year</th>\n",
       "      <td>2010</td>\n",
       "      <td>2015</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>profit</th>\n",
       "      <td>-413912431</td>\n",
       "      <td>29355203</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                                                                   2244  \\\n",
       "id                                                                46528   \n",
       "popularity                                                      0.25054   \n",
       "budget                                                        425000000   \n",
       "revenue                                                        11087569   \n",
       "original_title                                        The Warrior's Way   \n",
       "cast                  Kate Bosworth|Jang Dong-gun|Geoffrey Rush|Dann...   \n",
       "director                                                     Sngmoo Lee   \n",
       "keywords              assassin|small town|revenge|deception|super speed   \n",
       "runtime                                                             100   \n",
       "genres                        Adventure|Fantasy|Action|Western|Thriller   \n",
       "production_companies                           Boram Entertainment Inc.   \n",
       "release_date                                        2010-12-02 00:00:00   \n",
       "vote_count                                                           74   \n",
       "vote_average                                                        6.4   \n",
       "release_year                                                       2010   \n",
       "profit                                                       -413912431   \n",
       "\n",
       "                                                                   30    \n",
       "id                                                               280996  \n",
       "popularity                                                     3.927333  \n",
       "budget                                                                0  \n",
       "revenue                                                        29355203  \n",
       "original_title                                               Mr. Holmes  \n",
       "cast                  Ian McKellen|Milo Parker|Laura Linney|Hattie M...  \n",
       "director                                                    Bill Condon  \n",
       "keywords                               london|detective|sherlock holmes  \n",
       "runtime                                                             103  \n",
       "genres                                                    Mystery|Drama  \n",
       "production_companies  BBC Films|See-Saw Films|FilmNation Entertainme...  \n",
       "release_date                                        2015-06-19 00:00:00  \n",
       "vote_count                                                          425  \n",
       "vote_average                                                        6.4  \n",
       "release_year                                                       2015  \n",
       "profit                                                         29355203  "
      ]
     },
     "execution_count": 659,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "find_minmax('budget')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 660,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAABGcAAAIjCAYAAACuznYoAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjYuMywgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy/P9b71AAAACXBIWXMAAA9hAAAPYQGoP6dpAACtvklEQVR4nOzdd3xO9///8edFZC97RmIkxB6hRDUoTWxqVWOPFlWlRqlaJVIlVn2MGgmqqJpFrXwkJa0aJRSNUcSn1WqNRIwIuX5/+OV8XZKQGL1afdxvt+t2c53zPu/zOudKeuv1zPv9Piaz2WwWAAAAAAAArCKHtQsAAAAAAAD4NyOcAQAAAAAAsCLCGQAAAAAAACsinAEAAAAAALAiwhkAAAAAAAArIpwBAAAAAACwIsIZAAAAAAAAKyKcAQAAAAAAsCLCGQAAAAAAACsinAEAAIDVRUVFyWQyKSoq6rGP/fLLL59+Yf9QZ8+elclkUkREhLVL+Vvq1q2bvLy8rF0GABgIZwAAAJ4xk8mUpdfjBBPZNWfOHLVr107FixeXyWRSt27dMm179epVvfHGG8qfP7+cnJxUv359/fDDD1k6T7169VShQoUM96UFB1OmTHmcS/jb+PzzzzV9+vQst/fy8rL4vO3t7eXt7a2hQ4fq8uXLz67QZ2j27NnZCoDSrr1Xr14Z7h85cqTR5s8//3xKVQLA35+NtQsAAAB43i1dutTi/ZIlS7R9+/Z02319fZ95LZMmTdK1a9dUs2ZNXbhwIdN2qampatq0qWJjYzV06FDly5dPs2fPVr169XTgwAF5e3s/1bpeeukl3bx5U7a2tk+132fp888/148//qiBAwdm+ZgqVapo8ODBkqRbt27pwIEDmj59uqKjo7V3795nVOmzM3v2bOXLl++hId+D7O3ttXr1as2ePTvd5718+XLZ29vr1q1bT7lSS/Pnz1dqauozPQcAZAfhDAAAwDPWqVMni/d79uzR9u3b023/K0RHRxujZpydnTNt9+WXX+rbb7/VqlWr1LZtW0lS+/bt5ePjozFjxujzzz9/qnXlyJFD9vb2T7XPv6OiRYtafO69evWSs7OzpkyZopMnTz710OvvKCgoSBs2bNDXX3+tli1bGtu//fZbnTlzRm3atNHq1aufaQ25cuV6pv0DQHYxrQkAAOBv4Pr16xo8eLA8PDxkZ2enMmXKaMqUKTKbzRbtTCaT+vfvr2XLlqlMmTKyt7dX9erV9c0332TpPJ6enjKZTI9s9+WXX6pgwYJ69dVXjW358+dX+/bttX79eiUnJ2fvAh8hszVn/vOf/6hkyZJycHBQzZo1tWvXLtWrV0/16tVL10dqaqpCQkJUrFgx2dvb6+WXX9apU6fStfv+++8VFBQkNzc3OTo6KiAgQDExMRZtrl27poEDB8rLy0t2dnYqUKCAGjVqZEzrqlevnjZt2qRz584Z03Aedw2TQoUKSZJsbP7v76aZXWNGa6VcvXpV3bp1k5ubm9zd3dW1a1ddvXo1w3OtWrVK5cqVk729vSpUqKC1a9dm2GdqaqqmT5+u8uXLy97eXgULFtSbb76pK1euGG28vLx09OhRRUdHG/cgo5ofVLRoUb300kvpAr5ly5apYsWKmU6HW7VqlapXry4HBwfly5dPnTp10i+//GLsnzJlikwmk86dO5fu2BEjRsjW1tao/3GvWZL279+vwMBA5cuXTw4ODipRooR69OjxyOsGgIdh5AwAAICVmc1mtWjRQjt37lTPnj1VpUoVbd26VUOHDtUvv/yiadOmWbSPjo7WypUrNWDAANnZ2Wn27NkKCgrS3r17M/1im10HDx5UtWrVlCOH5d/yatasqU8//VQnTpxQxYoVH9rH3bt3M1w35MEvu5mZM2eO+vfvr7p162rQoEE6e/asWrVqpdy5c6tYsWLp2n/00UfKkSOHhgwZooSEBH388ccKDg7W999/b7T573//q8aNG6t69eoaM2aMcuTIofDwcDVo0EC7du1SzZo1JUl9+vTRl19+qf79+6tcuXK6dOmSdu/erePHj6tatWoaOXKkEhIS9L///c/4fB42EilNSkqKcU9u3bqlgwcPaurUqXrppZdUokSJLN2X+5nNZrVs2VK7d+9Wnz595Ovrq7Vr16pr167p2m7atEkdOnRQxYoVFRoaqitXrqhnz54qWrRourZvvvmmIiIi1L17dw0YMEBnzpzRrFmzdPDgQcXExChXrlyaPn263n77bTk7O2vkyJGSpIIFC2ap7tdff13vvPOOkpKS5OzsrDt37mjVqlV69913M5zSlFZLjRo1FBoaqt9//10zZsxQTEyMDh48KHd3d7Vv317Dhg3TF198oaFDh1oc/8UXX+iVV15R7ty5M60pK9d88eJFvfLK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p7V48WKFhoaqfPnyVh2L4gwAAMADztHRUV5eXvLy8tKjjz6qqKgoHT16VP/9738lSQkJCTKZTDp16pT5NSkpKTKZTBbXzcfGxqpWrVpycXHRc889pz///LPYsaZNm6Zq1arJzc1NAwYMUFRUlMXlMNKVokpAQICcnJzUoEEDffjhh+Z9derUkSQFBgbKZDKpXbt21z2v+Ph4de7c2WJbSZfXvPnmm+rXr5/c3NxUq1Yt/etf/7phvm72S6phGJo9e7YmTJigLl26qEmTJvr000/122+/mWfZpKWlaf369Vq0aJGCg4P1+OOPa86cOYqPj9dvv/0mSfr111/VuXNnVapUSa6urmrUqJHWrl173bhOnjyp3r17q1KlSnJxcVGHDh3MXxASEhLMxZinnnpKJpPJ4tfdq5lMJi1YsEDPPvusXFxcFBAQoB07duinn35Su3bt5OrqqlatWikjI8P8mmsva7qZay9rysrKUpcuXVShQgW5u7ure/fu+v3334v1v3jxYvn6+srDw0M9evTQ2bNnzW2+/PJLNW7cWM7OzvL09FRoaKjy8vLM+zt37qz4+PhSxwgAN5KVlaWYmBgtX75cbdq00cMPP6zIyEg9/vjjiomJkXTlb9a3336r//f//p8cHR1VsWJFHTt2TF988YXVx6M4AwAA8BeSm5urJUuWqF69elbNhNi1a5f69++v4cOHKyUlRU8++aSmTZtm0Wbp0qWaPn263n77bSUnJ6tWrVrFZjIsXbpUkyZN0vTp05WWlqY333xTEydOVFxcnCRp9+7dkqRNmzYpOztbK1asKDGeEydO6NChQwoKCrpp7DNnzlRQUJD27dunoUOH6h//+IfS09NLfe7XyszM1PHjxxUaGmre5uHhoeDgYO3YsUOStGPHDlWsWNEivtDQUJUrV067du2SJA0bNkz5+fnatm2bUlNT9fbbb6tChQrXPW7fvn21Z88effPNN9qxY4cMw1DHjh116dIltWrVynxOX331lbKzs9WqVavr9jV16lT17t1bKSkpatCggf7+979r8ODBGj9+vPbs2SPDMDR8+PBbztHVCgsL1aVLF504cUJbt27Vxo0b9fPPP+vFF1+0aJeRkaGVK1dq9erVWr16tbZu3aq33npLkpSdna2ePXuqX79+SktLU0JCgrp16ybDMMyvb9mypY4dO3ZLC3ECwLVS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",
      "text/plain": [
       "<Figure size 1000x600 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "import seaborn as sns\n",
    "import matplotlib.pyplot as plt\n",
    "\n",
    "# Sort the 'budget' column in descending order and store it in a new dataframe\n",
    "info = pd.DataFrame(df['budget'].sort_values(ascending=False))\n",
    "info['original_title'] = df['original_title']\n",
    "\n",
    "# Extract the top 10 budget movies data from the dataframe\n",
    "top_10_budget_movies = info.head(10)\n",
    "\n",
    "# Plot the figure\n",
    "plt.figure(figsize=(10, 6))\n",
    "ax = sns.barplot(x='budget', y='original_title', data=top_10_budget_movies, palette='viridis')\n",
    "ax.set_title(\"Top 10 Highest Budget Movies\")\n",
    "ax.set_xlabel(\"Budget (in 100s of millions)\")\n",
    "ax.set_ylabel(\"Movie Title\")\n",
    "plt.show()\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Research Question 6 (Which year has the highest and lowest release of movies ?)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 661,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Number of movie releases by year:\n",
      "2014    700\n",
      "2013    659\n",
      "2015    629\n",
      "2012    588\n",
      "2011    540\n",
      "2009    533\n",
      "2008    496\n",
      "2010    489\n",
      "2007    438\n",
      "2006    408\n",
      "2005    364\n",
      "2004    307\n",
      "2003    281\n",
      "2002    266\n",
      "2001    242\n",
      "2000    227\n",
      "1999    224\n",
      "1998    210\n",
      "1996    204\n",
      "1997    192\n",
      "1994    184\n",
      "1993    178\n",
      "1995    175\n",
      "1988    145\n",
      "1989    137\n",
      "1991    133\n",
      "1992    133\n",
      "1990    132\n",
      "1987    125\n",
      "1986    121\n",
      "1985    109\n",
      "1984    105\n",
      "1981     82\n",
      "1982     81\n",
      "1983     80\n",
      "1980     78\n",
      "1978     65\n",
      "1977     57\n",
      "1979     57\n",
      "1973     55\n",
      "1971     55\n",
      "1976     47\n",
      "1974     47\n",
      "1966     46\n",
      "1975     44\n",
      "1964     42\n",
      "1970     41\n",
      "1967     40\n",
      "1972     40\n",
      "1968     39\n",
      "1965     35\n",
      "1963     34\n",
      "1960     32\n",
      "1962     32\n",
      "1961     31\n",
      "1969     31\n",
      "Name: release_year, dtype: int64\n"
     ]
    }
   ],
   "source": [
    "# Count the number of movie releases for each year\n",
    "movie_counts_by_year = df['release_year'].value_counts()\n",
    "\n",
    "# Display the number of movie releases for each year\n",
    "print(\"Number of movie releases by year:\")\n",
    "print(movie_counts_by_year)\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 662,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "\n",
      "Year with the highest number of movie releases: 2014\n",
      "Number of movie releases in the highest year: 700\n",
      "\n",
      "Year with the lowest number of movie releases: 1961\n",
      "Number of movie releases in the lowest year: 31\n"
     ]
    }
   ],
   "source": [
    "# Find the year with the highest number of movie releases\n",
    "year_highest_release = movie_counts_by_year.idxmax()\n",
    "highest_release_count = movie_counts_by_year.max()\n",
    "\n",
    "# Find the year with the lowest number of movie releases\n",
    "year_lowest_release = movie_counts_by_year.idxmin()\n",
    "lowest_release_count = movie_counts_by_year.min()\n",
    "\n",
    "# Display the year with the highest and lowest number of movie releases\n",
    "print(\"\\nYear with the highest number of movie releases:\", year_highest_release)\n",
    "print(\"Number of movie releases in the highest year:\", highest_release_count)\n",
    "print(\"\\nYear with the lowest number of movie releases:\", year_lowest_release)\n",
    "print(\"Number of movie releases in the lowest year:\", lowest_release_count)\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 663,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAABKQAAAJOCAYAAACJLN8OAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjYuMywgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy/P9b71AAAACXBIWXMAAA9hAAAPYQGoP6dpAADGHUlEQVR4nOzde5yM5f/H8fc9u/Zgj3btAeucWuSssilUtOTbiVISklIiOUYn0sHpm0pF5+igkk6/QnKITlRWDokQyyYW67CbZXftzv37Q3N/d8zM7ozWrNbr+Xh4PMw119zzec99zabPXnOPYZqmKQAAAAAAAMBPbOVdAAAAAAAAAM4uNKQAAAAAAADgVzSkAAAAAAAA4Fc0pAAAAAAAAOBXNKQAAAAAAADgVzSkAAAAAAAA4Fc0pAAAAAAAAOBXNKQAAAAAAADgVzSkAAAAAAAA4Fc0pAAAOIstX75chmHoww8/LO9SvLJ3717dcMMNio2NlWEYevbZZ8u7pFLddtttqlOnTnmXUaJZs2bJMAzt2LGjvEs5rR599FEZhqGsrKzyLgUAgLMeDSkAAE4zx//sh4SE6M8//3S5v0OHDjr//PPLobJ/n2HDhunLL7/UAw88oLfffludO3f2ONcwDBmGoTvuuMPt/Q899JA159/UoHA0VRx/KlWqpDp16mjIkCE6fPhweZd3VktPT1flypXVs2dPt/fPmTNHhmFo+vTpfq4MAIAzDw0pAAD8JD8/X5MmTSrvMv7VvvrqK1177bUaOXKkbr31ViUnJ5c4PyQkRB999JEKCgpc7nvvvfcUEhJyukq1vPrqq9q8eXOZH/fFF1/U22+/rRdeeEEXXnihnn/+ef3nP/8p8+eB9+rWratx48bp/fff16JFi5zuy8nJ0bBhw3TRRRdp4MCB5VQhAABnDhpSAAD4SfPmzfXqq69q9+7d5V2K3+Xm5pbJcfbt26fo6Giv53fu3Fk5OTn64osvnMZXrFih9PR0de3atUzqKkmlSpUUHBxc5se94YYbdOutt+quu+7SBx98oJtuuknff/+9fvrppzJ/LnhvxIgRatKkie655x4dO3bMGn/ooYe0f/9+vfLKK7LZTv8/wcvqPQcAwOlCQwoAAD958MEHVVRUVOouqR07dsgwDM2aNcvlPsMw9Oijj1q3HR/f2rJli2699VZFRUUpLi5OjzzyiEzT1B9//KFrr71WkZGRSkxM1NSpU90+Z1FRkR588EElJiYqLCxM11xzjf744w+XeT/++KM6d+6sqKgoVa5cWe3bt9f333/vNMdR08aNG3XLLbeoSpUquuSSS0rMvH37dt14442KiYlR5cqV1aZNG82fP9+63/GxR9M0NX36dOvjaqWpUaOG2rVrp3fffddpfPbs2WrSpInHj0rOnTtXrVq1UmhoqKpWrapbb73V6eOWTz31lAzD0M6dO10e+8ADDygoKEiHDh2S5P4aUna7Xc8++6waN26skJAQJSQk6K677rIecyouvfRSSdK2bducxr05Z5588cUXuvTSSxUWFqaIiAh17dpVv/76q9Oc9evX67bbblO9evUUEhKixMRE3X777Tpw4IDTvL/++ktDhw5VnTp1FBwcrPj4eHXq1Ek///yzz/V6eyxPsrKy1KNHD0VGRio2Nlb33Xef8vLyrPvbt2+vZs2auX3seeedp9TUVI/HDgwM1CuvvKL09HQ98cQTkqTVq1drxowZGjFihJo2bSpJeuedd6w1FhMTo5tvvtnlPfftt9/qxhtvVK1atRQcHKyaNWtq2LBhTo0u6cQaCw8P17Zt23TVVVcpIiJCvXr18uq1AACgvNCQAgDAT+rWras+ffqcll1SN910k+x2uyZNmqSLLrpITzzxhJ599ll16tRJNWrU0OTJk3XOOedo5MiR+uabb1we/+STT2r+/PkaPXq0hgwZosWLF6tjx45O/+P71VdfqV27dsrJydG4ceM0YcIEHT58WJdffrnbXTk33nijjh49qgkTJujOO+/0WPvevXt18cUX68svv9Q999yjJ598Unl5ebrmmmv0ySefSJLatWunt99+W5LUqVMnvf3229bt0txyyy36/PPPdeTIEUlSYWGh5s6dq1tuucXt/FmzZqlHjx4KCAjQxIkTdeedd+rjjz/WJZdcYl2jqUePHjIMQx988IHL4z/44ANdeeWVqlKlisea7rrrLo0aNUpt27bVtGnT1K9fP82ePVupqak6fvy4V7lO5rggefHn9fWcFff222+ra9euCg8P1+TJk/XII49o48aNuuSSS5wufr548WJt375d/fr10/PPP6+bb75Z77//vq666iqZpmnNu/vuu/Xiiy+qe/fumjFjhkaOHKnQ0FBt2rTJ53q9OVZJevTooby8PE2cOFFXXXWVnnvuOQ0YMMC6v3fv3lq/fr02bNjg9LhVq1ZZzd+StGnTRgMHDtR///tf/fLLL7rrrrtUp04djRs3TtKJ91ufPn3UoEEDPf300xo6dKiWLl2qdu3aOV0HbO7cuTp69KgGDhyo559/XqmpqXr++efVp08fl+csLCxUamqq4uPj9dRTT6l79+5evRYAAJQbEwAAnFYzZ840JZmrVq0yt23bZgYGBppDhgyx7m/fvr3ZuHFj63Z6eropyZw5c6bLsSSZ48aNs26PGzfOlGQOGDDAGissLDSTkpJMwzDMSZMmWeOHDh0yQ0NDzb59+1pjy5YtMyWZNWrUMHNycqzxDz74wJRkTps2zTRN07Tb7WaDBg3M1NRU0263W/OOHj1q1q1b1+zUqZNLTT179vTq9Rk6dKgpyfz222+tsb/++susW7euWadOHbOoqMgp/6BBg7w6rmPuwYMHzaCgIPPtt982TdM058+fbxqGYe7YscOqdf/+/aZpmmZBQYEZHx9vnn/++eaxY8esY82bN8+UZI4dO9YaS0lJMVu1auX0nD/99JMpyXzrrbessb59+5q1a9e2bn/77bemJHP27NlOj124cKHb8ZM5at68ebO5f/9+c8eOHeYbb7xhhoaGmnFxcWZubq5pmr6dM8caTU9PN03zxOsfHR1t3nnnnU7PnZmZaUZFRTmNHz161KXG9957z5RkfvPNN9ZYVFRUiefOl3pLO5YnjtfummuucRq/5557TEnmunXrTNM0zcOHD5shISHm6NGjneYNGTLEDAsLM48cOVLqc2VnZ5vVq1c3Y2JiTEnmwoULTdM0zR07dpgBAQHmk08+6TT/l19+MQMDA53G3b22EydONA3DMHfu3GmN9e3b15RkjhkzptS6AAA4U7BDCgAAP6pXr5569+6tV155RXv27Cmz4xb/JrmAgAC1bt1apmmqf//+1nh0dLTOO+88bd++3eXxffr0UUREhHX7hhtuULVq1bRgwQJJ0tq1a7V161bdcsstOnDggLKyspSVlaXc3FxdccUV+uabb2S3252Oeffdd3tV+4IFC3ThhRc6fawvPDxcAwYM0I4dO7Rx40bvXgQPqlSpos6dO+u9996TJL377ru6+OKLVbt2bZe5aWlp2rdvn+655x6nC5537dpVycnJTh8jvOmmm7R69Wqnj8jNmTNHwcHBuvbaaz3WM3fuXEVFRalTp07W65iVlaVWrVopPDxcy5Yt8yrXeeedp7i4ONWpU0e33367zjnnHH3xxReqXLmypFM7Zw6LFy/W4cOH1bNnT6caAwICdNFFFznVGBoaav09Ly9PWVlZatOmjSQ5fYQuOjpaP/74o8fdgb7UW9qxSjNo0CCn2/fee68kWes9KipK1157rd577z1rl1dRUZHmzJmj6667TmFhYaU+R2RkpJ599lkdPHhQN910k/Uxv48//lh2u109evRwem0TExPVoEEDj69tbm6usrKydPHFF8s0Ta1Zs8blOblYOgDg3ySwvAsAAOBs8/DDD+vtt9/WpEmTNG3atDI5Zq1atZxuR0VFKSQkRFWrVnUZP/naPpLUoEEDp9uGYeicc86xPpq1detWSVLfvn091pCdne30cbG6det6VfvOnTt10UUXuYw3bNjQut/TtZ68dcstt6h3797KyMjQp59+qilTpnisRTrR7DlZcnKyvvvuO+v2jTfeqOHDh2vOnDl68MEHZZqm5s6dqy5duigyMtJjLVu3blV2drbi4+Pd3r9v3z6vMn300UeKjIzU/v379dxzzyk9Pd2pgXEq5+zkx15++eVuH1c838GDBzV+/Hi9//77LrVnZ2dbf58yZYr69u2rmjVrqlWrVrrqqqvUp08f1atXz+d6SztWaU5e7/Xr15fNZnP6KGKfPn00Z84cffvtt2rXrp2WLFmivXv3qnfv3l49hyRdcMEFkqTWrVtbY1u3bpVpmi41OFSqVMn6e0ZGhsaOHavPPvvM5fpixV9b6cS1q5KSkryuDQCA8kZDCgAAP6tXr55uvfVWvfLKKxozZozL/Z4u1l1UVOTxmAEBAV6NSXK6ro+3HDtT/vvf/6p58+Zu54SHhzvdLt4cKW/XXHONgoOD1bdvX+Xn56tHjx7/+JjVq1fXpZdeqg8++EAPPvigfvjhB2VkZGjy5MklPs5utys+Pl6zZ892e39cXJxXz9+uXTur4Xj11VerSZMm6tWrl1avXi2bzXZK56x4jdKJ60glJia63B8Y+L9/Qvbo0UMrVqzQqFGj1Lx5c4WHh8tut6tz585OO7B69OihSy+9VJ988okWLVqk//73v5o8ebI+/vhjdenSxad6SzuWr9y951JTU5WQkKB33nlH7dq10zvvvKPExER17NjR5+MXZ7fbZRiGvvjiC7fvUUfGoqIiderUSQcPHtTo0aOVnJyssLAw/fnnn7rttttcdrcFBwf75dv7AAAoKzSkAAAoBw8//LDeeecdt80Lx46V4hc3luT2G93KimN3ioNpmvr999+tbwSrX7++pBM7Y/7p/5CfrHbt2tq8ebPL+G+//Wbd/0+Fhobquuuu0zvvvKMuXbq47BwrXoskbd682WV30ObNm11quemmm3TPPfdo8+bNmjNnjipXrqyrr766xFrq16+vJUuWqG3btmXWtAsPD9e4cePUr18/ffDBB7r55pv/0TlzPDY+Pr7Exx46dEhLly7V+PHjNXbsWGv85PXkUK1aNd1zzz265557tG/fPrVs2VJPPvmkunTp4nO9JR2rNFu3bnXawff777/Lbrc7fRtiQECAbrnlFs2aNUuTJ0/Wp59+qjvvvNNjo9db9evXl2maqlu3rs4991yP83755Rdt2bJFb775ptNFzBcvXvyPnh8AgDMFv0YBAKAc1K9fX7feeqtefvllZWZmOt0XGRmpqlWrunwb3owZM05bPW+99Zb++usv6/aHH36oPXv2WP9z36pVK9WvX19PPfWU9W11xe3fv/+Un/uqq67STz/9pJUrV1pjubm5euWVV1SnTh01atTolI9d3MiRIzVu3Dg98sgjHue0bt1a8fHxeumll5Sfn2+Nf/HFF9q0aZO6du3qNL979+4KCAjQe++9p7lz5+o///lPqdcX6tGjh4qKivT444+73FdYWOjSiPRWr169lJSUZDU5/8k5S01NVWRkpCZMmOD2W/8cj3U0Z07edffss8863S4qKnL5iFl8fLyqV69uvc7e1uvNsUozffp0p9vPP/+8JLk0s3r37q1Dhw7prrvu0pEjR0r9dj1vdOvWTQEBARo/frzL62aapvWRWnevrWmaZfYxXwAAyhs7pAAAKCcPPfSQ3n77bW3evFmNGzd2uu+OO+7QpEmTdMcdd6h169b65ptvtGXLltNWS0xMjC655BL169dPe/fu1bPPPqtzzjlHd955pyTJZrPptddeU5cuXdS4cWP169dPNWrU0J9//qlly5YpMjJSn3/++Sk995gxY/Tee++pS5cuGjJkiGJiYvTmm28qPT1dH330UZl9DKlZs2Zq1qxZiXMqVaqkyZMnq1+/fmrfvr169uypvXv3atq0aapTp46GDRvmND8+Pl6XXXaZnn76af31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nKwZM2aUmGHDhg3q0qWLwsPDlZCQoN69eysrK8u6f+HChbrkkksUHR2t2NhY/ec//9G2bdus+wsKCjR48GBVq1ZNISEhql27tiZOnGjdf/jwYd1xxx2Ki4tTZGSkLr/8cq1bt866f926dbrssssUERGhyMhItWrVSmlpaV6fg7JGQwoAAAAAgL/lFuR6/JNXmOf13GPHj3k1119mz56tJ598UpMnT9bq1atVq1Ytvfjiiy7zli1bpm3btmnZsmXWDqJZs2ZZ9w8ePFgrV67U+++/r/Xr1+vGG29U586dtXXrVknSoEGDlJ+fr2+++Ua//PKLJk+erPDwcNWsWVMfffSRJGnz5s3as2ePpk2bJulE88yXb3UrKCjQO++8o9tvv9163OrVq3X8+HF17NjRmpecnKxatWpp5cqVkqSVK1eqSZMmSkhIsOakpqYqJydHv/76a4nPOWbMGN13333atGmTUlNTNXv2bI0dO1ZPPvmkNm3apAkTJuiRRx7Rm2++6fbxhw8f1uWXX64WLVooLS1NCxcu1N69e9WjRw9rTm5uroYPH660tDQtXbpUNptN119/vex2uyTpueee02effaYPPvhAmzdv1uzZs1WnTh3r8TfeeKP27dunL774QqtXr1bLli11xRVX6ODBg5KkXr16KSkpSatWrdLq1as1ZswYVapUyevXvawFltszAwAAAABwhgmfGO7xvqsaXKX5t8y3bsc/Fa+jx4+6ndu+dnstv225dbvOtDrKOprlMs8cZ/pc47x58xQe7lxnUVFRiY95/vnn1b9/f/Xr10+SNHbsWC1atEhHjhxxmlelShW98MILCggIUHJysrp27aqlS5fqzjvvVEZGhmbOnKmMjAxVr15dkjRy5EgtXLhQM2fO1IQJE5SRkaHu3burSZMmkqR69epZx46JiZEkxcfHO+3eioqK0nnnned1/k8//VSHDx922mGVmZmpoKAgl11hCQkJyszMtOYUb0Y57nfcV5KhQ4c6ffxv3Lhxmjp1qjVWt25dbdy4US+//LL69u3r8vgXXnhBLVq00IQJE6yxN954QzVr1tSWLVt07rnnqnv37k6PeeONNxQXF6eNGzfq/PPPV0ZGhho0aKBLLrlEhmGodu3a1tzvvvtOP/30k/bt26fg4GBJJ3a6ffrpp/rwww81YMAAZWRkaNSoUUpOTpYkNWjQoMTMp1u57pAq7aJkXJAMAAAAAABnl112mdauXev057XXXivxMZs3b9aFF17oNHbybUlq3LixAgICrNvVqlXTvn37JEm//PKLioqKdO655yo8PNz68/XXX1sfLRsyZIieeOIJtW3bVuPGjdP69etLzXP99dfrt99+K3Wew+uvv64uXbpYTTF/aN26tfX33Nxcbdu2Tf3793d6HZ544gmnj9gVt27dOi1btsxpvqMx5HjM1q1b1bNnT9WrV0+RkZHW7qeMjAxJJy5ov3btWp133nkaMmSIFi1a5HT8I0eOWP0Tx5/09HTr+MOHD9cdd9yhjh07atKkSR5r9Zdy3SG1atUqpy7uhg0b1KlTJ+uiZMOGDdP8+fM1d+5cRUVFafDgwerWrZu+//57Sf+7IFliYqJWrFihPXv2qE+fPqpUqZJT1xEAAAAAAG8ceeCIx/sCbAFOt/eN3Odxrs1w3v+x474d/6iu4sLCwnTOOec4je3atatMjn3yR7gMw7A+MnbkyBEFBARo9erVTk0rSdaOrTvuuEOpqamaP3++Fi1apIkTJ2rq1Km69957y6S+nTt3asmSJfr444+dxhMTE1VQUKDDhw877ZLau3evEhMTrTk//fST0+Mcm14cczwJCwuz/u7YVfbqq6/qoosucpp38utS/DFXX321Jk+e7HJftWrVJElXX321ateurVdffVXVq1eX3W7X+eefb13fqmXLlkpPT9cXX3yhJUuWqEePHurYsaM+/PBDHTlyRNWqVXO6npeD4/V49NFHdcstt2j+/Pn64osvNG7cOL3//vu6/vrrS8x+upRrQyouLs7p9qRJk6yLkjkuSPbuu+/q8ssvlyTNnDlTDRs21A8//KA2bdpYFyRbsmSJEhIS1Lx5cz3++OMaPXq0Hn30UQUFBZVHLAAAAADAv1RYUFjpk07z3NPhvPPO06pVq9SnTx9rbNWqVT4do0WLFioqKtK+fft06aWXepxXs2ZN3X333br77rv1wAMP6NVXX9W9995r/T96aR8vLMnMmTMVHx+vrl27Oo23atVKlSpV0tKlS62Pvm3evFkZGRlKSUmRJKWkpOjJJ5/Uvn37rG8gXLx4sSIjI9WoUSOva0hISFD16tW1fft29erVy6vHtGzZUh999JHq1KmjwEDXVsyBAwe0efNmvfrqq9Zr+91337nMi4yM1E033aSbbrpJN9xwgzp37qyDBw+qZcuWyszMVGBgoNN1pU527rnn6txzz9WwYcPUs2dPzZw58+xsSBXnuCjZ8OHDZRhGqRcka9OmjccLkg0cOFC//vqrWrRo4fa58vPzlZ+fb93OycmRJBUWFlof97PZbLLZbLLb7VY3uPh4UVGRTNMsdTwgIECGYbh8jNDRNT35jehpPDAwUKZpOo0bhqGAgACXGj2Nk4lMZCITmchEJjKRiUxkIhOZ7CosLJRpmtYfwzCc6ij+mNM57ouTj+H4u2Pccbv434vPGzx4sAYMGKDWrVsrJSVFc+bM0fr161WvXj3rNTj5McWZpqkGDRqoV69e6tOnj6ZOnarmzZtr//79Wrp0qZo2baquXbtq6NCh6tKli84991wdOnRIy5YtU8OGDWWapmrVqiXDMPT555/rqquuUuXKlRUWFqZPPvlEDz74oDZt2lTi62WapmbOnKk+ffooICDA6TWIjIzU7bffruHDh6tKlSqKjIzUkCFDlJKSoosuukimaapTp05q1KiRevfurcmTJyszM1MPP/yw7rnnHqtZdvLzenpdH330Ud13332KjIxU586dlZ+fr7S0NB0+fFjDhg1zedygQYP06quvqmfPnho1apRiYmL0+++/a86cOXr11Vetb9Z75ZVXlJiYqD/++ENjxoxxOsbTTz+t6tWrq3nz5rLZbPrggw+UmJioqKgodezYUSkpKbruuus0efJknXvuudq9e7cWLFig6667To0bN9aoUaN0ww03qG7dutq1a5dWrVqlbt26eXytTdO03ovF309ldZmkM6YhdfJFyU7nBckmTpyo8ePHu4yvWbPG2oYXFxenuTlRqvLXboUdO2zNyQmLU05YnKoe3qmQglydE3Vi0darV0/x8fHasGGDjh3737cpJCcnKzo6WmvWrHH6Ydi0aVMFBQW5fMVi69atVVBQ4PQ524CAAF1wwQXKzs52+lxtaGiomjVrpqysLG3fvt0aj4qKUsOGDbV7926nbZtxcXGqX7++0tPTtX//fms8KSlJSUlJ2rJli7Kzs61xMpGJTGQiE5nIRCYykYlMZKqomUJCQnT06FHrvuPHj1sfjZJONLVCQkKUn5/v9D/gQUFBCgoKUl5enlONwcHBqlSpko4dO+bUlAsJCVFgYKCOHj3q9D/+oaGhstlsys11/qa9sLAw2e12p9fF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+/bt/+ErdMKYMWM0adIkbdq0SU2bNtXEiRP11ltv6aWXXtKvv/6qYcOG6dZbb9XXX3/t9vGlvS6SdPz4cT3++ONat26dPv30U+3YsUO33Xabdf8jjzyijRs36osvvtCmTZv04osvqmrVqtZjU1NTFRERoW+//Vbff/+9wsPD1blzZxUUFKiwsFDXXXed2rdvr/Xr12vlypUaMGCADMMok9fHXwLLuwAAAAAAAM4Y4eGe77vqKmn+/P/djo+Xjh51P7d9e6lYo0d16khZWa7zTPNUqnRrxowZqlmzpl544QUZhqHk5GTt3r1bo0eP1tixYxUVFaXmzZtr+fLlat26tZYvX65hw4Zp/PjxOnLkiLKzs/X7779bjZ+JEyeqV69e1vWZGjRooOeee07t27fXiy++qIyMDIWFhek///mPIiIiVLt2bbVo0UKSFBUVpaCgIFWuXFmJiYlOddavX99qvpSkZ8+e+r//+z8dO3ZMV199tV577bUyeZ0ee+wxderUSdKJj/5NmDBBS5YsUUpKiiSpXr16+u677/Tyyy+7bYKV9rqEhITo9ttvt+bXq1dPzz33nC644AIdOXJE4eHhysjIUIsWLdS6dWtJJ5p0DnPmzJHdbtdrr71mNZlmzpyp6Oho69xlZ2frP//5j+rXry9JatiwYZm8Nv7EDikAAAAAACqATZs2KSUlxWmnTNu2bXXkyBHt2rVLktS+fXstX75cpmnq22+/Vbdu3dSwYUN99913+vrrr1W9enU1aNBAkrRu3TrNmjVL4eHh1p/U1FTZ7Xalp6erU6dOql27turVq6fevXtr9uzZOuqpQVfM0qVLnXYTefLMM8/o559/1v/93/9p27ZtGj58+Cm+Ms4cTSBJ+v3333X06FF16tTJKedbb72lbdu2uX18aa+LJK1evVpXX321atWqpYiICKuxlZGRIUkaOHCg3n//fTVv3lz333+/VqxY4XT833//XREREdbxY2JilJeXp23btikmJka33XabUlNTdfXVV2vatGnas2dPmbw2/sQOKQAAAAAAHI4c8XxfQIDz7WLXBHJhO2n/h5fXTzrdOnTooDfeeEPr1q1TpUqVlJycrA4dOmj58uU6dOiQ046gI0eO6K677tKQIUNcjlOrVi0FBQXp559/1vLly7Vo0SKNHTtWjz76qFatWqXo6Oh/XGtiYqISExOVnJysmJgYXXrppXrkkUdUrVq1f3TcsLAw6+9H/j7f8+fPV40aNZzmBQcHu318aa9Lbm6uUlNTlZqaqtmzZysuLk4ZGRlKTU1VQUGBJKlLly7auXOnFixYoMWLF+uKK67QoEGD9NRTT+nIkSNq1aqVZs+e7XL8uLg4SSd2TA0ZMkQLFy7UnDlz9PDDD2vx4sVq06bNqb0o5YCGFAAAAAAADsWaFeU29xQ1bNhQH330kUzTtHZJff/994qIiFBSUpKk/11H6plnnrGaTx06dNCkSZN06NAhjRgxwjpey5YttXHjRp1zzjkenzMwMFAdO3ZUx44dNW7cOEVHR+urr75St27dFBQUZF1A/Z+y2+2STnzEriw1atRIwcHBysjI8PoaVaW9Lr/88osOHDigSZMmWdfNSktLc5kXFxenvn37qm/fvrr00ks1atQoPfXUU2rZsqXmzJmj+Ph4RUZGeqyjRYsWatGihR544AGlpKTo3XffpSEFAAAAAABOj+zsbK1du9ZpLDY2Vvfcc4+effZZ3XvvvRo8eLA2b96scePGafjw4bL9vWOrSpUqatq0qWbPnq0XXnhBktSuXTv16NFDx48fd2rKjB49Wm3atNHgwYN1xx13KCwsTBs3btTixYv1wgsvaN68edq+fbvatWunKlWqaMGCBbLb7TrvvPMknbgu0o8//qgdO3ZYHzuz2Wy64oordP3113v82N6CBQu0d+9eXXDBBQoPD9evv/6qUaNGqW3btk7XWnK8BkeOHNH+/fu1du1aBQUFqVGjRl6/lhERERo5cqSGDRsmu92uSy65RNnZ2fr+++8VGRmpvn37ujymtNfFsXvs+eef1913360NGzbo8ccfdzrG2LFj1apVKzVu3Fj5+fmaN2+edR2oXr166b///a+uvfZaPfbYY0pKStLOnTv18ccf6/7779fx48f1yiuv6JprrlH16tW1efNmbd26VX369PE695mAhhQAAAAAAP8iy5cvty4e7tC/f3+99tprWrBggUaNGqVmzZopJiZG/fv318MPP+w0t3379lq7dq31bXoxMTFq1KiR9u7dazWTJKlp06b6+uuv9dBDD+nSSy+VaZqqX7++brrpJklSdHS0Pv74Yz366KPKy8tTgwYN9N5776lx48aSpJEjR6pv375q1KiRjh07pvT0dNWpU0fbtm1TlrsLvP8tNDRUr776qoYNG6b8/HzVrFlT3bp105gxY5zmFX8NVq9erXfffVe1a9fWDh8/Hvn4448rLi5OEydO1Pbt2xUdHa2WLVvqwQcfdDu/tNclLi5Os2bN0oMPPqjnnntOLVu21FNPPaVrrrnGOkZQUJAeeOAB7dixQ6Ghobr00kv1/vvvS5IqV66sb775RqNHj1a3bt30119/qUaNGrriiisUGRmpY8eO6bffftObb76pAwcOqFq1aho0aJDuuusun3KXN8M0y/CS/v9SOTk5ioqKUnZ2ttN2uElrPL9BHMa0KP2bAQAAAAAAZ468vDylp6erbt26CgkJKe9ygDNOSe8RTz0UX/EtewAAAAAAAPArGlIAAAAAAADwKxpSAAAAAAAA8CsaUgAAAAAAAPArvmXPT7y5QLrERdIBAAAAAEDFxw4pAAAAAAAA+BUNKQAAAAAAAPgVDSkAAAAAAAD4FQ0pAAAAAAAA+BUNKQAAAAAAKrAOHTpo6NCh5V0G4IRv2QMAAAAA4G/efkN6WeGb1nG2YocUAAAAAAD/UgUFBeVdQoXA6+h/NKQAAAAAAPiX6NChgwYPHqyhQ4eqatWqSk1N1YYNG9SlSxeFh4crISFBvXv3VlaW551e+fn5GjlypGrUqKGwsDBddNFFWr58uXX/gQMH1LNnT9WoUUOVK1dWkyZN9N577zkd48MPP1STJk0UGhqq2NhYdezYUbm5udb9r732mho2bKiQkBAlJydrxowZXuW7/PLLNXjwYKex/fv3KygoSEuXLi2z+t29jvAvGlIAAAAAAPyLvPnmmwoKCtL333+vSZMm6fLLL1eLFi2UlpamhQsXau/everRo4fHxw8ePFgrV67U+++/r/Xr1+vGG29U586dtXXrVklSXl6eWrVqpfnz52vDhg0aMGCAevfurZ9++kmStGfPHvXs2VO33367Nm3apOXLl6tbt24yTVOSNHv2bI0dO1ZPPvmkNm3apAkTJuiRRx7Rm2++WWq2O+64Q++++67y8/OtsXfeeUc1atTQ5ZdfXib1u3sdX3rpJR/OAMqCYTpWzFksJydHUVFRys7OVmRkpDXuzWeHvf28r7efQ+bzwwAAAABweuXl5Sk9PV1169ZVSEiI031n+jWkOnTooJycHP3888+SpCeeeELffvutvvzyS2vOrl27VLNmTW3evFnnnnuuOnTooObNm+vZZ59VRkaG6tWrp4yMDFWvXt16TMeOHXXhhRdqwoQJbp/3P//5j5KTk/XUU0/p559/VqtWrbRjxw7Vrl3bZe4555yjxx9/XD179rTGnnjiCS1YsEArVqwoMV9eXp6qV6+ul156yWqqNWvWTN26ddO4cePKpH53ryOclfQe8dRD8RUXNQcAAAAA4F+kVatW1t/XrVunZcuWKTw83GXetm3bdO655zqN/fLLLyoqKnIZz8/PV2xsrCSpqKhIEyZM0AcffKA///xTBQUFys/PV+XKlSWdaBBdccUVatKkiVJTU3XllVfqhhtuUJUqVZSbm6tt27apf//+uvPOO63jFxYWKioqqtRsISEh6t27t9544w316NFDP//8szZs2KDPPvuszOp39zrC/2hIAQAAAADwLxIWFmb9/ciRI7r66qs1efJkl3nVqlVzGTty5IgCAgK0evVqBQQEON3naGr997//1bRp0/Tss8+qSZMmCgsL09ChQ60LfwcEBGjx4sVasWKFFi1apOeff14PPfSQfvzxR6vp8+qrr+qiiy5yOv7Jz+fJHXfcoebNm2vXrl2aOXOmLr/8cmsnVlnU71D8dYT/0ZACAAAAAOBfqmXLlvroo49Up04dBQaW/r/4LVq0UFFRkfbt26dLL73U7Zzvv/9e1157rW699VZJkt1u15YtW9SoUSNrjmEYatu2rdq2bauxY8eqdu3a+uSTTzR8+HBVr15d27dvV69evU4pU5MmTdS6dWu9+uqrevfdd/XCCy+Uef0of1zUHAAAAACAf6lBgwbp4MGD6tmzp1atWqVt27bpyy+/VL9+/VRUVOQy/9xzz1WvXr3Up08fffzxx0pPT9dPP/2kiRMnav78+ZKkBg0aWDugNm3apLvuukt79+61jvHjjz9qwoQJSktLU0ZGhj7++GPt379fDRs2lCSNHz9eEydO1HPPPactW7bol19+0cyZM/X00097neuOO+7QpEmTZJqmrr/++jKtH2cGGlIAAAAAAPxLVa9eXd9//72Kiop05ZVXqkmTJho6dKiio6Nls7n/X/6ZM2eqT58+GjFihM477zxdd911WrVqlWrVqiVJevjhh9WyZUulpqaqQ4cOSkxM1HXXXWc9PjIyUt98842uuuoqnXvuuXr44Yc1depUdenSRdKJZtJrr72mmTNnqkmTJmrfvr1mzZqlunXrep2r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fc1q+prVi7VXWlbHeSrLrCce/3fuUtbeyTW5PR+e3gdyn7W0teea1f358JTV5Xz8/d4ube15lVUezutJr4GjhtLOh7dZPa0xj1lLWXveZDUMw6usDr6+zzydD09ZXf8b4Tiv3mctae25z3rqa8+brKYtwG09PmUtdj6KP66k8+FLVm/WnlPWEtaeV1mlEv7b6vv7zP1/E0997TmfV++zelp7Jf07ovj5cOQrbe2dnNdT1pL+22o9trSsf9d+8rG8/u9QKeNe/9xzU/upjnvzb6N/Mk4mMnkaJxOZJDJ5qtHX8YqeydPjfFWuDakjR47o999/t26np6dr7dq1iomJUa1atTR06FA98cQTatCggerWratHHnlE1atXt3ZRNWzYUJ07d9add96pl156ScePH9fgwYN188038w17AAAAAAAAZ6hybUilpaXpssv+v707D6uq2t8Avg6gkjggmCgqOKECgqLiFP7ECdSbpuKYmlOllhNeM6ec8zpnpanlLbPRzKxbmuVQmZo5JCg45TwPiAMgg3De3x/cs+85nGkfzuawsvfzPD1PbuH1u/Zee+191tlDW+XPEyZMEEIIMXjwYLFu3ToxadIkkZGRIV588UVx7949ERUVJbZt2yY8PT2V3/nkk0/E6NGjRfv27YWbm5uIi4sTb731lsvbQkRERERERERE6hTrhFR0dLTpm5kK0Ol0Ys6cOWLOnDlWf8bHx0d8+umnRVEeEREREREREREVAfObEYmIiIiIiIiIiIoQJ6SIiIiIiIiIiMilOCFFREREREREREQuxQkpIiIiIiIiIiJyKU5IERERERERERGRS3FCioiIiIiIiIiIXMqjuAsgIiIiInKFBUdSVP3c5IiKxZJHRET0d8IJKSIiIiIiCaiZ4OLkFhERPS44IUVERERE9Jjh1VtERCQ7PkOKiIiIiIiIiIhcihNSRERERERERETkUpyQIiIiIiIiIiIil+KEFBERERERERERuRQnpIiIiIiIiIiIyKU4IUVERERERERERC7FCSkiIiIiIiIiInIpTkgREREREREREZFLeRR3AUREREREJLcFR1JU/dzkiIpFXAkRET0ueIUUERERERERERG5FCekiIiIiIiIiIjIpTghRURERERERERELsUJKSIiIiIiIiIicik+1JyIiIiIiFxK64ekq8njA9eJiOTCK6SIiIiIiIiIiMileIUUERERERHRfxXH1VuO5BERPS54hRQREREREREREbkUJ6SIiIiIiIiIiMilOCFFREREREREREQuxQkpIiIiIiIiIiJyKT7UnIiIiIiI6C9Cy4ek8wHuRFSceIUUERERERERERG5FK+QIiIiIiIiIunwiiuixxsnpIiIiIiIiOixxwkuIrlwQoqIiIiIiIjIAbI/f4uTb/RXwAkpIiIiIiIiIrJKzQQXJ7fIUXyoORERERERERERuRQnpIiIiIiIiIiIyKV4yx4RERERERERuQSfl0UGvEKKiIiIiIiIiIhcildIERERERERERGJ4rmC6+/6NkZeIUVERERERERERC7FCSkiIiIiIiIiInIpTkgREREREREREZFLcUKKiIiIiIiIiIhcihNSRERERERERETkUpyQIiIiIiIiIiIil+KEFBERERERERERuRQnpIiIiIiIiIiIyKU4IUVERERERERERC7FCSkiIiIiIiIiInIpTkgREREREREREZFLcUKKiIiIiIiIiIhcihNSRERERERERETkUpyQIiIiIiIiIiIil+KEFBERERERERERudRjMyG1cuVKUaNGDeHp6SmaN28uDhw4UNwlERERERERERGRBY/FhNSGDRvEhAkTxMyZM8Uff/whGjZsKGJjY8WtW7eKuzQiIiIiIiIiIirgsZiQWrZsmXjhhRfE0KFDRUhIiFi9erUoXbq0eP/994u7NCIiIiIiIiIiKuAvPyGVk5MjDh8+LDp06KAsc3NzEx06dBC//fZbMVZGRERERERERESWeBR3Ac5KSUkReXl5ws/Pz2S5n5+fOHnypMXfyc7OFtnZ2cqf79+/L4QQIjU1VeTm5goh8ie1stLThIBe6ADlZ6HTCaFzEzrohQBEaqqb8vNubm4iLy9PwOjn3d3dhU6nE9kP7pnUAF3+7+mgN1l+/34JIYQQeXl5Jss9PDwEAGV59oN7Quh0+TmAaY6yXK/UZ1yjXq8Xer3eZHlWeprSJpMadTqT5ampbkqbDOvKuK2G2o3ba62tDx6UNGlTfuk64e7ublKjaVstbw9rbS24Pey2Vf+/WgxtNbRJVVvd3K1uj3v3PEzWu7W2GrfJWt9T01Z3d/f8tupNa7e0PWy11bjvKW210/cKttVa38tKu2+yP5nUaNT3DO211fey0h6Y9TFrbS24P+WX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7KZNm7q0LURERETO8CjuAoiIiIj+Tjw8PISHR/4pWHp6uujatatYuHCh2c8Zbrnr2rWrCAwMFO+9957w9/cXer1eNGjQQOTk5Jj8vJeXV9EXT0RERKQRTkgRERERFZPGjRuLTZs2iRo1aiiTVMbu3LkjTp06Jd577z3RunVrIYQQe/bscXWZRERERJrjLXtERERExeTll18Wqampon///uLgwYPi7Nmz4ocffhBDhw4VeXl5okKFCsLX11e8++674syZM2LXrl1iwoQJxV02ERERkdM4IUVERERUTPz9/cXevXtFXl6eiImJEWFhYWL8+PHC29tbuLm5CTc3N/H555+Lw4cPiwYNGoj4+HixePHi4i6biIiIyGl8yx4REREREREREbkUr5AiIiIiIiIiIiKX4oQUERERERERERG5FCekiIiIiIiIiIjIpTghRURERERERERELsUJKSIiIiIiIiIicilOSBERERERERERkUtxQoqIiIiIiIiIiFyKE1JERERERERERORSnJAiIiIiIiIiIiKX4oQUERERERERERG5FCekiIiIiIiIiIjIpTghRURERERERERELvX/oG9CEq05d7IAAAAASUVORK5CYII=",
      "text/plain": [
       "<Figure size 1200x600 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "import matplotlib.pyplot as plt\n",
    "\n",
    "# Plot the number of movie releases by year\n",
    "plt.figure(figsize=(12, 6))\n",
    "movie_counts_by_year.plot(kind='bar', color='skyblue')\n",
    "plt.title('Number of Movie Releases by Year')\n",
    "plt.xlabel('Year')\n",
    "plt.ylabel('Number of Releases')\n",
    "plt.xticks(rotation=45)\n",
    "plt.grid(axis='y', linestyle='--', alpha=0.7)\n",
    "plt.tight_layout()\n",
    "\n",
    "# Highlight the years with the highest and lowest number of releases\n",
    "plt.axvline(x=year_highest_release, color='green', linestyle='--', label=f'Highest: {highest_release_count} releases')\n",
    "plt.axvline(x=year_lowest_release, color='red', linestyle='--', label=f'Lowest: {lowest_release_count} releases')\n",
    "plt.legend()\n",
    "\n",
    "plt.show()\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "\n",
    "# <a id='conclusions'></a>\n",
    "## Conclusions\n",
    "\n",
    "- **Highest Profit Year:** The analysis revealed that the year 2015 had the highest profit rate in the dataset.\n",
    "- **Highest Rated Movie:** The movie titled \"The Story of Film: An Odyssey\" obtained the highest rating of 9.2.\n",
    "- **Highest and Lowest Revenues:** The movie \"Avatar\" had the highest revenue, while \"Wild Card\" had the lowest revenue.\n",
    "- **Budget vs. Ratings:** There was a weak positive correlation (correlation coefficient ≈ 0.08) between movie budgets and ratings.\n",
    "- **Highest and Lowest Budget Movies:** \"The Warrior's Way\" had the highest budget, while \"Mr. Holmes\" had the lowest budget.\n",
    "- **Release Trends:** The year 2014 saw the highest number of movie releases, while 1961 had the lowest.\n",
    "### Limitations\n",
    "\n",
    "- **Data Quality:** The analysis relies on the quality of the data provided. Incomplete or inaccurate data could lead to biased conclusions.\n",
    "\n",
    "- **Generalization:** The findings are based on the dataset and may not be applicable to all movie industries or time periods. Regional and temporal variations could influence the results.\n",
    "\n",
    "## Submitting your Project \n",
    "\n",
    "> **Tip**: Before you submit your project, you need to create a .html or .pdf version of this notebook in the workspace here. To do that, run the code cell below. If it worked correctly, you should see output that starts with `NbConvertApp] Converting notebook`, and you should see the generated .html file in the workspace directory (click on the orange Jupyter icon in the upper left).\n",
    "\n",
    "> **Tip**: Alternatively, you can download this report as .html via the **File** > **Download as** submenu, and then manually upload it into the workspace directory by clicking on the orange Jupyter icon in the upper left, then using the Upload button.\n",
    "\n",
    "> **Tip**: Once you've done this, you can submit your project by clicking on the \"Submit Project\" button in the lower right here. This will create and submit a zip file with this .ipynb doc and the .html or .pdf version you created. Congratulations!"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 665,
   "metadata": {
    "tags": []
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "[NbConvertApp] Converting notebook Investigate_a_Dataset.ipynb to html\n",
      "[NbConvertApp] WARNING | Alternative text is missing on 4 image(s).\n",
      "[NbConvertApp] Writing 639337 bytes to Investigate_a_Dataset.html\n"
     ]
    }
   ],
   "source": [
    "# Running this cell will execute a bash command to convert this notebook to an .html file\n",
    "!python -m nbconvert --to html Investigate_a_Dataset.ipynb"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3 (ipykernel)",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.10.13"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 4
}
