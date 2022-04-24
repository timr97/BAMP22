This repository consists of two independent prototype implementations which have been worked out as part of the BAMP 2022 by Ante Jelavic, Franziskus Perkhofer, Manuel Mencher, Melissa Ewering, Tim Ritzheimer.

While the first prototype, saved in folder "1-Sentiment & Emotion Analysis" deals with classifying twitter data in sentiments and emotions, the second prototype, saved in folder "2-Topic Modelling" deals with the automatic detection of themes. This README file will in the follwing explain what has to be considered to run this scripts.

**1-Sentiment & Emotion Analysis:**

Folder structure:
- Input data: This is one file ("Demographics.xls") which has been created manually
- Output data: Here, all files which are created with the scripts (except visualizations) are stored. Three files ("Tweets.csv" + "enTweetsNew.csv" + "FinalResults.csv") have been uploaded with a smaller data set because of space limitation of GitHub (100 MB). However, the full version of those three can be found here (Access limited to Mannheim Business School accounts): https://mbs3du-my.sharepoint.com/:f:/g/personal/tritzhei_mbs_education/ErAZdCpLKNlCsiZFnk9nrtABTDre2eB_fO3hqabttb-evw?e=hCsqOZ 
- Scripts: All scripts are save including the outputs. The follwing order does represent the process in which the scripts were run / implemented:
    1. DataCollectionTweetsPerUser
    2. SentimentAnalysis: Should be run in Google colab - otherwise commands (e.g. like data reading) needs to be adjusted to run locally
    3. VisualizationOfResults
    4. HypothesisTesting
- Scripts_PDF: All scripts saved including Output are stored as PDF version here
- Visualization: All visualization which have been created in the file "VisualizationOfResults" are stored here

During runtime, it is necessary to put the files, which are loaded from the scipt, in the same folder where the scripts are stored. 
All scripts were created under Pyhton Version 3.8.3 and with newest available packages. 

**2-Topic Modelling**

In this folder the codes and additional assets (such as the underlying data) for the topic modeling prototypes are stored.
The following readme section first describes the Python codes used to perform the topic modeling research activities and second, more details about supported assets are given.

--------------------------------------------------------------
FIRST – PYTHON CODE
In the first part the created python scripts are listed and explained.

PRELIMINARY REMARK
Important to state, the scripts are developed via GoogleColab in order to ensure everyone can easily execute the files. Otherwise, every local environment looks differently and it is difficult to ensure to have a common virtual environment. Hence, utilizing GoogleColab as an easy to access Cloud platform ensuring to have a common environment for everyone who uses it makes a lot of sense. Thus, it is strongly recommended to execute the file in GoogleColab. Alternatively, the files can be executed in another Python IDE but in this case it has to be ensured the right libraries are installed on the local machine and potentially a few GoogleColab related methods for data reading and storing have to be adjusted.

INTRO
In order to setup the analysis around the topic modeling topic four categories of scripts were created.
First, scripts to gather the data from Twitter and building corresponding dataset for further usage were needed (category: DATA GATHERING). Second, scripts for preparing the data, training the model, and storing the corresponding result were created (category: TRAIN MODELS). Third, scripts to build survey for the human judgement experiment were implemented (category: BUILD SURVEYS). Fourth, scripts to assess the human maintained survey were programmed (category: ASSESS SURVEYS).
In the following paragraphs the categories and their respective scripts are listed and briefly explained.

DATA GATHERING
These scripts are required to gather the needed data from Twitter. It leverages the Twitter API and store the acquired data in corresponding CSVs grouped by search term categories. In a later stage these CSV files were merged and prepared for the next step – training the model.
-	BAMP_DG_GetTwitterTweets.ipynb: This script is responsible for reading (maximal) up to 20,000 tweets from Twitter via the recentsearch API method. It takes a search term and a language code as an input and then searches randomly for corresponding messages (from now to 7 days in the past). It stores the results in a corresponding CSV file (per search term pool) for later processing. For obtaining all required data this script was executed with several alterations (changing search criteria).
-	BAMP_DG_PrepocessTweets.ipynb: This script is responsible for preprocessing the loaded Twitter tweets. The data gained from the Twitter API have certain characteristics in the data that should be adjusted for all datasets. For instance, it uses partially deep structures. This means a field basically includes a list of further fields. Hence, this script performs some data processing steps to flatten the structure to have a common table structure without deep fields. However, it does not alter the content itself. This preprocessed data set can then be used in later scripts.
-	BAMP_DG_BuildDataset.ipynb: This script is responsible for merging certain data sets together into one data set that can be used for training a topic model. For this, first relevant small data sets (gathered from the previous scripts – created based on distinct search term) are loaded and merged to one new data set. This is then stored again as a new CSV with all data from the selected small data sets. The script was in general executed twice. First, with all available data and as an output the complete (large) data set was created. A second time with a limited selection of small data sets in order to create the compact (small) data set. With the different data sets the deviation in the model performance based on the data size and spread of topics should be tested.

