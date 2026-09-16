# Voice Assistant

## Project Overview

This is a desktop voice assistant written in Python. It listens to a spoken command
through the microphone, converts the speech to text, works out what the user is asking
for, and then replies out loud while also printing the same response in the terminal.

It can tell the time and date, open a web search in the browser, fetch live weather from
an online API, answer a few general knowledge questions from a local knowledge base, set
timed reminders, send an email through SMTP, and run custom commands that are defined in
a JSON file.

The whole assistant is written in a single, readable file (`voice_assistant.py`) with
small functions, so it is easy to follow and easy to explain.

## OASIS INFOBYTE Internship

Python Programming — Task 1

## Objective

Build a Python based voice assistant that listens to spoken commands and responds with
useful actions, covering both the beginner tier and the advanced tier of the task.

## Features

Every feature listed below is implemented in the code.

- Voice input from the microphone using `speech_recognition`
- Speech to text using the Google Web Speech API (through `recognize_google`)
- Spoken responses using `pyttsx3`, with the same response printed in the terminal
- Greeting that changes with the time of day
- Current time
- Current date
- Web search that opens the default browser with the spoken query
- Live weather from the OpenWeatherMap API
- General knowledge answers from a local knowledge base
- Timed reminders that run in the background while the assistant keeps listening
- Sending an email through `smtplib`, with a spoken confirmation step before sending
- Custom commands loaded from `commands.json` (no Python editing needed)
- Intent detection that works on normal sentences, not just exact keywords
- A `help` command that lists everything the assistant can do
- Error handling for unclear speech, microphone problems, network problems, missing
  configuration and unknown commands
- A typed input mode (`--text`) that is used automatically if no microphone is found

## Beginner Tier Requirements

| OASIS requirement | How it is implemented |
|---|---|
| Voice input with `speech_recognition` | `listen()` records from the microphone with `sr.Microphone()` and converts it using `recognize_google()` |
| Recognized command shown in terminal | `listen()` prints `You: <command>` after recognition |
| Microphone error handling | `listen()` catches `OSError`; `main()` falls back to typed input if no microphone exists |
| Greeting | `handle_greeting()` replies with a greeting based on the time of day |
| Current time | `handle_time()` uses `datetime.now().strftime("%I:%M %p")` |
| Current date | `handle_date()` formats the weekday, day, month and year |
| Web search | `handle_search()` extracts the query and calls `webbrowser.open()` |
| "I didn't understand that. Please try again." | Spoken in `listen()` when `sr.UnknownValueError` is raised |
| Assistant keeps running | The `while` loop in `main()` catches every exception and continues |
| Text to speech with `pyttsx3` | `speak()` prints the response and speaks it aloud |

## Advanced Tier Requirements

| OASIS requirement | How it is implemented |
|---|---|
| Natural language understanding | `INTENT_PATTERNS` + `detect_intent()` match the sentence against ordered regular expressions for each intent |
| Voice email with `smtplib` | `handle_email()` collects recipient, subject and message by voice; `send_email()` sends it over SMTP with TLS |
| Timed reminder | `parse_reminder()` extracts the duration and message; `handle_reminder()` starts a `threading.Timer` so the main loop stays usable |
| Live weather API | `handle_weather()` calls the OpenWeatherMap current weather endpoint with `requests` |
| General knowledge | `KNOWLEDGE_BASE` dictionary plus `handle_knowledge()` for topic matching |
| Custom commands | `commands.json` is loaded by `load_config()` and matched by `match_custom_command()` |
| Privacy documentation | See the "Privacy Considerations" section below |

## Technologies Used

| Technology | Why it is used |
|---|---|
| Python 3.9+ | Main language |
| `speech_recognition` | Records microphone audio and converts it to text |
| `PyAudio` | Microphone backend required by `speech_recognition` |
| `pyttsx3` | Offline text to speech |
| `datetime` | Time and date replies |
| `webbrowser` | Opens web searches and custom command links |
| `requests` | Calls the OpenWeatherMap API |
| `smtplib`, `email.message` | Sends the email |
| `threading` | Runs reminder timers in the background |
| `json` | Reads `commands.json` |
| `re` | Intent matching and extracting details such as city, duration and search query |
| `python-dotenv` | Loads the API key and email credentials from `.env` |
| `logging` | Writes unexpected errors to `assistant.log` |
| `argparse` | Adds the `--text` option |

