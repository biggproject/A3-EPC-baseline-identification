# BC4_pipeline

## Context:

The goal of this business case is to track savings realised by the Energy Conservation Measures (ECMs) undertaken by 
the ESCO on a daily/weekly/monthly basis (M&V). The process to estimate savings involves the identification of a
baseline model for the electricity consumption of the building before the retrofit period, e.g. before new equipment
is installed. This model will be used to predict the electricity consumption after the renovation, i.e. post-retrofit, 
to know what the consumption would have been without retrofit. The real consumption post-retrofit and the predicted 
one are then compared to estimate savings.

### Input

- Timeseries:
  - Electricity consumption
  - Outdoor temperature
  - Global horizontal irradiation


- Additional information:
  - Aggregation functions (time grid alignment)
  - Retrofit period from and to (model identification)
  - Country where the building is located (holidays)

### Output

- Model identification/training phase:
  - Model reference (e.g. MLflow URI)
  - Model scores (R^2, MBE, NMBE, RMSE, CVRMSE)


- Prediction phase:
  - Predicted Electricity consumption timeseries

## How to run it:

### Jupyter notebooks:
There are two jupyter notebooks that you can run as demo for this application:
- **BC4_pipeline_training_github.ipynb**:  workflow to train a baseline model for electricity consumption data starting 
from harmonised data.
- **BC4_pipeline_prediction_github.ipynb**: workflow to make predictions using the locally stored model that
was trained using the previous notebook. We assume that also the new data used to predict are harmonised.

### Install requirements:
You must have Python installed on your system and a tool capable of running jupyter notebooks. For the official one
you can follow the procedure here: https://docs.jupyter.org/en/latest/install.html
This procedure was tested with **Python 3.8** even though it should work also with other versions.
There are several dependencies to install before running the two notebooks.

#### 1. Install AI TOOLBOX:
Currently, the AI TOOLBOX is not on PyPI, so please follow the installation instructions here: 
https://github.com/biggproject/biggpy/blob/main/ai_toolbox/README.md

#### 2. Install other dependencies:
There are other libraries used for visualizations and to handle rdf files.
If you installed already a virtual env for the AI TOOLBOX, you can activate it, `cd` to this project location
and then install the missing dependencies with:
dependencies with:
```commandline
pip install -r requirements.txt
```

#### 3. Install Intel extension for sklearn (optional):
This extension will speed up the calculations when using sklearn but requires your PC to have an Intel CPU.
If you meet this requirement, please follow the instructions here: 
https://intel.github.io/scikit-learn-intelex/installation.html

The easiest way would be to install it using pip using:
```
pip install scikit-learn-intelex
```

If you decide not to install it, please **remove** these two initial lines from all the notebooks:
```python
from sklearnex import patch_sklearn 

patch_sklearn()
```
