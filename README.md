# Gemini-Powered Travel Agent (Homework Week 4)

This project demonstrates an LLM application built using the **Google Gemini 2.5 Flash** API. It showcases how to move beyond simple chat by enforcing structured data schemas and allowing the model to interact with real Python functions.

## Features & Implementation

### 1. API Setup & Configuration
- **Model:** `gemini-2.5-flash` chosen for its speed and high reasoning capabilities.
- **Error Handling:** Utilizes the native exception handling of the `google-genai` SDK.
- **Decoding Parameters:**
    - **Temperature:** Set to `0.0` for extraction (precision) and `0.7` for creative tasks.
    - **Top-K / Top-P:** Configured to balance token diversity vs. coherence.

### 2. Structured Output (Pydantic)
I used a Pydantic model (`LocationEntity`) to define a rigid schema. Gemini's `response_schema` parameter ensures that the model's response is valid JSON that maps perfectly to our Python object. This eliminates the need for manual regex or "JSON-cleaner" scripts.

### 3. Tool Calling
I implemented two local functions: `get_weather` and `get_exchange_rate`. 
- **The Loop:** When the user asks about weather and currency, Gemini identifies that its internal knowledge is insufficient. 
- **Execution:** It generates a `tool_call`, the SDK executes the local Python function, and the result is fed back to Gemini to generate a natural language summary.

## How to Run
1. Get an API key from [Google AI Studio](https://aistudio.google.com/).
2. Export it: `export GEMINI_API_KEY=''`.
3. Install dependencies: `pip install google-genai pydantic`,`pip install google-genai`.
4. Run: the notebook

## Example Interaction
**Input:** "What's the weather in Tbilisi and the GEL exchange rate?"
**Internal Process:**
1. Call `get_weather(location="Tbilisi")` -> "Sunny, 24°C"
2. Call `get_exchange_rate(currency="GEL")` -> "1 USD = 2.65 GEL"
**Final Output:** "In Tbilisi, it's currently a sunny 24°C, and the exchange rate is 1 USD to 2.65 GEL."
