This repository consists of two independent prototype implementations which have been worked out as part of the BAMP 2022 by Ante Jelavic, Franziskus Perkhofer, Manuel Mencher, Melissa Ewering and Tim Ritzheimer.

While the first prototype, saved in folder "1-Sentiment & Emotion Analysis" deals with classifying twitter data in sentiments and emotions, the second prototype, saved in folder "2-Topic Modelling", deals with the automatic detection of themes. This README file will in the follwing explain what has to be considered to run this scripts.

**1-Sentiment & Emotion Analysis:**

Folder structure:
- Input data: This is one file ("Demographics.xls") which has been created manually - This includes public person and their twitter ID so that a API call to collect tweet data can be made
- Output data: Here, all files which are created with the scripts (except visualizations) are stored. For example the collected Tweets which will be analyzed are stored here. Three files ("Tweets.csv" + "enTweetsNew.csv" + "FinalResults.csv") have been uploaded with a smaller data set because of space limitation of GitHub (100 MB). However, the full version of those three can be found here (Access limited to Mannheim Business School accounts): https://mbs3du-my.sharepoint.com/:f:/g/personal/tritzhei_mbs_education/ErAZdCpLKNlCsiZFnk9nrtABTDre2eB_fO3hqabttb-evw?e=hCsqOZ 
- Scripts: All scripts are save including the outputs. The follwing order does represent the process in which the scripts were run / implemented:
    1. DataCollectionTweetsPerUser: A Twitter Developer account is needed and credentials (Bearer Token) need to be included in the script
    2. SentimentAnalysis: Should be run in Google colab - otherwise commands (e.g. like data reading) needs to be adjusted to run locally
    3. VisualizationOfResults
    4. HypothesisTesting
- Scripts_PDF: All scripts saved including Output are stored as PDF version here
- Visualization: All visualization which have been created in the file "VisualizationOfResults" are stored here

During runtime, it is necessary to put the files, which are loaded from the scipt, in the same folder where the scripts are stored. 
All scripts were created under Pyhton Version 3.8.3 and with newest available packages. 

**2-Topic Modelling**
