# COMP S351F Software Project Management - ChatMate - AI Chatbot For Educational Use
## Project Overview
ChatMate is an AI-powered WeChat chatbot (v3.28) that integrates with large language models to provide intelligent automated conversations. Built with Python and Flask, it supports multi-user/group chat with independent AI personas, advanced memory management, and web UI configuration.
<img width="400" height="600" alt="_cgi-bin_mmwebwx-bin_webwxgetmsgimg__ MsgID=8631460246398693010 skey=@crypt_40c08e15_5b4c8b0218899ecafc675faa2a828c28 mmweb_appid=wx_webfilehelper" src="https://github.com/user-attachments/assets/c7f476d0-3f5f-47c7-af08-e2e1b32bd622" />

### Key Features
- **Multi-user/group chat support** with independent AI personas (Prompt per user)
- **Image and emoji recognition** with emotion-based emoji responses (9 emotion categories)
- **Long-term memory system** with importance-based scoring and automatic summarization
- **Web search integration** and URL content extraction
- **Scheduled reminders** with optional voice call notifications
- **Flask-based Web UI** for configuration management (no manual file editing needed)
- **Character roleplay forum** for interactive conversations
- **Auto-message system** for proactive conversations
- **Complete thread management** (8 concurrent threads for scalability)

## Tech Stack
| Component | Technology |
|-----------|-----------|
| Language | Python 3.9 - 3.12 |
| Web Framework | Flask 3.1.0 + Flask-CORS |
| AI Integration | OpenAI SDK 1.84.0 (compatible with DeepSeek, Gemini, GPT, and any OpenAI-compatible API) |
| WeChat Automation | wxautox4_wechatbot (private library, included in `libs/`) |
| Data Storage | SQLAlchemy + JSON file persistence |
| GUI Automation | PyAutoGUI + pywin32 |

## System Requirements
- **OS:** Windows 10/11 (required - uses Windows COM and registry)
- **Python:** 3.9 - 3.12 (installer provided: `installers/python-3.11.9-amd64.exe`)
- **WeChat:** Version 4.1.2 (installer provided: `installers/微信4.1.2.exe`)
- **API Key:** From any OpenAI-compatible LLM provider (e.g., DeepSeek, OpenAI, Google Gemini via proxy)

## Demo Video
📹 **A demo video has been included in this repository:** `demo_video.mp4`

Watch the demo video to see the bot in action, including:
- Multi-user conversation handling
- Emoji response generation based on emotion detection
- Web UI configuration interface
- Automated message processing and responses

## Setup Instructions

### Step 1: Install Python
1. Run `installers/python-3.11.9-amd64.exe`
2. **IMPORTANT:** Check "Add Python to PATH" during installation
3. Verify: open Command Prompt, run `python --version` (should show 3.11.9)

### Step 2: Install WeChat
1. Run `installers/微信4.1.2.exe` to install WeChat Desktop
2. Log in to your WeChat account and keep WeChat running in background
3. (Optional) In WeChat Settings, enable "Auto-transcribe voice messages" for voice message support

### Step 3: Configure the Bot
1. Navigate to `WeChatBot_WXAUTO_SE-3.28/`
2. Open `config.py` in a text editor and configure the following:

| Setting | What to Change | Example |
|---------|---------------|---------|
| `DEEPSEEK_API_KEY` | Replace `YOUR_API_KEY_HERE` with your API key | `'sk-xxxxxxxxxxxx'` |
| `DEEPSEEK_BASE_URL` | Your API provider's base URL | `'https://api.deepseek.com'` (for DeepSeek official) |
| `MODEL` | The LLM model name | `'deepseek-chat'` or `'gpt-4o'` |
| `LISTEN_LIST` | WeChat display name + prompt file name | `[['John', 'Chat_Agent']]` |
| `MOONSHOT_API_KEY` | API key for image recognition (can be same key) | `'sk-xxxxxxxxxxxx'` |
| `ONLINE_API_KEY` | API key for web search (can be same key) | `'sk-xxxxxxxxxxxx'` |
| `ASSISTANT_API_KEY` | API key for auxiliary model (can be same key) | `'sk-xxxxxxxxxxxx'` |

> **Note:** All 4 API keys can use the same key if your provider supports the required models.

### Step 4: Start the Bot
1. Double-click `Run.bat` in the `WeChatBot_WXAUTO_SE-3.28/` folder
2. The script will automatically:
   - Check WeChat and Python versions
   - Install Python dependencies from `libs/` folder
   - Check for program updates (requires internet; safe to skip if offline)
   - Launch the Web UI configuration editor
3. A browser window will open at **http://localhost:5000**
4. In the Web UI, click **"Start Bot"** (top-right) to activate the chatbot
5. Send a message to the bot's WeChat account from another device to test

