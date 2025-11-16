# Off-the-Grid Travel Planning Chatbot (Australia)

This project is a **Dialogflow CX + Gemini** chatbot that helps tourists plan **remote, off-the-grid trips across Australia** with **seasonal, safety, and ethical travel guidance**.

The chatbot is designed as a **virtual travel assistant** for adventure-seekers heading to regions like the **Outback, Nullarbor, Gibb River Road, or Cape York**, where planning for connectivity, weather, and safety is critical.

---

## Project Goal

To support **tourists exploring remote areas of Australia** by providing:

- **Location- and month-specific travel advice**
- Guidance on **safety, weather, and preparation**
- Ethically aligned, **responsible and culturally sensitive travel recommendations**

The chatbot aims to **increase traveller confidence** before they “go off-grid”, especially where connectivity and services may be limited.

---

## Tech Stack

- **Dialogflow CX** – for intents, entities, pages, and conversation flow.
- **Google Vertex AI (Gemini)** – for **generative fulfilment**, producing personalised travel advice.
- **Parameters & Entities**
  - `location` – remote area / region (custom entity).
  - `month` – travel month (system or custom entity, mapped to season).

---

## Conversation Flow

1. **Start Page**
   - Triggered by: `Default Welcome Intent`
   - Bot: “Hi there! I'm your travel assistant for off-the-grid Aussie adventures.”
   - Transition → `WelcomePage`

2. **WelcomePage**
   - Bot: “Would you like help planning your remote trip?”
   - Yes → `LocationInfoPage`  
   - No → Session ends

3. **LocationInfoPage**
   - Bot: “Which remote region would you like to explore?”
   - Collects: `location`
   - If `location` is set → `MonthInfoPage`

4. **MonthInfoPage**
   - Bot: “Which month are you planning to travel?”
   - Collects: `month`
   - If `month` is set → `ConfirmInput1`

5. **ConfirmInput1**
   - Bot: “You're planning to visit **$location** in **$month**. Would you like to continue with this plan?”
   - Yes → `AdvicePage`  
   - No → `ConfirmInput2`

6. **ConfirmInput2** – Revision Loop
   - Bot: “No problem! What would you like to update — the location, the travel month, or both?”
   - Location → Clear `location`, go back to `LocationInfoPage`
   - Month → Clear `month`, go back to `MonthInfoPage`
   - Both → Clear both, re-collect location and month

7. **AdvicePage**
   - Uses **Vertex AI / Gemini** to generate customised advice.
   - Prompt includes:
     - `location`
     - `month` (internally mapped to a **season** like dry/wet/shoulder)

8. **ConfirmationPage**
   - Bot: “Was this advice helpful? Would you like to go ahead with this plan?”
   - Yes → `GoodbyePage` (end session)
   - No → Back to `ConfirmInput2` for adjustments

---

## How It Works 

- **Intent Recognition**
  - Handles yes/no decisions and user choices (e.g., update location, month, or both).

- **Parameter Collection**
  - Uses Dialogflow CX entities to capture `location` and `month`.
  - Validation ensures both parameters are present before generating advice.

- **Conditional Routing**
  - Routing logic between pages ensures a clean revision loop for correcting inputs.

- **Generative Fulfilment (Gemini)**
  - Gemini receives structured context:
    - Travel destination (location)
    - Month + inferred season
    - Returns contextual advice on:
    - Weather expectations
    - Safety precautions
    - Road and fuel considerations
    - Suggested travel window and activities

---

## Demo

The prototype includes a short demo video showing:

- The user entering a remote location and month
- The chatbot confirming details
- Gemini generating tailored travel advice
- The revision loop (changing location/month if the user is not satisfied)

 **Video link:** https://drive.google.com/file/d/1p0lHAjNo7pYcx2KG5yZOlALRK2nESODD/view?usp=sharing 

---

## Future Improvements

- Add **visa and biosecurity** guidance flows.
- Expand **cultural storytelling** and integrate First Nations content more deeply.
- Integrate **real-time alerts** (bushfires, flooding, park closures).
- Add **multilingual support** for key inbound markets (e.g., Japanese, Mandarin, Vietnamese).
