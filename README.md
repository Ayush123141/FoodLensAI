# MacroSnap

MacroSnap is a Streamlit app that helps users estimate calories and macros from a meal photo or a text description using Gemini AI. It then lets them send a final summary straight to WhatsApp using Twilio.

This project is built for demo and learning purposes and is perfect for workshops, hackathons, or portfolio projects.

## Demo

A user can:
- enter their name and WhatsApp number once
- ask a nutrition question
- upload a meal photo
- get quick calorie and macro estimates
- send a summary to WhatsApp

## Features

- AI nutrition assistant powered by Gemini
- Image-based meal analysis
- Text-based meal queries
- Calorie and macro estimation
- Conversation memory within a single chat session
- WhatsApp summary delivery via Twilio
- Clean Streamlit UI

## Tech Stack

- Python
- Streamlit
- Google GenAI (Gemini)
- Twilio WhatsApp API

## Project Structure

```text
macrosnap/
├── app.py
├── prompts.py
├── requirements.txt
├── README.md
├── .gitignore
├── .streamlit/
│   ├── secrets.toml
│   └── secrets.toml.example
└── .venv-1/               # local virtual environment
```

## Prerequisites

Before running the app, make sure you have:

- Python 3.9 or newer
- A Google AI Studio account
- A Gemini API key
- A Twilio account
- A WhatsApp number that has joined Twilio's sandbox

## Setup

### 1. Clone the project

```bash
git clone <your-repo-url>
cd macrosnap
```

### 2. Create a virtual environment

Windows PowerShell:

```powershell
python -m venv .venv-1
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv-1\Scripts\Activate.ps1
```

### 3. Install dependencies

```powershell
pip install -r requirements.txt
```

## Secrets Configuration

Copy the example file and fill in your real values:

```bash
copy .streamlit\secrets.toml.example .streamlit\secrets.toml
```

Then update the file:

```toml
GEMINI_API_KEY = "your-google-gemini-key"

TWILIO_ACCOUNT_SID = "ACxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
TWILIO_AUTH_TOKEN = "your-twilio-auth-token"
TWILIO_WHATSAPP_FROM = "whatsapp:+14155238886"
TWILIO_CONTENT_SID = "HXxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

### Important notes

- `TWILIO_WHATSAPP_FROM` is the sandbox sender number provided by Twilio.
- `TWILIO_CONTENT_SID` is the Content Template SID you create in Twilio.
- Your actual WhatsApp number is entered inside the app during onboarding.

## Gemini API Key

1. Go to Google AI Studio
2. Create a project or use an existing one
3. Generate an API key
4. Paste it into `GEMINI_API_KEY`

## Twilio WhatsApp Sandbox Setup

1. Log in to Twilio Console
2. Open Messaging
3. Go to Try it out → WhatsApp
4. Copy the sandbox number and join code
5. Open WhatsApp on your mobile phone
6. Send the join message from your real WhatsApp number

Example:

```text
join twilio-trial
```

This is required so the number can receive messages from the sandbox.

## Create the WhatsApp Content Template

In Twilio:

1. Go to Messaging → Content Template Builder
2. Create a new template
3. Use a structure like this:

```text
Hi {{1}}, here's your MacroSnap summary:

{{2}}
```

After saving, Twilio gives you a Content SID starting with `HX...`.

Paste that value into `TWILIO_CONTENT_SID`.

## Run the App

From the project folder:

```powershell
cd "C:\Users\Ayush\Downloads\macrosnap"
.\.venv-1\Scripts\Activate.ps1
streamlit run app.py --server.port 8503
```

Then open:

```text
http://localhost:8503
```

If port 8503 is busy, use another port such as 8502 or 8501.

## How It Works

### Onboarding
The app asks for:
- name
- WhatsApp number with country code

### Chat Interface
Users can send:
- text questions
- meal photos
- follow-up nutrition questions

### Nutrition Analysis
Gemini analyzes the request and gives a friendly estimate for:
- meal name
- calories
- protein
- carbs
- fat

### WhatsApp Summary
When the user clicks the WhatsApp button:
- the app asks Gemini to summarize the conversation
- Twilio sends the summary using the approved WhatsApp template

## Troubleshooting

### Button stays disabled
The button becomes active only after the user sends an actual chat message.

### Twilio timeout error
This usually means:
- the wrong WhatsApp number was used
- the sandbox was not joined from the intended phone
- the template is wrong or inactive
- the Content SID does not belong to the correct template

### Wrong template message received
This happens when the template in Twilio does not match the MacroSnap summary format.
Use a custom MacroSnap template, not a default appointment or event template.

### Port already in use
Use another port:

```powershell
streamlit run app.py --server.port 8502
```

## Notes

This project is meant for educational and demo use. For production WhatsApp business communication, Twilio requires a verified business profile and approved templates.

## License

This project is intended for learning, demos, and personal projects.
