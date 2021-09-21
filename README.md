# Python package for training the model required for https://github.com/Debadri3/Personalized-Cancer-Diagnosis [deployed]

## Steps needed for reproducing the creation of the package-
1. Clone the repo 
2. Go to the directory just above the cloned repo
3. [Type this in cmd prompt] set PYTHONPATH= PATH_TO_REPO\packages\regression_model;.; [For me 'set PYTHONPATH=C:\Users\Debadri\Documents\GitHub\deploying-machine-learning-models\packages\regression_model ;.;'] [Stack OverFlow link: https://stackoverflow.com/questions/338768/python-error-importerror-no-module-named]
4. cd PATH_TO_REPO\packages\regression_model\regression_model>python train_vect_pipeline.py
5. One_hot_encoded_feature models and standard scaler models will be created in the trained_encoders folder 
4. cd PATH_TO_REPO\packages\regression_model\regression_model>python train_pipeline.py
6. Trained Logistic Regression model will be created in the trained_model folder.
7. Test model on a sample prediction-
8. pytest packages\regression_model\tests -W ignore::DeprecationWarning [a bug may be here]
9. Create a .whl file inside the dist folder which is required to  build the package. Also copies content of regression_model child package into build/lib using setuptools and find_package.
10. python setup.py bdist_wheel
11. Install the wheel distribution
11. pip install -e packages/regression_model [Note that this is the parent regression_model directory and not the child. The -e flag ensures the package is not copied in our Python distribution. We just want to work with the code in our source directory]
12. To test the package, run a python CLI inside the command prompt (using python command)
13. Inside Python interpreter: import regression_model
14. regression_model.__version__ (to check version)
15. quit()
Next if you want publish the package, do so in PyPI or Gemfury etc.  

## A description on each sub-directories within 'regression_model' package has been provided-
1. regression_model -> contains python scripts and folders for training the model.
2. tests -> contains sample test to run to check correctness of model

Inside the parent package directory regression_model:

whl file is a type of built distribution that tells installers what Python versions and platforms the wheel will support. 

MANIFEST.IN specifies which files to be included while building our package

setup.py is the file which Python uses for configuration before publishing the package to PYPI.

VERSION is the version number for the package release

1. config-
config.py -> contains variable names of saved models' destination path, names of features etc.

2. datasets -> contains train and test datasets in csv format

3. processing-

data_management.py -> contains function definitions to load and save the model pipelines and vectorizers. Note that whenever a new pipeline is saved, the old pipeline is deleted (excepting some files).

errors.py -> contains input error definitions etc.

vect_preprocessor -> sklearn like class definitions of data preprocessors and encoders used while training the one-hot-models and standard scalers.

preprocessors.py -> sklearn like class definitions of data preprocessors and encoders used while training the Logistic Regression model and while making predictions.

validation.py -> validates input type to the model

4. pipeline.py -> defines the scikit-learn pipeline used while training the one-hot-models and standard scalers.

5. vect_pipeline.py -> defines the scikit-learn pipeline used while training the Logistic Regression model and while making predictions.

6. train_pipeline.py -> main file. Splits dataset into train and validation which is used while training the Logistic Regression model.

7. train_vect_pipeline.py -> another main file. Splits dataset into train and validation used while training the one-hot models and standard scalers.

8. predict.py -> used for single input predictions. Also logs input variables, outputs and model version with the result.

## Further challenges-
1. The uploaded train.csv is only a subset of the original train file on Kaggle [https://www.kaggle.com/c/msk-redefining-cancer-treatment]. This is due to GitHub limitations on maximum file size per commit. This will be solved using GitHub LFS. Meanwhile feel free to download the dataset from Kaggle and use that instead.
2. Set up a CI/CD pipeline (preferably using CircleCI)
3. Docker + Heroku
