# AIVoterGuide

**Nonpartisan AI that explains ballot measures in plain language — without telling you how to vote.**

[aivoterguide.org](https://www.aivoterguide.org)

---

## What is this?

AIVoterGuide is an open-source, AI-powered ballot guide that helps everyday voters understand propositions and how they impact that voter and their community.

Ballot propositions are written by lawyers in legal jargon. AIVoterGuide translates them into plain English — explaining what each measure does and how it impact individual voters and their communities. It presents all sides neutrally and never tells users how to vote.

---

## Pilot: King County, WA — February 10, 2026

This repository contains the pilot version of AIVoterGuide, built for the King County, Washington Special Election on February 10, 2026. The pilot was launched with zero paid marketing and served 150+ users in the days leading up to the election. User feedback was consistently positive — voters reported cutting their ballot research time from several hours to under 30 minutes.

---

## How it works

1. **Ballot data** is curated from official election sources and structured in `ballot-data.js`
2. **A system prompt** (`prompt.txt`) instructs the AI to remain nonpartisan, cite sources inline, and stay grounded in the official data — never hallucinating facts or URLs
3. **A lightweight Node.js proxy** (`server.js`) routes requests to the Anthropic Claude API, keeping the API key server-side and out of the browser
4. **A single-page frontend** (`index.html`) provides the chat interface with no framework dependencies

The system prompt is publicly available at [aivoterguide.org/prompt.txt](https://www.aivoterguide.org/prompt.txt) — full transparency into how the AI is instructed to behave.

---

## Adapting for your county or state

AIVoterGuide is designed to be redeployable for any election. To adapt it:

### 1. Replace the ballot data
Edit `ballot-data.js` with your jurisdiction's measures. Each measure includes:
- Proposition title and district
- Explanatory statement
- Arguments for and against (with submitters)
- Levy details (rates, years, amounts) or bond details
- Contact information

Source your data from official election authority materials — voters' pamphlets, measure resolution texts, and official election websites.

### 2. Update the system prompt
Edit `prompt.txt` to reference your jurisdiction, election date, and official URLs. Key things to update:
- Jurisdiction name and election date
- Official ballot measure URL format
- Scope restrictions (what the AI should and shouldn't discuss)
- Any jurisdiction-specific voting logistics

### 3. Set your API key
Copy `.env.example` to `.env` and add your Anthropic API key:
```
ANTHROPIC_API_KEY=your_key_here
```

### 4. Update the frontend
In `index.html`, update the title, header text, district list, and data source links to match your jurisdiction.

### 5. Run it
```bash
node server.js
```
Then open `index.html` in a browser or serve it as a static file.

---

## Project structure

```
├── index.html        # Frontend chat interface (no framework dependencies)
├── server.js         # Node.js proxy server (keeps API key server-side)
├── ballot-data.js    # Structured ballot measure data
├── prompt.txt        # Public system prompt governing AI behavior
├── .env.example      # Template for environment variables
└── .gitignore        # Excludes API keys and local tooling
```

---

## Design principles

- **Nonpartisan by design** — the system prompt explicitly prohibits advocacy or persuasion
- **Grounded, not generative** — the AI is instructed to draw only from `ballot-data.js` and official sources, never to invent facts or URLs
- **Transparent** — the system prompt is publicly published so anyone can audit how the AI behaves
- **Privacy-first** — no user data or conversation history is stored
- **Open source** — built to be forked, localized, and improved by civic technologists everywhere

---

## Roadmap

- [ ] Multilingual support
- [ ] Statewide coverage for California and Washington November 2026 elections
- [ ] Engage local officials, target 20% of voters engagement

---

## License

Apache 2.0 

---

## Contributing

Pull requests welcome. If you're adapting this for a new jurisdiction, open an issue and we'll help you get set up. Civic technologists, researchers, and election administrators are especially encouraged to reach out.
