# Chatbot for Healthcare Using AI

## Project Overview

The **Chatbot for Healthcare Using AI** is a Python-based web
application that lets users interact with a healthcare chatbot, enter
symptoms, and receive a possible disease prediction based on a symptom
dataset and a pre-trained machine-learning model. Users can also look up
symptoms associated with a disease.

The application uses a Flask web interface and a conversational flow to
collect user input. It includes account registration and login pages, a
symptom list, disease-information lookup, and a link to search for
nearby hospitals.

> **Important:** This is an academic project and is intended for
> learning and informational purposes only. Predictions may be incorrect
> and must not be treated as a medical diagnosis. Consult a qualified
> healthcare professional for medical advice. If you may be experiencing
> a medical emergency, contact local emergency services.

## Features

-   **Healthcare chatbot:** Interact with the system through a
    text-based conversation.
-   **Symptom-based prediction:** Enter symptoms and receive a possible
    disease prediction from the trained model.
-   **Disease symptom lookup:** Enter a disease name to retrieve
    symptoms associated with it in the dataset.
-   **Symptom matching:** Uses text vectorization and cosine similarity
    to match user-entered symptoms with supported symptom labels.
-   **Disease information:** Attempts to retrieve a short disease
    description from an online search result.
-   **Nearby hospital search:** Provides a link to search online for
    hospitals related to the predicted condition.
-   **User registration and login:** Includes basic registration and
    login routes.
-   **Web interface:** Uses Flask routes and HTML templates for the
    chatbot and related pages.

## Technology Stack

The report and implementation show the following technologies:

-   **Language:** Python
-   **Web framework:** Flask
-   **Database / ORM:** SQLite with Flask-SQLAlchemy
-   **Data processing:** pandas, NumPy
-   **Machine learning:** scikit-learn
-   **Model loading:** joblib
-   **Text matching:** `CountVectorizer` and cosine similarity
-   **Data source format:** Excel dataset (`dataset.xlsx`)
-   **Frontend:** HTML templates rendered by Flask
-   **Disease information lookup:** `duckduckgo_search` package

## How It Works

1.  The user opens the web application and starts a chatbot session.
2.  The chatbot asks for basic information, including the user's name
    and age.
3.  The user chooses one of the available options:
    -   **Predict Disease** --- enter symptoms, separated by commas.
    -   **Check Disease Symptoms** --- enter a disease name.
4.  For symptom prediction, the application matches the entered symptoms
    to its supported symptom list, converts them into model input
    features, and loads the saved model from
    `model/random_forest.joblib`.
5.  The model returns a possible disease label. The application then
    attempts to retrieve disease information and offers a web search
    link for nearby hospitals.
6.  For disease symptom lookup, the application searches the dataset for
    the matching disease and displays the associated symptoms.

The prediction depends on the dataset and saved model included with the
project. The report does not establish clinical validation or
medical-grade accuracy.

## Project Structure

The following is a suggested structure based on the files referenced in
the source code. Adjust names to match the files in your repository.

``` text
Chatbot-for-Healthcare-Using-AI/
├── app.py                         # Flask application entry point (use your actual filename)
├── dataset.xlsx                   # Dataset containing Disease and Symptoms columns
├── database.db                    # SQLite database; may be created when the app starts
├── model/
│   └── random_forest.joblib       # Pre-trained machine-learning model
├── templates/
│   ├── index.html
│   ├── index_auth.html
│   ├── instructions.html
│   ├── bmi.html
│   ├── diseases.html
│   ├── pred.html
│   ├── login.html
│   └── register.html
├── msgConstant.py                 # Chatbot greeting/message constants
└── README.md
```

This is an illustrative structure, not a verified listing of the
original project files. Keep only paths and filenames that exist in your
repository. Do not upload private user data or unnecessary generated
database files.

## Prerequisites

-   Python 3 installed
-   pip
-   The project source files and HTML templates
-   The dataset file `dataset.xlsx`
-   The trained model file `model/random_forest.joblib`

The exact Python and package versions are not specified in the report.
If the project was developed with particular versions, document those
versions in a `requirements.txt` file.

