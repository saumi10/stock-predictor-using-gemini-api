# AI-Powered Stock Analysis Assistant

This project is a web application built with React that allows users to input key financial metrics for a stock and receive an analysis powered by the Google Gemini AI model. The application calculates common financial ratios and provides an assessment of whether the stock appears overvalued or undervalued, along with a potential buy/hold/sell suggestion based on the provided data.

## Overview

The application presents a simple form where users can enter fundamental financial data points such as Market Price per Share, Earnings Per Share (EPS), Book Value, Sales, Dividends, Debt, Equity, and Net Income. Upon submission, this data is packaged and sent to the Google Gemini API with specific instructions to:

1.  Calculate standard financial ratios.
2.  Analyze the provided data to determine if the stock seems overvalued or undervalued.
3.  Provide a basic recommendation (e.g., Buy/Don't Buy).
4.  Return the analysis formatted as HTML.

The resulting HTML, containing the calculated ratios and AI-generated assessment, is then displayed directly within the application.

## Features

*   **Intuitive Input Form:** Easily enter relevant financial metrics for a stock.
*   **AI-Powered Analysis:** Leverages the Google Gemini API (`gemini-1.5-flash-latest`) to perform calculations and generate insights.
*   **Key Ratio Calculation:** Automatically calculates and displays:
    *   P/E Ratio (Price-to-Earnings)
    *   P/B Ratio (Price-to-Book)
    *   P/S Ratio (Price-to-Sales)
    *   Dividend Yield
    *   Earnings Growth (%)
    *   Debt-to-Equity Ratio
    *   ROE (Return on Equity) (%)
*   **Valuation Assessment:** Provides an AI-driven opinion on whether the stock is Overvalued or Undervalued based on the inputs.
*   **Simple Recommendation:** Offers a basic suggestion regarding buying the stock.
*   **Clear Results Display:** Presents the analysis in a structured HTML table format.
*   **Loading Indicator:** Shows a loading animation while waiting for the API response.
*   **Reset Functionality:** Allows clearing the current results to perform a new analysis.

## Tech Stack

*   **Frontend:** React.js (using Create React App)
*   **AI/Analysis Engine:** Google Gemini API (via REST API call)
*   **API Client:** Native `fetch` API
*   **UI Components:**
    *   Standard HTML/CSS
    *   `react-spinners` (for loading animation)
*   **Development Environment:** Node.js, npm (or yarn)

## How it Works

1.  **Data Input:** The user fills in the financial metrics in the `FinancialForm` component.
2.  **Prompt Engineering:** When the form is submitted, the `FinancialForm.js` component constructs a specific prompt for the Gemini API. This prompt includes:
    *   Pre-defined "training" messages to set the context (acting as a stock analyzer).
    *   Instructions detailing *which* financial ratios to calculate.
    *   Instructions specifying the desired output format (HTML `div` and `table`).
    *   The user-provided financial data, stringified as JSON.
3.  **API Call:** The application makes a `POST` request to the Google Generative Language API endpoint (`https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash-latest:generateContent`) using the `fetch` API. The request includes the structured prompt and the necessary API key.
4.  **AI Processing:** The Gemini model processes the input data and instructions, performs the requested calculations, generates the analysis, and formats the response as HTML.
5.  **Response Handling:** The React application receives the HTML response from the API.
6.  **Rendering:** The `Result` component uses `dangerouslySetInnerHTML` to render the received HTML content, displaying the analysis and ratios to the user.

**Note:** The core calculations and qualitative analysis (over/undervalued, buy/don't buy) are performed by the external Google Gemini LLM based on the prompt and data provided, not by custom algorithms embedded within this React application itself.

## Setup and Installation

1.  **Clone the repository:**
    ```bash
    git clone <your-repository-url>
    cd <repository-directory>
    ```
2.  **Install dependencies:**
    ```bash
    npm install
    # or
    yarn install
    ```
3.  **Set up Environment Variables:**
    *   You need an API key from Google for the Gemini API. You can obtain one from [Google AI Studio](https://aistudio.google.com/app/apikey) or Google Cloud Console.
    *   Create a file named `.env` in the root directory of the project.
    *   Add your API key to the `.env` file like this:
        ```
        REACT_APP_GEMINI_API=YOUR_GEMINI_API_KEY
        ```
        Replace `YOUR_GEMINI_API_KEY` with your actual key.

## Running the Application

1.  **Start the development server:**
    ```bash
    npm start
    # or
    yarn start
    ```
2.  Open your web browser and navigate to `http://localhost:3000` (or the port specified in your console).

## Environment Variables

*   `REACT_APP_GEMINI_API`: **Required**. Your API key for accessing the Google Gemini API.