
# GARCH Time Series Model for Stock Volatility Prediction

This project aims to build a GARCH (Generalized Autoregressive Conditional Heteroscedasticity) time series model to predict stock volatility. The stock data is acquired from AlphaVantage API, cleaned, and stored in a SQLite database. The model is trained on the historical stock data and used to predict future volatility. The model predictions are served using a FastAPI web application.

This project aims to build a GARCH (Generalized Autoregressive Conditional Heteroscedasticity) time series model to predict stock volatility. The stock data is acquired from AlphaVantage API, cleaned, and stored in a SQLite database. The model is trained on the historical stock data and used to predict future volatility. The model predictions are served using a FastAPI web application.

# Installation
1- Clone the repository
    `git clone https://github.com/<username>/<repository>.git
    cd <repository>`

2- Create a virtual environment and activate it
    `virtualenv venv
    source venv/bin/activate  # For Linux and macOS.\venv\Scripts\activate  # For Windows`

3- Install the required packages
    `pip install -r requirements.txt`

4-Set up AlphaVantage API key

To access the AlphaVantage API, you need to obtain an API key from the AlphaVantage website. Once you have obtained the API key, set it as an environment variable in your terminal.

    `export ALPHAVANTAGE_API_KEY=<your-api-key>`
Alternatively, you can add the following line to the .env file in the project directory:

    `ALPHAVANTAGE_API_KEY=<your-api-key>`

5- Run the web application
    `uvicorn app.main:app --reload`

# Usage Example
    `url = "http://localhost:8008/fit"

    # Data to send to path
    json = {
        "ticker": "IBM",
        "use_new_data" : True,
        "n_observations": 2000,
        "p":1,
        "q" : 1
        
    }
    # Response of post request
    response = requests.post(url=url,json=json)
    # Inspect response
    print("response code:", response.status_code)
    response.json()`
### output for the above code
`response code: 200
{'ticker': 'IBM',
 'use_new_data': True,
 'n_observations': 2000,
 'p': 1,
 'q': 1,
 'success': True,
 'message': "Trained and saved 'models/2023-04-12T11:31:32.368947_IBM.pkl' Metrics: AIC 7137.549002867772, BIC 7159.952612705941."}
`

## For Specific Model Prediction

    `url = "http://localhost:8008/predict"
    # Data to send to path
    json = {
        "ticker":"IBM",
        "n_days": 5
    }
    # Response of post request
    response = requests.post(url=url,json=json)
    response.json()`

### output for the above code
`{'ticker': 'IBM',
 'n_days': 5,
 'success': True,
 'forecast': {'2023-04-12T00:00:00': 2.1223784293917447,
  '2023-04-13T00:00:00': 2.14359654731172,
  '2023-04-14T00:00:00': 2.164181671150938,
  '2023-04-17T00:00:00': 2.184160259127017,
  '2023-04-18T00:00:00': 2.2035571217161554},
 'message': ''}`