# Serious-Adverse-Events-Based-on-Age-and-Gender
Predicting Serious Adverse Events Based on Age and Gender (FAERS)
🧠 Project Summary:
"Predicting Serious Adverse Events Based on Age and Gender (FAERS)"

✅ 1. What the Data Represents
working with real-world adverse drug event reports from the FDA's FAERS system via openFDA.
Each report contains:
* Patient age
* Patient sex (1 = Male, 2 = Female)
* Seriousness flag (1 = serious event: death, hospitalization, etc.)

Out of 100 pulled records:
✅ 89 were usable
🔀 23 were in the test set after train/test split

🔍 2. Goal
a binary classification model:
Can we predict whether a drug adverse event will be “serious” based on age and gender?

🧹 3. Feature Engineering
created input features:
* female: Binary (1 if patient is female)
* age_group: Age binned into categories: child, adult, senior, elder
* Converted categorical variables using one-hot encoding (get_dummies)

🧪 4. Model Training
* Model used: RandomForestClassifier
* Target: serious (0 = not serious, 1 = serious)
* Train/test split: 75% training, 25% testing

📊 5. Classification Results (from screenshot)
Metric    Value
Accuracy    65%
Serious class recall    12% (very low)
ROC AUC    0.28 (not good — closer to 0.5 is random, < 0.5 is worse than guessing)

Interpretation:
* The model overfits on the majority class (non-serious) and struggles to catch serious events.
* This happens because the dataset is imbalanced: more non-serious than serious cases.

📈 6. Feature Importance (Bar Chart)
This tells us which features the model used most to make its decision:
Feature    Importance
female    ~34%
age_group_adult    ~30%
age_group_senior    ~20%
age_group_elder    ~10%

Interpretation:
* The model sees being female and being an adult as most predictive of whether an event is classified as serious.
* Second bullet point

While this doesn’t guarantee causality, it can guide further investigation (e.g., does this group report more serious reactions?).

⚠️ 7. Limitations
* Tiny dataset (only 89 examples → only 23 in test set)
* Imbalanced classes (few serious cases → poor recall)
* OpenFDA API is sampled, not the entire FAERS database

💡 8. How to Improve
* Pull more records using &skip=100, &skip=200, etc.
* Apply class balancing (e.g., class_weight="balanced" or SMOTE)
* Add drug info and reaction descriptions as features
* Train on hundreds or thousands of rows

🧭 TL;DR Summary
Step          What Happened
✅ Pull    Got 100 live adverse event records
🧼 Clean    Kept 89 valid rows with age + gender
🧠 Predict    Trained a model to classify “serious” cases
📉 Weak Signal    ROC AUC = 0.28 due to imbalance/small data
📊 Importance    Top drivers were gender + age group
🚀 Ready to scale    built the baseline — next is scaling up 🚀