## Project Structure

```
Python-Programming-Task-1-Voice-Assistant/
│
├── voice_assistant.py     # All assistant logic
├── commands.json          # Custom commands and saved email contacts
├── requirements.txt       # Python dependencies
├── .env.example           # Template for API key and email credentials
├── .gitignore             # Keeps .env and cache files out of Git
├── README.md              # This file
└── screenshots/           # Screenshots for the internship submission
```

`assistant.log` is created automatically when an unexpected error happens. It is ignored
by Git.

## How the Voice Assistant Works

1. The program loads `.env` (API key and email settings) and `commands.json`
   (custom commands and contacts).
2. `pyttsx3` is started once and reused for every spoken response.
3. The assistant greets the user, then enters a loop.
4. In each round it records one command from the microphone and sends the audio to the
   Google Web Speech service, which returns the text.
5. The text is printed as `You: ...`.
6. The text is first compared with the phrases in `commands.json`. If one matches, that
   custom command runs.
7. Otherwise `detect_intent()` matches the sentence against the intent patterns and
   returns an intent such as `time`, `weather` or `reminder`.
8. `handle_command()` calls the matching handler function, which does the work and calls
   `speak()` with the reply.
9. `speak()` prints `Assistant: ...` and says the same text out loud.
10. The loop repeats until the user says something like "exit" or "goodbye".

If anything fails at any step, the error is reported politely and the loop continues.

## Installation

These steps are written for Windows, which is what I used.

### Required Python Version

Python 3.9 or newer. Check with:

```
python --version
```

### Install Dependencies

```
cd Python-Programming-Task-1-Voice-Assistant
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
```

### Microphone Setup

`speech_recognition` needs `PyAudio` to use the microphone.

- On most current Windows systems `pip install -r requirements.txt` installs PyAudio
  directly, because official wheels are available.
- If PyAudio fails to build, install a prebuilt wheel instead:

  ```
  pip install pipwin
  pipwin install pyaudio
  ```

- Then check that Windows can hear you: **Settings → System → Sound → Input**, pick the
  correct microphone and confirm that the input bar moves when you speak.
- Allow microphone access for desktop apps in **Settings → Privacy & security →
  Microphone**.

If no microphone is available, the program prints a message and switches to typed input
instead of crashing. You can also start it that way on purpose with
`python voice_assistant.py --text`.

### Environment Variables

Copy the template and fill in your own values:

```
copy .env.example .env
```

`.env` is in `.gitignore`, so it is never uploaded to GitHub. No key or password is
stored anywhere in the source code.

### Weather API Setup

1. Create a free account at <https://openweathermap.org/api>.
2. Open the **API keys** tab and copy your key.
3. Put it in `.env`:

   ```
   OPENWEATHER_API_KEY=your_key_here
   ```

A new key can take a little while to become active. Until the key is added, the
assistant simply says that the weather key is not configured.

### Email Setup

Use a **test Gmail account**, not your personal one.

1. Turn on 2-Step Verification for that account.
2. Create an **App Password** (Google Account → Security → App passwords). It is a
   16 character password made for programs like this one.
3. Put the values in `.env`:

   ```
   EMAIL_ADDRESS=your.test.account@gmail.com
   EMAIL_APP_PASSWORD=your_16_character_app_password
   SMTP_HOST=smtp.gmail.com
   SMTP_PORT=587
   ```

Your normal Gmail password will not work, and it should never be used here.

If these values are missing, the assistant says that email is not configured instead of
crashing.

## How to Run

```
python voice_assistant.py
```

Typed input mode (useful for testing without a microphone):

```
python voice_assistant.py --text
```

Example session:

```
--------------------------------------------------
VOICE ASSISTANT
--------------------------------------------------
OASIS INFOBYTE SIP Internship | Python Programming - Task 1
Say 'help' to hear the supported commands, or 'exit' to quit.

Assistant: Good morning! Hello! How can I help you?

Listening...
Processing...
You: what time is it
Assistant: The current time is 9:30 AM.

Listening...
```

## Example Voice Commands

