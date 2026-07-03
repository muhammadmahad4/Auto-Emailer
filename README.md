# Auto Emailer

Auto Emailer helps job-seekers turn a list of leads — a job-postings webpage or a spreadsheet of contacts — into personalized outreach emails, sent straight from your own Gmail account.

You give it a URL or an Excel file plus a bit about yourself (school, major, skills, why you're reaching out). It scrapes or parses the leads, pulls out contact emails, and drafts a personalized email using an AI model. You review and edit the draft on a confirmation screen, then send it via Gmail — no email ever leaves your account without your say-so.

## How it works

1. **Provide leads** — paste a URL to a job/contact listing, or upload an `.xlsx`/`.xls` file of contacts.
2. **Add your details** — name, institution, major, relevant experience, skills, and purpose of outreach.
3. **Extraction & drafting** — the backend scrapes the page (or reads the spreadsheet), extracts email addresses, and generates a subject + body using an AI model, while you wait it out with a quick trivia quiz.
4. **Sign in with Google** — authorize Gmail send access for your own account (nothing is sent through a third-party mail server).
5. **Review & send** — edit the subject, body, and recipient list on the confirmation page, then send.

## Tech stack

**Frontend** — React 18 + Vite, `react-router-dom`, `@react-oauth/google`, Axios
**Backend** — Node.js (Express), Multer (file uploads), Cheerio + Axios (scraping), `xlsx` (spreadsheet parsing), Hugging Face Inference API (email extraction & generation)

## Project structure

```
AutoEmailer/
├── front-end/     React + Vite single-page app
└── back-end/      Express API (scraping, parsing, AI email generation)
```

## Getting started

### Prerequisites

- Node.js 18+
- A [Google Cloud OAuth client ID](https://console.cloud.google.com/apis/credentials) with the Gmail `gmail.send` scope enabled
- A [Hugging Face API token](https://huggingface.co/settings/tokens)

### Backend setup

```bash
cd back-end
npm install
```

Create a `.env` file in `back-end/` (see [Environment variables](#environment-variables) below), then:

```bash
npm run dev   # starts the API on http://localhost:8000 with auto-reload
```

### Frontend setup

```bash
cd front-end
npm install
npm run dev   # starts the dev server, typically on http://localhost:5173
```

Run both servers at once, in separate terminals, for local development.

### Environment variables

The backend reads the following from `back-end/.env`:

| Variable | Description |
|---|---|
| `PORT` | Port the API listens on (defaults to `8000`) |
| `HF_API_TOKEN` | Hugging Face Inference API token, used for email extraction and generation |
| `MONGODB_USERNAME` | MongoDB username |
| `MONGODB_PASSWORD` | MongoDB password |

The frontend currently uses a Google OAuth client ID configured directly in `front-end/src/main.jsx` — swap in your own client ID before running.

> **Note:** Never commit real credentials to `.env` files or source code. Use placeholder values in version control and keep actual secrets local or in your deployment platform's secret manager.

## Deployment

The backend includes an `app.yaml` for deployment to Google App Engine.

## License

No license has been set for this project yet.
