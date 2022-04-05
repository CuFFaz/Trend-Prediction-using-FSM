## Trend Forecasting using FSM

# A Brief Intro
Predicting trend patterns based on <a href='https://en.wikipedia.org/wiki/Finite-state_machine'>Finite State machine</a> via state-slope estimation. Trend patterns when considered as a state machine, shows the possibility of an arbitrary point on the trendline to possess one of the multiple states(based on its state transition table)(predefined in the script) through its slope and direction. 
Just for a brief understanding, for a certain trend 3 states can be considered - ascending, peak or descending. Based on initial input slope of a line we map a particular state and furthermore transitions between these states are estimated based on the training data of different variants of <a href='https://www.ig.com/en/trading-strategies/10-chart-patterns-every-trader-needs-to-know-190514'>trend patterns</a>. For such a data dependent model we use data from <a href='https://trends.google.com/trends'>Google Trends</a>. 

Vision to the Project: Extrapolate unusual keywords whose polularity on Google Search just started amplifying swiftly. Example- Covid, Omicron, Someone's Death, etc

Primarily this project has 3 parts:
1. Data Extraction and Preprocessing
2. Training Data for states
3. Get dataframe of current & forecasted Trends 


#### Google Search based Data
Google Trends provides Periodic Trends for keywords in the form of normalised values which are structured in a beautiful manner. Trends of multiple keywords can be compared and the relative trend data is obtained. These values are respectively scaled upto the one which has highest search volumes among a set of upto 5 keywords. Now, GT doesn't let us compare for more than a set of 5 keywords at once, hence we normalise it ourselves via mathematical means. Thanks to <a href='https://towardsdatascience.com/using-google-trends-at-scale-1c8b902b6bfa#:~:text=Currently%2C%20the%20public%2Dfacing%20Google,of%20all%20the%20major%20candidates.'>this</a>.
Every bit of the data was acquired from Google Trends via <a href='https://pypi.org/project/pytrends/'>PyTrends</a>, an unconventional api for GT.

## Data Preprocessing
Data is gathered by scraping from pytrends and later pre-processed followed by 
- Normalisation
- Concatenation 
- Minimization
- Moving averages (Moving Averages to focus and smooth up the trend slopes and directions) (_file)
- Transform (Take Transpose of every individual datapoint and make it more model specific) (_file)

## Local Maxima, Slopes and Trend Durations
Find the local peaks such that we obtain only the trending pattern, from the trend's initial ascend till its death which is proportional to a threshold which is peak specific.
Slopes calculated