## Setup and Run

### 1. Clone the repository

``` bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd <YOUR_REPOSITORY_FOLDER>
```

Replace the placeholders with your repository URL and folder name.

### 2. Create and activate a virtual environment (recommended)

**Windows:**

``` bash
python -m venv .venv
.venv\Scripts\activate
```

**macOS / Linux:**

``` bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

If your repository contains a `requirements.txt` file:

``` bash
pip install -r requirements.txt
```

If you do not yet have one, the imports shown in the report indicate
that the project uses packages including:

``` bash
pip install Flask Flask-SQLAlchemy pandas numpy scikit-learn joblib duckduckgo-search openpyxl
```

Package versions and the `duckduckgo_search` API may vary. Use the
versions compatible with your code. Do not include `openpyxl` unless it
is needed to read the Excel dataset in your environment.

### 4. Check required files

Before running the app, confirm that:

-   The Flask application file is present.
-   `dataset.xlsx` exists at the path expected by the code.
-   `model/random_forest.joblib` exists.
-   The HTML files referenced by `render_template()` are inside the
    `templates/` directory.
-   Any imported project modules, such as `msgConstant.py`, are present.

### 5. Start the application

Run the actual Flask entry-point file. If it is named `app.py`, use:

``` bash
python app.py
```

The source code in the report configures Flask to use port `3000`. If
the application starts successfully, open:

``` text
http://127.0.0.1:3000/
```

If your entry-point filename or port differs, use the values in your
code.

## Example Usage

### Predict a possible disease

1.  Open the application.
2.  Start a chatbot session and provide the requested name and age.
3.  Select **Predict Disease**.
4.  Enter the symptoms supported by the project, separated by commas.
5.  Ask the chatbot to check the disease and review the returned result
    as general information only.

### Check symptoms for a disease

1.  Start a chatbot session.
2.  Select **Check Disease Symptoms**.
3.  Enter a disease name supported by the dataset.
4.  Review the symptoms returned by the application.

The output depends on the dataset, the saved model, and how closely the
entered text matches supported symptom names.

## Dataset and Model

The implementation reads an Excel file named `dataset.xlsx` and expects
columns named `Disease` and `Symptoms`. It also loads a pre-trained
model from `model/random_forest.joblib`.

Ensure that both files are included in the repository or provide clear
instructions for obtaining them. Do not claim a particular dataset size,
model accuracy, or number of supported diseases unless you have verified
it from the actual dataset and evaluation results.

## Limitations

-   The result is a model-generated possibility, not a confirmed
    diagnosis.
-   Only symptoms and diseases represented in the available dataset can
    be handled reliably.
-   User-entered wording may not match the symptom labels recognized by
    the application.
-   Disease descriptions and hospital searches rely on external search
    services and may be unavailable or inaccurate.
-   The report does not provide verified model evaluation metrics or
    evidence of clinical validation.
-   The report describes multiple approaches in different sections; the
    implementation excerpt specifically loads a Random Forest model for
    symptom prediction and uses cosine similarity for text matching.
-   The login code shown in the report compares submitted passwords
    directly with stored values. This is not suitable for production;
    passwords should be stored using a secure password-hashing method,
    and authentication should be reviewed before deployment.
-   The code excerpt includes a hard-coded Flask secret key. Replace it
    with a secure environment variable before any deployment.
-   The application should not be used to make treatment decisions or
    delay professional care.

## Future Enhancements

-   Add secure password hashing and stronger session management.
-   Improve symptom normalization and handling of spelling variations.
-   Add input validation and clearer messages for unsupported symptoms.
-   Evaluate the model using documented metrics and a separate test
    dataset.
-   Use a reliable, maintained source for disease information.
-   Add automated tests and document dependency versions.
-   Improve accessibility, privacy protections, and error handling.

## Academic Context

This project was documented as an internship project titled **"Chatbot
for Healthcare system using AI"** and was conducted at **Compsoft
Technologies** during the 2023--2024 academic year.

## Disclaimer

This project is for educational demonstration only. It is not a
substitute for professional medical advice, diagnosis, or treatment. Do
not rely on its output for medical decisions.
