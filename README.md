# Food Waste Risk Classification for Small Cafés and Bakeries
Student: Alona Fedorova
Student Number: x25121626
Stage: Interim Submission

# 1. Project Overview
Small cafés and bakeries usually make a bit more than they sell, and whatever doesn't go out by closing ends up as waste. A place that size rarely has any system for noticing which products this keeps happening to.

This project predicts that from past sales. For a given product on a given day, the model says whether the waste risk is low, medium, or high.

Right now all the work is on the machine learning side. The notebook prepares the data, builds the risk labels, trains a few models, and compares them.

# 2. Current Status
This is the interim version. The notebook is the part that's actually working — it runs start to finish, loads the data, builds the columns I need, creates the target label, and trains and compares three models.
What's done:

loaded the sales data and looked at its structure and any missing values
added the extra columns the project relies on
labelled each record as low, medium, or high risk
trained a baseline, a decision tree, and a random forest
compared all three on accuracy, precision, recall, F1, and confusion matrices

The app itself doesn't exist yet. The form, the MySQL database, live prediction, the history table, and input validation are all next-stage work

# 3. Dataset
I'm using the Store Item Demand Forecasting Challenge dataset from Kaggle. The original file has only four columns:

- `date`
- `store`
- `item`
- `sales`

There are no real prepared or leftover quantities in the data, so I build those in the notebook. What it derives:

- `weekday` from the date
- `category` from `item`
- `sold_quantity` from `sales`
- `prepared_quantity` from previous sales plus a small buffer
- `leftover_quantity`
- `leftover_percentage`
- `risk_label`, the final low / medium / high class

The notebook reads it from `../data/raw/train.csv`.


# 4. Project Structure
```
Fedorova_Alona_x25121626_food-waste-risk-classification/
├── app/
├── data/
│   └── raw/
│       └── train.csv
├── models/
├── notebooks/
│   └── food_waste_risk_classification.ipynb
└── README.md
```


# 5. How to Run the Notebook
Clone the repo:

```
git clone https://github.com/psfedorova/Fedorova_Alona_x25121626_food-waste-risk-classification.git
cd Fedorova_Alona_x25121626_food-waste-risk-classification
```

Then install what the notebook needs:

```
pip install pandas numpy matplotlib scikit-learn jupyter
```

Start Jupyter:

```
jupyter notebook
```

and open notebooks/food_waste_risk_classification.ipynb. Run the cells in order, top to bottom

# 6. Libraries Used
- pandas
- numpy
- matplotlib
- scikit-learn
- Jupyter Notebook

# 7. Models
Three models at this stage:

- baseline with `DummyClassifier`
- decision tree with `DecisionTreeClassifier`
- random forest with `RandomForestClassifier`

The baseline is there as a floor: a very simple prediction the other two have to beat to be worth anything.

They're evaluated on accuracy, precision, recall, F1, and the confusion matrix

# 8. Work Still To Do
The next stage is turning the notebook into a small working app.

- save the chosen model into `models/`
- build the app in `app/`
- a form for category, prepared quantity, and weekday
- wire the form up to the trained model
- show the predicted risk back to the user
- store records and predictions in MySQL
- add a history table
- add input validation
- add a simple summary chart if there's time
- finish testing, screenshots, the final report, and the presentation
