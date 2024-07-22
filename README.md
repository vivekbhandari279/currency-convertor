# Currency Converter

## Overview

The Currency Converter is a versatile and user-friendly application designed to provide real-time currency conversion rates for over 150 different currencies worldwide. This project leverages cutting-edge technology to ensure accurate and up-to-date exchange rates, making it an essential tool for travelers, businesses, and anyone dealing with multiple currencies.

## Features

- **Real-time Exchange Rates**: Fetches the latest exchange rates from reliable financial APIs to ensure accuracy.
- **Multi-Currency Support**: Supports conversion between a wide range of currencies.
- **User-Friendly Interface**: Intuitive design with easy-to-use input fields and clear, concise conversion results.
- **Historical Data**: Access to historical exchange rate data for trend analysis.
- **Offline Mode**: Stores the latest exchange rates locally for offline conversion.
- **Customizable Settings**: Options to set default currencies and personalize the user experience.
- **Mobile and Web Compatibility**: Responsive design ensures seamless usage across various devices.

## Technology Stack

- **Frontend**: React
- **Backend**: Node.js
- **APIs**: Financial APIs like ExchangeRate-API or Open Exchange Rates
- **Database**: MongoDB

## Installation

1. Clone the repository:
    ```bash
    git clone https://github.com/yourusername/currency-converter.git
    ```

2. Navigate to the project directory:
    ```bash
    cd currency-converter
    ```

3. Install dependencies:
    ```bash
    npm install
    ```

4. Start the development server:
    ```bash
    npm start
    ```

## Usage

1. Open your browser and navigate to `http://localhost:3000`.
2. Select the currencies you want to convert between.
3. Enter the amount to be converted.
4. Click the "Convert" button to view the conversion result in real-time.

## Example

Here's an example of how to use the `App.jsx` file:

```jsx
import { useState } from "react";
import "./App.css";
import { InputBox } from "./components";
import useCurrencyInfo from "./hooks/useCurrencyInfo";

function App() {
  const [amount, setAmount] = useState(0);
  const [from, setFrom] = useState("usd");
  const [to, setTo] = useState("inr");
  const [convertedAmount, setConvertedAmount] = useState(0);
  const currencyInfo = useCurrencyInfo(from);
  const currencies = Object.keys(currencyInfo);

  const convert = () => {
    setConvertedAmount(amount * currencyInfo[to]);
  };

  return (
    <div
      className="w-full h-screen flex flex-wrap justify-center items-center bg-cover bg-no-repeat"
      style={{
        backgroundImage: `url('https://images.unsplash.com/photo-1519751138087-5bf79df62d5b?q=80&w=2940&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D')`,
      }}
    >
      <div className="w-full">
        <div className="w-full max-w-md mx-auto border border-gray-60 rounded-lg p-5 backdrop-blur-sm bg-white/30">
          <form
            onSubmit={(e) => {
              e.preventDefault();
              convert();
            }}
          >
            <div className="w-full mb-1">
              <InputBox
                label="From"
                currencyOptions={currencies}
                selectCurrency={from}
                amount={amount}
                onCurrencyChange={(currency) => {
                  setAmount(amount);
                }}
                onAmountChange={(amount) => setAmount(amount)}
              />
            </div>
            <div className="relative w-full h-0.5">
              <button
                type="button"
                className="absolute left-1/2 -translate-x-1/2 -translate-y-1/2 border-2 border-white rounded-md bg-blue-600 text-white px-2 py-0.5"
                onClick={() => (
                  setFrom(to), 
                  setTo(from),
                  setConvertedAmount(amount),
                  setAmount(convertedAmount)
                )}
              >
                swap
              </button>
            </div>
            <div className="w-full mt-1 mb-4">
              <InputBox
                label="To"
                currencyOptions={currencies}
                selectCurrency={to}
                amount={convertedAmount}
                onCurrencyChange={(currency) => {
                  setTo(currency);
                }}
                amountDisable
              />
            </div>
            <button
              type="submit"
              className="w-full bg-blue-600 text-white px-4 py-3 rounded-lg"
            >
              {`Convert ${from.toUpperCase()} To ${to.toUpperCase()}`}
            </button>
          </form>
        </div>
      </div>
    </div>
  );
}

export default App;
