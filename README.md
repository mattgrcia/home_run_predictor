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

#### Model Training

```
Main file - training/class_model.ipynb
```

#### Predicting

```
Main file - predictions/automated_predictions.ipynb
```

### Further Implementation