| What you say | What happens |
|---|---|
| "Hello" / "Hi" / "Good morning" | Greeting |
| "What time is it?" / "Could you tell me the current time?" | Speaks the current time |
| "What is today's date?" / "Tell me today's date" | Speaks today's date |
| "Search for Python programming" | Opens a Google search in the browser |
| "Look up weather forecasting" | Opens a web search (not the weather API) |
| "What is the weather in Hyderabad?" | Live weather from OpenWeatherMap |
| "What is Python?" / "Explain machine learning" | Answer from the local knowledge base |
| "Remind me after 10 seconds to check my internship task" | Sets a timed reminder |
| "Send an email" | Starts the guided email flow |
| "Open my portfolio" | Custom command from `commands.json` |
| "Help" | Lists all supported commands |
| "Exit" / "Goodbye" | Closes the assistant |

## Custom Commands

Custom commands live in `commands.json`, so a new command can be added without touching
the Python code.

```json
{
  "name": "portfolio",
  "phrases": ["open my portfolio", "show my portfolio"],
  "action": "open_url",
  "value": "https://github.com/",
  "response": "Opening your portfolio page."
}
```

| Field | Meaning |
|---|---|
| `name` | A short label for you; it is not spoken |
| `phrases` | Spoken phrases that trigger the command. If any phrase appears in the sentence, the command runs |
| `action` | `open_url` opens a website, `say` speaks a saved sentence |
| `value` | The website address for `open_url`, or the sentence for `say` |
| `response` | What the assistant says after running an `open_url` command |

**To add a new command:**

1. Open `commands.json` in a text editor.
2. Add a new object inside the `custom_commands` list, following the format above.
3. Remember the comma between objects, and keep all phrases in lower case.
4. Save the file and restart the assistant.

Custom commands are checked **before** the built in intents, so they always take
priority.

`commands.json` also has an `email_contacts` section. These are short names you can speak
during the email flow, for example saying "mentor" instead of dictating a full address:

```json
"email_contacts": {
  "mentor": "mentor@example.com"
}
```

The addresses in this file are placeholders. Replace them with your own test addresses.

## Error Handling

| Situation | What the assistant does |
|---|---|
| Speech could not be understood | Says "I didn't understand that. Please try again." and keeps listening |
| No speech within the timeout | Quietly listens again |
| Microphone not available or blocked | Reports the problem and switches to typed input mode |
| Speech service unreachable | Says the speech service is not reachable and keeps running |
| Missing weather API key | Says the key is not configured |
| Invalid city name (HTTP 404) | Says it could not find weather for that place |
| Rejected weather key (HTTP 401) | Says the key was rejected |
| Weather network failure or unexpected response | Reports the problem without crashing |
| Missing email credentials | Says email is not configured |
| Wrong email password / SMTP failure | Reports the exact type of failure |
| Missing or invalid `commands.json` | Prints a message and continues with built in commands only |
| Unknown command | Suggests saying "help" |
| Any unexpected error | Logged to `assistant.log`, and the loop continues |
| Ctrl+C | Says goodbye and exits cleanly |

## Privacy Considerations

This section describes what the program actually does.

**Microphone input**
The microphone is only opened while the assistant is actively listening for a command.
Recording stops as soon as you stop speaking or the phrase time limit is reached.

**Is audio stored?**
No. The recorded audio is kept in memory only while the command is being recognized, and
no audio file is written to disk by this project.

**What is sent to external services?**
The assistant uses `recognizer.recognize_google()`. **Your recorded audio is sent over the
internet to Google's Web Speech service**, which returns the text. This project is not
offline speech recognition, and an internet connection is required for voice input. If
you are not comfortable with that, run the assistant with `--text` and type the commands
instead.

**What the weather API receives**
When you ask for weather, the city name and your OpenWeatherMap API key are sent to
`api.openweathermap.org`. Nothing else, and no audio, is sent there.

**What the email service receives**
When you send an email, your email address, app password, recipient, subject and message
body are sent to the SMTP server (Gmail by default) over a TLS encrypted connection. The
message is not stored by this project after it is sent.

**What is stored locally**
- `commands.json` — your custom commands and saved contact names.
- `.env` — your API key and email credentials, on your computer only.
- `assistant.log` — technical error messages if something goes wrong. It does not contain
  your commands or your credentials.

