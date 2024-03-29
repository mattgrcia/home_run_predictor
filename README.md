## Home Run Predictor

#### Install

From your command line or Terminal (MacOS):

```
git clone https://github.com/mattgrcia/home_run_predictor
```

#### Required Software

<a href="http://www.r-project.org/">R</a>

<a href="http://www.python.org/downloads/">Python</a>

#### Recommended

<a href="http://rstudio.com/products/rstudio/">RStudio</a>

<a href="http://jupyter.org/install">Jupyter Notebook</a>

### Fast Track

1. Create master data sheet in <i>R</i> using <b>data/create_master.Rmd</b>.

2. Train and select model in <i>Python</i> using <b>training/class_model.ipynb</b>.

3. Generate matchups in <i>Python</i> using <b>predictions/create_matchups.ipynb</b>.

4. Combine pitcher and hitter stats in <i>R</i> using <b>predictions/create_matchups.Rmd</b>.

5. Generate predictions in <i>Python</i> using <b>predictions/automated_predictions.ipynb</b>.


### Detailed Pipeline

#### Data Collection

```
Main file - data/create_master.Rmd
```

Using the <a href="http://github.com/cpsievert/pitchRx">pitchRx</a> package, a database is created with the information on every pitch within the selected date range.  From this information, outcomes (singles, doubles, flyouts, etc.) in order to determine stats.  Basic, advanced, and split stats are created, as well as hot zone statistics.  A hot zone graph, also referred to as a heat map, looks like this:

![Hot Zone](img/hotzone.png?raw=true "Hot Zone")

Each pitcher and hitter has a slugging percentage in each zone.  These are ranked by zone, creating a psuedo-power center profile for each player.

Once all stats are collected, each player has a profile for that season.

The same process is then run (without the stats collection) to get all atbats for the next season.  Pitchers and hitters are matched up to have a complete view of each atbat with each player's stats from the previous season.  Knowing the handedness of the pitcher and hitter allows us to select the relevant split stats.  The hot zone profiles are matched up using the sum of the squared error for zone ranks (think the higher the number, the less the zones match up).  Intuitively, a closer hot zone match would mean a greater chance of success for the hitter.

This consitutes our master data set and it is exported for training and testing.


#### Model Training

```
Main file - training/trad_model.ipynb
Optional file - training/gbm_model.ipynb
```

Now that you have a data set ready for training, you have some options in terms of modeling.  Optionally, you can choose to train a gradient-boosted model (XGBoost in this case).  The optional file will allow you to tune hyperparameters and select a model to save.  The main file will allow you to train the following sci-kit learn models:

<a href="http://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html">Logistic Regression</a>

<a href="http://scikit-learn.org/stable/modules/generated/sklearn.naive_bayes.GaussianNB.html">Gaussian Naive Bayes</a>

<a href="http://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.htmlDecision">Decision Tree</a>

<a href="http://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html">Random Forest</a>

Of course, you can add to this list by appropriately importing and adding a model to <i>scaled_models</i> or <i>unscaled_models</i>.

Unsurprisingly, there is a very large class imbalance issue, as we would not expect anywhere near half of MLB atbats to result in home runs.  The true ratio is about 97:3 in favor of non-home run atbats.  Therefore, this code makes use of oversampling to balance the dataset for training purposes.  Running through the code will allow you to evaluate models training on oversampled data and those trained on the unaltered data.  Once you select and save a model, you are ready to make predictions on current/future matchups.

#### Predicting

```
File 1 - predictions/create_matchups.ipynb
File 2 - predictions/create_matchups.Rmd
File 3 - predictions/generate_predictions.ipynb
```

Generating predictions for a specific day will take three steps.  First, you must use File 1 to scrape up-to-date information on projected starting pitchers and lineups.  After downloading your DraftKings playerpool file for the day (saved by default as 'DKSalaries.csv'), this code will spit out a file of pitcher-hitter matchups on which a model could predict, assuming the required stats were included.

These stats are introduced by running File 2, which will then output a matchups file with all the stats you need to run File 3 and generate predictions for the day.


### Further Implementation

To make this more scalable, stats should be left in and pulled from a SQL database, rather than my showcasing the ability to use R and Python.

The DraftKings playerpool download will be automated once the 2020 baseball season rolls around.