TRAIN MODELS
These scripts are responsible for processing the data according to the needs of the specific utilized topic model algorithm and also to train the model. Furthermore, the training process includes hyperparameter tuning and a selection of the most promising models.
-	BAMP_TM_LDA.ipynb: This script is responsible for the model training of the LDA topic models. It does the required data preprocessing and includes all the hyperparameter runs. Furthermore, it has logic to document and store the execution results and also perform an assignment run of the tweets based on the finally chosen model. Important to note, it does only deal with unigrams – as part of the data processing. For the use of bi-grams with LDA the next script is used.
-	BAMP_TM_LDA_bigram.ipynb: This script is responsible for the model training of the LDA topic model with bigrams. It is basically identical to the previous script (BAMP_TM_LDA.ipynb) but includes some addition to create bi-grams and accordingly, build LDA models with bigram data.
-	BAMP_TM_BERT.ipynb: This script is responsible for the model training of the BERTopic topic model. It does the required data processing. The hyperparameter tuning is not automated here as the calculation time was very expensive. Hence, the hyperparameter tuning was done here manually with running the same code with altering parameter again and again. After the best model was identified the model was also applied on the utilized data set and this assignment was stored for later usage when comparing the human results. Finally, the script includes functions to store and document the performed training.

BUILD SURVEYS
These scripts are responsible for building the surveys for the human judgement experiment (based on topic intrusion). The scripts can be executed multiple times and by this, can be used to generate multiple unique surveys as it builds up the surveys based on a random generation.
-	BAMP_BS_YesNo.ipynb: This script is used to generate the YesNo surveys. It takes the results from the trained models and builds up surveys accordingly. It is used for both LDA and BERTopic models but it needs to be adjusted accordingly (some values needs to be adjusted). Further, it allows to account for the different complexity. Finally it allows to store the generated surveys to the local file share.
-	BAMP_BS_Choice.ipynb: This script is used to generate the Choice surveys. It takes the results from the trained models and builds up surveys accordingly. It is used for both LDA and BERTopic models but it needs to be adjusted accordingly (some values needs to be adjusted). Further, it allows to account for the different complexity. Finally, it allows to store the generated surveys to the local file share.

ASSESS SURVEYS
These scripts are responsible for assessing the completed surveys from the human experiment. The scripts are run multiple times to assess it survey by survey. A consolidation of all results is done manually by leveraging the assessment generated by these scripts.
-	BAMP_AS_YesNo.ipynb: This script is responsible for comparing a Yes-No survey. It basically uploads a completed survey, it uploads the corresponding reference survey (this has to be adjusted case by case when executing), it then compares the surveys including calculating a success measure, and finally store the protocol of the assessment for later usage.
-	BAMP_AS_Choice.ipynb: This script is responsible for comparing a Choice survey. It basically uploads a completed survey, it uploads the corresponding reference survey (this has to be adjusted case by case when executing), it then compares the surveys including calculating a success measure, and finally store the protocol of the assessment for later usage.


--------------------------------------------------------------
SECOND – ADDITONAL ASSETS
In the second part, further details regarding the generated data and conducted surveys is given (in the DATA part) and information regarding the results (in the RESULTS part) of the model training is provided.
However, as the files partially too large to upload and in order to avoid they are spread across too many sources, it is decided to provide these additional assets on an OneDrive share that can be accessed by any MBS account:
https://mbs3du-my.sharepoint.com/:f:/g/personal/mmencher_mbs_education/Epm9XPgHq1xMrZQwzFPkdncBBeP6QJSj94qXaxX4kiWRCA?e=OGxtP2
In this one drive folder, two subfolders are provided and they consist of the following data files and folders.

DATA
In this section, different used and produced data files are listed.
-	TwitterLoaded: Lists all 23 data pools gathered by calling the Twitter API respectively.
-	Preprocessed: Lists all 23 preprocessed data pools. 
-	MergedSets: Consist of the two main data sets used for the thesis. The small data set is called  “data_compact_all_types.csv” and the large set is called “data_complete_all_types.csv”.
-	Surveys: List all surveys used in the human experiment. It includes the uncompleted and completed surveys and also in different file formats. Furthermore, it lists the control group of the surveys and also has a summary of all completed surveys.

RESULTS
In this section the four chosen prototypes are listed including the training protocols, the respective models, and the generated surveys for the human experiment.
-	Alpha: Is the LDA prototype trained with the small data set.
-	Beta: Is the LDA prototype trained with the large data set.
-	Gamma: Is the BERTopic prototype trained with the small data set.
-	Delta: Is the BERTopic prototype trained with the large data set.