Reminders, questions and recognized commands are only kept in memory while the program is
running. No conversation history is saved.

## Security Considerations

- No password, app password or API key is written anywhere in the source code.
- All secrets are read from environment variables using `python-dotenv`.
- `.env` is listed in `.gitignore`; only `.env.example`, which has empty values, is
  committed.
- The email feature is meant to be used with a throwaway test account and a Gmail App
  Password, never a personal account password.
- SMTP uses `starttls()`, so the login and the message are encrypted in transit.
- Before an email is sent, the assistant reads back the recipient, subject and message and
  asks for confirmation, so a misheard command cannot send mail by accident.

## Screenshots

Screenshots are stored in the `screenshots/` folder. I will capture these myself while
running the project.

| File | What it should show |
|---|---|
| `screenshots/01-startup.png` | The startup banner and the first greeting |
| `screenshots/02-time-date.png` | A time request and a date request |
| `screenshots/03-web-search.png` | The search command in the terminal with the browser open |
| `screenshots/04-weather.png` | A live weather reply |
| `screenshots/05-knowledge.png` | A general knowledge answer |
| `screenshots/06-reminder.png` | The reminder being set and firing |
| `screenshots/07-email.png` | The email flow and the success message |
| `screenshots/08-custom-command.png` | A custom command running |
| `screenshots/09-error-handling.png` | The "I didn't understand that" message |
| `screenshots/10-github-repo.png` | The OIBSIP repository page on GitHub |

## Demo Video

Demo video link: `[ADD YOUR DEMO VIDEO LINK HERE]`

## Testing Checklist

Fill in the "Actual result" column after running each test yourself.

| # | Input | Expected behavior | Actual result |
|---|---|---|---|
| 1 | "Hello" | Speaks and prints a greeting | |
| 2 | "What time is it?" | Speaks the current time in 12 hour format | |
| 3 | "What is today's date?" | Speaks the weekday, day, month and year | |
| 4 | "Search for Python programming" | Browser opens a Google search for "python programming" | |
| 5 | Mumble or stay silent while it listens | Says "I didn't understand that. Please try again." and keeps running | |
| 6 | "What is the weather in Hyderabad?" | Speaks the condition, temperature, feels like and humidity | |
| 7 | "What is machine learning?" | Speaks the knowledge base answer | |
| 8 | "Remind me after 10 seconds to check my internship task" | Confirms the reminder, then announces it after 10 seconds | |
| 9 | "Send an email" | Asks for recipient, subject and message, reads them back, then sends after "yes" | |
| 10 | "Open my portfolio" | Browser opens the link from `commands.json` | |
| 11 | "Exit" | Says goodbye and closes the program | |

Extra checks worth running:

| # | Input | Expected behavior | Actual result |
|---|---|---|---|
| 12 | Weather request with `OPENWEATHER_API_KEY` empty | Says the weather key is not configured | |
| 13 | "What is the weather in Xyzabc?" | Says it could not find weather information for that place | |
| 14 | "Send an email" with `.env` email values empty | Says email is not configured | |
| 15 | "Help" | Lists built in commands and custom commands | |
| 16 | Ctrl+C while running | Says goodbye and exits cleanly | |

## Future Improvements

These are ideas for later; they are **not** part of the current implementation.

- Offline speech recognition (for example Vosk) so audio never leaves the computer
- Saving reminders to a file so they survive a restart
- A larger knowledge base, or a Wikipedia lookup as a fallback
- Multi language support
- A simple graphical interface instead of the terminal
- A wake word such as "Hey Assistant" so it only responds when called

## Author

**[YOUR NAME]**
OASIS INFOBYTE SIP Internship — Python Programming, Task 1

## OASIS Task Requirement Checklist

- [x] Voice input using speech_recognition
- [x] Greeting response
- [x] Current time
- [x] Current date
- [x] Web search
- [x] Graceful speech/error handling
- [x] pyttsx3 text-to-speech
- [x] Natural-language understanding
- [x] Voice email using smtplib
- [x] Timed reminder
- [x] Live weather API
- [x] General knowledge / local knowledge base
- [x] Custom commands
- [x] Privacy documentation
