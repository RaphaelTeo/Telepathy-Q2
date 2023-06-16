# QUESTION 1 (Software Design and Implementation)

## Metadata

Language: Python

Environment Setup:

1. Create new virtual environment with venv
2. Activate with q1venv\scripts\activate
3. Install required packages
    - pandas
    - openpyxl


## Submission (main)

This interpretation takes **"Canonical Models" as the base** and supplements it with *  *additional data from the "Car Models [X]" sheets ** where possible, then tries to **fill in any data gaps**.

As **"Car Models 2"** does not provide any additional data, we **discard** it.



## Submission (Interpretation 2)

To put it in the context of a practical scenario, let's assume that a client has provided us with a list of car models (e.g. "Car Models [X]"), and we need to ensure that its entries are matches our official database of "Canonical Models". Hence, we **take each "Car Models [X]" sheet** as the base of comparison and try to **augment its data using "Canonical Models"**.

"Car Models 2", however, is missing the full spelling of "Make", and we cannot eliminate the possibility that different Makes use the same Model names, which affects the reliability of the key used to compare between sheets. Therefore, while "Car Models 1" can be augmented directly with "Canonical Models", **"Car Models 2" needs to use the output from the previous step**.

2 sheets are produced, one for "Car Models 1" and one for "Car Models 2".



## Considerations and Issues Encountered

1. Take note of **missing spaces** cause it to seem different ("G80 EV" vs "G80EV").
2. Take note of **different make names** ("HYUN" vs "HYD").
3. When creating the key values, the **strings were forced to lowercase and stripped** (remove leading and trailing spaces). Format validation (string) is not required here since it would throw an error if the values were not strings, and it can be forced to be strings via str(x) if needed. 
4. There was an **extra whitespace** for " model" in the "Canonical Models" headers. Kept me puzzled for about 15 mins, since VSC doesn't highlight the space when you drag over it with the mouse/double-click. Checked back in the spreadsheet to find the issue.
5. "Car Models 1" has both a HYUN | EXCE | EXCEL, and a HYD | EXCEL | EXCEL. Which is correct? **Can we trust "Car Models 2" to be correct?** 