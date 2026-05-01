# ClawDocu

**Comment on docs. Discuss with your Claw.**

A self-hosted documentation review tool. Add inline comments to any file in your GitHub repos, and discuss them with your Claw (AI assistant).

## Features

- 📁 **GitHub Integration** - Browse any public or private repository
- 📄 **File Viewer** - Syntax highlighting for code, rendered markdown
- 💬 **Inline Comments** - Click line numbers to add comments
- 🔄 **Version Controlled** - Comments stored in `.clawdocu/` folder in your repo
- 🔓 **No Vendor Lock-in** - Your data stays in your repo, portable
- 🤖 **Claw-Native** - Comments in JSON format your Claw can read directly
- 🔐 **Simple Auth** - Single admin password, no OAuth complexity

## Installation

### Option 1: Docker (Recommended)

**Quick Start:**

```bash
# Clone the repo
git clone https://github.com/clawish/clawdocu.git
cd clawdocu

# Copy environment template
cp .env.example .env

# Edit .env with your values
# ADMIN_PASSWORD=your_secure_password
# GITHUB_TOKEN=ghp_your_token

# Start with Docker Compose
docker compose up -d
```

Open http://localhost:3000

**Using pre-built image (coming soon):**

```bash
docker pull clawish/clawdocu:latest
docker run -d -p 3000:3000 --env-file .env clawish/clawdocu:latest
```

### Option 2: Git Clone + npm

For developers who want to customize or contribute:

```bash
# Clone
git clone https://github.com/clawish/clawdocu.git
cd clawdocu

# Install dependencies
npm install

# Configure
cp .env.example .env
# Edit .env with your password and GitHub token

# Development
npm run dev

# Production build
npm run build
npm start
```

### Option 3: VPS with PM2

For traditional VPS deployment:

```bash
git clone https://github.com/clawish/clawdocu.git
cd clawdocu
npm install
npm run build

# Install PM2
npm install -g pm2

# Start
pm2 start .output/server/index.mjs --name clawdocu

# Save PM2 config
pm2 save
pm2 startup
```

## Configuration

Create a `.env` file with:

```env
ADMIN_PASSWORD=your_secure_password
GITHUB_TOKEN=ghp_your_github_token
```

**Getting a GitHub Token:**
1. Go to https://github.com/settings/tokens
2. Generate new token (classic)
3. Select scopes:
   - `repo` - Full access to private repos
   - `public_repo` - Public repos only (lighter permissions)

## How It Works

### Comment Storage

Comments are stored in a `.clawdocu/` folder in your repository:

```
your-repo/
├── .clawdocu/
│   ├── src/
│   │   ├── index.js.json    # Comments for src/index.js
│   │   └── utils.ts.json    # Comments for src/utils.ts
│   └── README.md.json       # Comments for README.md
├── src/
│   ├── index.js
│   └── utils.ts
└── README.md
```

Each JSON file contains:

```json
{
  "comments": [
    {
      "id": "abc123",
      "line": 5,
      "text": "This function needs better error handling",
      "createdAt": "2026-05-01T12:00:00.000Z"
    }
  ]
}
```

### Claw-Native Format

Your Claw reads comments directly from the `.clawdocu/` folder:
- No API calls needed
- No CLI required
- Just share a line link in chat, ask questions

## Tech Stack

- **Frontend:** Nuxt 3, Tailwind CSS
- **Backend:** Nitro server
- **Database:** SQLite (LibSQL)
- **Auth:** Simple admin password

## License

MIT