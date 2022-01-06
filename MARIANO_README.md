

# Resume

Hello Mariano.
Along with saying hello, I can tell you that this challenge was very entertaining because it includes knowledge in:
- Git
- Python or Java
- Basics of ML
- DBA
- ETL
- Documentation
- English

So thank you so much for the opportunity.

Now I will give you a summary of how I approached the problem:
Thinking that an ETL solution is needed for the Analytics area, I used the Kedro framework which was created by QuantumBlack and McKinsey in Python and is a very good open source tool for developing ML projects.
The solution was thought to be installed in a UNIX based SO:

* [What is Kedro?](https://kedro.readthedocs.io/en/stable/01_introduction/01_introduction.html)

The basic architecture of kedro consists of three types of objects:

- A "catalog" is a source of information that can be a GCP Bucket, CSV, Parquet, JSON, BigQuery Table and others, which you declare in a YML file. It also can be versioned.
- A "node" is the function where you will use the catalogs as inputs and outputs. Here is where I create the Python functions to resolve the problem, with the tag "walmart" that you are going to use to run the solution.
- And finally a "pipeline" is the grouping of several nodes. In this case, the pipeline is called "dataEngineer".

Basically, a pipeline contains nodes that receives catalogs as inputs, and then python fucntions returns dataframes that can be saved as outputs catalogs.

# Deployment

## V1.2
This file was modified because the V1.1 failed.
In this version we are going to use Ubuntu 18.04 LTS as OS.
First, we are going to update and upgrade Ubuntu:
```
  sudo apt update
  sudo apt upgrade
```
Then, we are going to download Miniconda, install it and create the enviroment "kedro"
```
  wget https://repo.anaconda.com/miniconda/Miniconda3-py39_4.10.3-Linux-x86_64.sh
  bash Miniconda3-py39_4.10.3-Linux-x86_64.sh
  conda create --name kedro python=3.9 && conda activate kedro
```
Now, we are going to install PIP3, Kedro itself whit kedro-viz and Pandas (which one was used to solve the problem):
```
  sudo apt install python3-pip
  sudo pip3 install kedro==0.17.0
  sudo pip3 install kedro-viz
  sudo pip3 install pandas
```
Finally, lets clone the repo and run the pipeline
```
  mkdir "your folder" && cd "your folder"
  git clone https://github.com/drojosr/pruebaWalmart.git
  cd pruebaWalmart/Deployment/kedro
  kedro run --tag walmart
```

## V1.1
So, let's get started with the installation.
The first thing I will ask you is to install "Miniconda", which I use to mantain my enviroment:

* [Install Miniconda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html)

Once Miniconda is installed, let's create a folder to clone my repository:
```
mkdir "your folder" && cd "your folder"
```

After that, use this to clone my GitHub repo:
```
git clone https://github.com/drojosr/pruebaWalmart.git
```

Then, use this command to access to the repo folder and create the "kedro" enviroment with all the dependencies, included Kedro:
```
cd pruebaWalmart && conda env create -f enviroment.yml
```

Following we are going to activate the enviroment, and enter to the Deployment folder:
```
conda activate kedro && cd Deployment/kedro
```
Finally, we are going to execute the Kedro pipeline:
```
kedro run --tag walmart
```
If it worked well, You can look in the console that Kedro automatically generate a log that can be included in a log file:
```
2022-01-04 13:19:57,588 - kedro.io.data_catalog - INFO - Loading data from `result` (CSVDataSet)...
2022-01-04 13:19:57,598 - kedro.pipeline.node - INFO - Running node: cleaningResult: cleaningResult([result]) -> [result_refined]
2022-01-04 13:19:57,602 - kedro.io.data_catalog - INFO - Saving data to `result_refined` (CSVDataSet)...
2022-01-04 13:19:57,624 - kedro.runner.sequential_runner - INFO - Completed 1 out of 6 tasks
2022-01-04 13:19:57,624 - kedro.io.data_catalog - INFO - Loading data from `result_refined` (CSVDataSet)...
2022-01-04 13:19:57,633 - kedro.io.data_catalog - INFO - Loading data from `consoles` (CSVDataSet)...
2022-01-04 13:19:57,634 - kedro.pipeline.node - INFO - Running node: joinData: joinData([consoles,result_refined]) -> [result_consoles]
2022-01-04 13:19:57,637 - kedro.io.data_catalog - INFO - Saving data to `result_consoles` (CSVDataSet)...
2022-01-04 13:19:57,658 - kedro.runner.sequential_runner - INFO - Completed 2 out of 6 tasks
2022-01-04 13:19:57,659 - kedro.io.data_catalog - INFO - Loading data from `result_refined` (CSVDataSet)...
2022-01-04 13:19:57,667 - kedro.pipeline.node - INFO - Running node: top10WorstGames: top10WorstGames([result_refined]) -> [top_10_worst_game]
2022-01-04 13:19:57,670 - kedro.io.data_catalog - INFO - Saving data to `top_10_worst_game` (CSVDataSet)...
2022-01-04 13:19:57,671 - kedro.runner.sequential_runner - INFO - Completed 3 out of 6 tasks
2022-01-04 13:19:57,671 - kedro.io.data_catalog - INFO - Loading data from `result_refined` (CSVDataSet)...
2022-01-04 13:19:57,679 - kedro.pipeline.node - INFO - Running node: top10BestGames: top10BestGames([result_refined]) -> [top_10_best_game]
2022-01-04 13:19:57,682 - kedro.io.data_catalog - INFO - Saving data to `top_10_best_game` (CSVDataSet)...
2022-01-04 13:19:57,683 - kedro.runner.sequential_runner - INFO - Completed 4 out of 6 tasks
2022-01-04 13:19:57,683 - kedro.io.data_catalog - INFO - Loading data from `result_consoles` (CSVDataSet)...
2022-01-04 13:19:57,692 - kedro.pipeline.node - INFO - Running node: top10WorstGamesCompany: top10WorstGamesCompany([result_consoles]) -> [top_10_worst_game_company]
2022-01-04 13:19:57,701 - kedro.io.data_catalog - INFO - Saving data to `top_10_worst_game_company` (CSVDataSet)...
2022-01-04 13:19:57,702 - kedro.runner.sequential_runner - INFO - Completed 5 out of 6 tasks
2022-01-04 13:19:57,702 - kedro.io.data_catalog - INFO - Loading data from `result_consoles` (CSVDataSet)...
2022-01-04 13:19:57,710 - kedro.pipeline.node - INFO - Running node: top10BestGamesCompany: top10BestGamesCompany([result_consoles]) -> [top_10_best_game_company]
2022-01-04 13:19:57,719 - kedro.io.data_catalog - INFO - Saving data to `top_10_best_game_company` (CSVDataSet)...
2022-01-04 13:19:57,720 - kedro.runner.sequential_runner - INFO - Completed 6 out of 6 tasks
2022-01-04 13:19:57,720 - kedro.runner.sequential_runner - INFO - Pipeline execution completed successfully.
```
Also, you can actually see the pipeline using this command. This shows to you functions(F Icons) and catalogs(Databases Icons). This is very useful to show in comercial meetings or to explain somebody the arquitecture of the model solution:
```
kedro viz
```

This is what the pipeline looks like :

<img width="600" alt="visualization" src="https://user-images.githubusercontent.com/12601497/148120799-438b4b54-13ee-46f7-bd3f-6996c7bd8cf7.png">

Finally, you can remove the enviroment:
```
conda deactivate && conda remove --name kedro --all
```

# Explaining the solution
First, this is the location of the node.
As I explain above, this is the file with all the functions used to resolve the problem :

```
./pruebaWalmart/Deployment/kedro/src/walmart/pipelines/dataEngineer/nodes.py
```

And this is the location of the whole dataEngineer pipeline:
```
./pruebaWalmart/Deployment/kedro/src/walmart/pipelines/dataEngineer/pipeline.py
```

### Cleaning
So, the first what I do after cloning the repo was to check both csv files. 
I encounter 2 consoles with blank spaces in the "result" file, so the pipeline starts with a cleaning function called "cleaningResult". This node takes the result csv and returns a refinedResult as an output catalog:

```
def cleaningResult(df):
    df['console']=df['console'].str.strip()
    return df
```
The filepath of this output is:
```
./pruebaWalmart/Deployment/kedro/data/02_intermediate/result_refined.csv
```
### Joindata ResultRefined - Consoles
Now with the new refined result file we can merge it with consoles file with an inner join:
```
def joinData(refinedResults,consoles): 
    df = refinedResults.merge(consoles,how='inner')
    return df
```
The filepath of this output is:
```
./pruebaWalmart/Deployment/kedro/data/02_intermediate/resultConsoles.csv
```

### Top 10 best/worst games

Now I can program the first 2 functions which deliver:
- The top 10 best games for all consoles
- The worst 10 games for all consoles.

For this two functions I actually encounter many games with the same grade using metascore field (As we spoke), so I modify this and I used metascore and userscore for the sorting
```
def top10BestGames(refinedResults): 
    df = refinedResults.sort_values(by=['metascore','userscore'],ascending= False).head(10).drop_duplicates(subset=['name'])
    return df
```
```
def top10WorstGames(refinedResults):   
    df = refinedResults.sort_values(by=['metascore','userscore'],ascending= True).head(10).drop_duplicates(subset=['name'])
    return df
```
The filepath of this 2 outputs are:
```
./pruebaWalmart/Deployment/kedro/data/08_reporting/top_10_best_game.csv
./pruebaWalmart/Deployment/kedro/data/08_reporting/top_10_worst_game.csv
```
### Top 10 best/worst games/company
And for the last two functions, I used the resultConsoles catalalog to obtain:
- The top 10 best games for each console/company.
- The worst 10 games for each console/company.

For this two other functions what I did was grouping the games by company/console with the joinedData:
```
def top10BestGamesCompany(resultConsoles):
    grouped =resultConsoles.groupby(['company','console'])
    df=grouped.apply(lambda g: g.sort_values(by="metascore",ascending=False).head(10))
    df2=df[['metascore','name']].reset_index()
    df2=df2[['company','console','metascore','name']]
    df2=pd.DataFrame(df2)
    return df2
```
```
def top10WorstGamesCompany(resultConsoles):   
    grouped =resultConsoles.groupby(['company','console'])
    df=grouped.apply(lambda g: g.sort_values(by="metascore",ascending=True).head(10))
    df2=df[['metascore','name']].reset_index()
    df2=df2[['company','console','metascore','name']]
    df2=pd.DataFrame(df2)
    return df2
```
The filepath of this 2 outputs are:
```
./pruebaWalmart/Deployment/kedro/data/08_reporting/top_10_best_game_company.csv
./pruebaWalmart/Deployment/kedro/data/08_reporting/top_10_worst_game_company.csv
```

# Data Model
Finally, this is the data model that I create based on the problem and the datasets.
I use Navicat Data Modeler because has multiple DB to choose, it's very popular around the web and is open source thinking that I'm using a Mac. In fact, I haven't used a tool like this in a long time:

<img width="554" alt="Screen Shot 2022-01-06 at 11 43 46" src="https://user-images.githubusercontent.com/12601497/148400627-a1929836-778a-4f49-939b-8ee9d5f16e76.png">

"A company can have one or more games, but a game can be in only one company"

The model file format is in this filepath:
```
./pruebaWalmart/DataModel/walmartModel.ndm2
```

### Thanks again for the opportunity and I hope this README will be easy to understand.


















