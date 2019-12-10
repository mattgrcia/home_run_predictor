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

![Hot Zone](img/hotzone.jpg?raw=true "Hot Zone")

Each pitcher and hitter has a slugging percentage in each zone.  These are ranked by zone, creating a psuedo-power center profile for each player.

Once all stats are collected, each player has a profile for that season.

The same process is then run (without the stats collection) to get all atbats for the next season.  Pitchers and hitters are matched up to have a complete view of each atbat with each player's stats from the previous season.  Knowing the handedness of the pitcher and hitter allows us to select the relevant split stats.  The hot zone profiles are matched up using the sum of the squared error for zone ranks (think the higher the number, the less the zones match up).  Intuitively, a closer hot zone match would mean a greater chance of success for the hitter.

This consitutes our master data set and it is exported for training and testing.


#### Model Training

```
Main file - training/class_model.ipynb
```



#### Predicting

```
Main file - predictions/automated_predictions.ipynb
```

### Further Implementation
