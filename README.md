# Deploying Machine Learning Models

## Project Setup and Key Tools
* Project code is compatiable to Python 3.8.
* GIT Installation and Setup.
  * Clone the Repo: git clone https://github.com/trainindata/deploying-machine-learning-models.git
  * Checkout the Particular Commit : git checkout COMMIT_HASH_FOUND_ON_GITHUB
  * Git cheatsheet: https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet
* MAC OS : PYTHONPATH="/Users/agoswam7/Desktop/UHG/POC/MLFLOW_POC/Deployment-machine-learning-models:$PYTHONPATH" ; export PYTHONPATH
* Other Tools : Pytest, TOX(generic virtualenv management and test command line tool), CircleCi, Heroku, Gemfury.
* TOX WorkFlow Diagram: -- Command [tox -r] (rebuild the environment from scratch)
  ![image](https://user-images.githubusercontent.com/13011167/103164936-6fbd2500-4837-11eb-9d16-59c65adf7216.png)
* Download Datasets from Kaggle.
  * https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data
  * Download the train.csv and test.csv and put them in the regression_model/regression_model/datasets directory.

## Building, Installing and testing the Python Package [Regression_Model]
* Versioning applies not just to model put also to training data and dependencies. So we want to be clear what our dependencies were  and what version of training 
  data we use to create the the model. 
* Using Wheel
* Creating & Building the Package locally [ tox -e install_locally]
* Installing & Testing the above Python Package Locally [pip install -e .]
![image](https://user-images.githubusercontent.com/13011167/103165797-16a6be80-4842-11eb-8554-26331baa8b91.png)

## Serving the Model Pridections Via REST APIs
* Creating REST APIs using Flask Micro Framework. "Lightweight and Flexiable". Alternatives - Django, Pyramid, Bottle, Tornado.
* [Serving the Model through REST APIs]: Serve Predicaitons on the fly to multiple clients. Decopule our model development from client facing layer. Scale by adding 
  more instances of API instance behind the Load Balancer.
* To build & run the REST APIs, execute the following commands from the ml_api directory
  * pip install -r ml_api/requirement.txt
  * export FLASH_APP=run.py
  * export FLASK_ENV=development
  * export FLASK_APP=run
  * [Execute the REST API and will give the API End Point] python run.py 

## CI/CD PIPELINE
* Automating the stages of App Development.
  ![image](https://user-images.githubusercontent.com/13011167/103168411-064e0e00-4859-11eb-9f15-540bd5e72472.png)
* System is always in the releasible stage. 
* CircleCI is CI/CD tool. Other alternatives for CI/CD Tool - Jenkins, Travis CI, Bamboo etc. 
* Enviornment Variables for CircleCI. 
  * KAGGLE_USERNAME=
  * KAGGLE_KEY=
  * PIP_EXTRA_INDEX_URL= https://<gemfurt_token>@pypi.fury.io/<gemfury_username>/
  * HEROKU_API_KEY = 257a8cba-5a27-4c05-95aa-2c5f51a521af
  * HEROKU_APP_NAME =
* Upload the Python Package to the Python Package Index Server. [Make use of Gemfury.com] 

## DIFFERENTIAL TESTS (Comparing different Model Versions)
* Type of test that compares the difference in execution from one version to another version of model when the inputs are same.
* Sometime differential tests are also called back-to-back testing.
* Suppose we forgot to include one pre-processing steo in the code or add the incorrect feature and other test will pass but the predictions that is made will 
  change, so differential test are to catch these type of problems
  
  
### Important Links to Read
* [Testing] : https://sre.google/sre-book/testing-reliability/

Amit Goswami