### Step 5: Customize (Optional)
- **Edit prompts:** Modify files in `prompts/` folder or use the Web UI "Prompt Management" page
- **Add emojis:** Place `.gif`/`.png`/`.jpg` files in `emojis/{emotion}/` subdirectories
- **Adjust behavior:** Use the Web UI to change auto-message timing, memory settings, etc.

## Directory Structure
```
COMP_S351F_Software_Project_Management_ChatMate/
├── README.md                          -- Main project documentation
├── demo_video.mp4                     -- Demo video showing bot functionality
├── installers/                        -- Runtime installers
│   ├── python-3.11.9-amd64.exe       -- Python interpreter (26 MB)
│   └── 微信4.1.2.exe                 -- WeChat Desktop (212 MB)
└── WeChatBot_WXAUTO_SE-3.28/         -- Main application
    ├── bot.py                         -- Core bot logic (4390 lines, message handling, AI calls, memory)
    ├── config.py                      -- All configuration settings (API keys removed for security)
    ├── config_editor.py               -- Flask Web UI for config editing and bot control
    ├── updater.py                     -- Auto-update mechanism (checks GitHub/Gitee)
    ├── Run.bat                        -- Startup script (dependency install + launch)
    ├── uninstall_all_packages.bat     -- Utility to clean pip packages
    ├── requirements.txt               -- Python dependency list
    ├── version.json                   -- Version metadata
    ├── chat_contexts.json             -- Runtime chat history (starts empty)
    ├── recurring_reminders.json       -- Scheduled reminders data
    ├── readme.md                      -- Original project documentation (Chinese)
    ├── CHANGELOG.md                   -- Version change history
    ├── LICENSE                        -- GNU GPL-3.0 license
    ├── LICENSE_COMPLIANCE.md          -- License compliance details
    ├── DEPENDENCIES.txt               -- Third-party dependency licenses
    ├── templates/                     -- Flask HTML templates
    │   ├── config_editor.html         -- Main configuration UI
    │   ├── character_forum.html       -- Character forum page
    │   ├── login.html                 -- Login page
    │   └── quick_start.html           -- Quick start guide
    ├── prompts/                       -- AI system prompts (character definitions)
    │   ├── 371_agent.md               -- Custom agent prompt
    │   └── Chat_Agent.md              -- Default educational assistant prompt
    ├── emojis/                        -- Emotion-based emoji packs (9 categories, 27 GIFs)
    ├── libs/                          -- Pre-packaged Python wheel dependencies (46 packages)
    ├── Demo_Image/                    -- Application screenshots
    ├── CoreMemory/                    -- Long-term AI memory storage (generated at runtime)
    ├── Memory_Temp/                   -- Temporary chat logs (generated at runtime)
    └── forum_data/                    -- Character forum data (generated at runtime)
```

## Architecture Overview
```
User (WeChat) <---> wxautox4_wechatbot <---> bot.py (Message Handler)
                                                 |
                                    +------------+------------+
                                    |            |            |
                              LLM API     Memory System   Web UI
                           (DeepSeek/    (CoreMemory/    (Flask on
                            GPT/Gemini)  Memory_Temp)    port 5000)
```

**Threading Model:** The bot runs 8 concurrent threads:
1. Main Thread (Flask web server)
2. Message Listener (receives WeChat messages)
3. Message Processor (per-user queue processing)
4. Auto-Message Checker (proactive messaging)
5. Reminder Handler (scheduled reminders)
6. Inactive User Checker (idle detection)
7. Keep-Alive Thread (web API heartbeat)
8. Log Handler Worker (async HTTP logging)

## Troubleshooting

| Problem | Solution |
|---------|---------|
| `Run.bat` shows "Python not found" | Reinstall Python with "Add to PATH" checked, then restart terminal |
| WeChat version check fails | Ensure WeChat 4.1.2 is installed (not portable version); the script will skip the check after 3 seconds |
| "API key invalid" error | Verify your API key and base URL in `config.py` match your provider |
| Bot not responding to messages | Check that `LISTEN_LIST` username exactly matches the WeChat display name |
| Web UI won't open | Check if port 5000 is available; change `PORT` in `config.py` if needed |
| Update check fails | Normal if offline; the bot will continue to start regardless |

## Security Note
All API keys have been removed from `config.py` and replaced with `YOUR_API_KEY_HERE` placeholders. You must insert valid API keys before running the bot.

## Project Statistics
- **Language Composition:** Python (55.1%), HTML (43.9%), Batch scripting (1%)
- **Main Application:** 4390+ lines of core logic
- **Threading:** 8 concurrent threads for optimal performance
- **Emoji Support:** 27 GIFs across 9 emotion categories
- **Dependencies:** 46 pre-packaged Python wheels included
