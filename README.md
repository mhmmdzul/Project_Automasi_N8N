# 🤖 Praja Assistant Chatbot — n8n AI Agent

A Telegram chatbot for IPDN cadets (*praja*) built with an **n8n AI agent** and **Google Gemini**. Cadets chat in natural language to look up their data, find learning resources, and get help with routine tasks — the agent decides which tool to use, from Google Sheets lookups to sending Gmail messages and creating Google Calendar events.

> Built solo during my internship at **Institut Pemerintahan Dalam Negeri (IPDN)** — Data Management & Information Systems Unit, July 2025. Status: **prototype**.

![Workflow](screenshots/chatbot-praja-workflow.jpg)

## 🧩 Problem

- Assignments are posted on IPDN's **Learning Management System (LMS)**, but the LMS sends **no notifications** — cadets can easily miss deadlines, especially while off campus.
- Reporting **attendance, permission, or sick leave** to supervisors (*pembina*) is still manual.
- Everyday information is scattered across different spreadsheets.

## 💡 Solution

A Telegram bot backed by an n8n AI agent:

1. **Telegram Trigger** receives every message sent to the bot.
2. The **AI Agent** (Google Gemini + short-term conversation memory) understands the request and picks the right tool.
3. **Tools** the agent can use:

   | Tool | Purpose |
   |---|---|
   | `data_praja` (Google Sheets) | Look up a cadet's class or hometown by NPP |
   | `list_kebutuhan_praja` (Google Sheets) | Find learning resources, e.g. Docker installation tutorials |
   | `gmail_praja` (Google Sheets) + Gmail | Send an email to every address on the cadet mailing list |
   | `Tanggal_Penting_Sigap` (Google Sheets) | Check important dates and leadership agendas |
   | Google Calendar | Create events from a natural-language message |
   | Date & Time | Resolve relative dates such as "tomorrow" |

4. The reply is sent back to the cadet through **Telegram**.

## 📸 Demo

| Looking up data & resources | Email & calendar actions |
|---|---|
| ![Chat 1](screenshots/chatbot-praja-chat-1.jpg) | ![Chat 2](screenshots/chatbot-praja-chat-2.jpg) |

*Personal data (NPP) in the screenshots has been blurred.*

## 🛠️ Tech Stack

n8n · Google Gemini · Telegram Bot API · Google Sheets · Gmail API · Google Calendar API · Docker

## 🚀 How to Run

1. Run n8n with Docker:
   ```bash
   docker run -it --rm -p 5678:5678 -v n8n_data:/home/node/.n8n n8nio/n8n
   ```
2. Open `http://localhost:5678`, then **Workflows → Import from File** and choose `workflow/project_bot_praja.json`.
3. Create your own credentials in n8n: **Telegram** (token from @BotFather), **Google Gemini** API key, and **Google** OAuth for Sheets, Gmail, and Calendar.
4. In every Google Sheets node, replace `YOUR_SPREADSHEET_ID` with your own spreadsheet ID; in the Gmail and Calendar nodes, replace `your-email@example.com`.
5. Activate the workflow and start chatting with your bot on Telegram.

> ⚠️ Never commit the `n8n-data/` folder — it contains your encryption key and credentials.

## 🗺️ Roadmap

- [ ] Scheduled reminders for new LMS assignments and upcoming deadlines
- [ ] Attendance, permission, and sick-leave reporting to supervisors (*pembina*)

## 👤 Author

**Muhammad Zul Rezky Zaaki** — [GitHub](https://github.com/mhmmdzul) · [LinkedIn](https://linkedin.com/in/muhammadzulrezkyzaaki)
