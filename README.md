# Daily Research Agent

An AI-powered research agent that runs automatically every morning. It researches your chosen topic, writes a report, saves it to Google Drive, and emails you the summary.

Built with [Claude Code](https://docs.anthropic.com/en/docs/claude-code) and [Valyu DeepSearch](https://docs.valyu.network/).

## Quick Setup (5 minutes)

### 1. Copy this template

Click the green **"Use this template"** button above, then **"Create a new repository"**. Name it whatever you like and click **Create repository**.

### 2. Edit your config

In your new repository, click on **config.md**, then click the **pencil icon** to edit. Change these three things to your own:

- **What to research** — your topic of interest
- **My email** — where reports get sent
- **Google Drive folder** — where reports get saved

Click **Commit changes** when done.

### 3. Add your API keys

Go to **Settings** > **Secrets and variables** > **Actions** > **New repository secret**.

Add these two secrets:

| Name | Value |
|------|-------|
| `ANTHROPIC_API_KEY` | Your Anthropic API key from [console.anthropic.com](https://console.anthropic.com/) |
| `VALYU_API_KEY` | Your Valyu API key from [valyu.network](https://valyu.network/) |

### 4. Test it

Go to the **Actions** tab > click **"Daily Research Agent"** on the left > click **"Run workflow"** > **"Run workflow"**.

Wait a few minutes, then check your inbox.

## Changing Things

| I want to... | Do this |
|---|---|
| Change the topic | Edit `config.md` (pencil icon) |
| Run it right now | Actions tab > Run workflow |
| Pause it | Actions tab > click workflow > **Disable workflow** |
| Resume it | Actions tab > click workflow > **Enable workflow** |
| Change the schedule | See below |

## Changing the Schedule

Edit `.github/workflows/research.yml` and find the `cron:` line:

```yaml
- cron: '0 12 * * 1-5'
```

Common schedules:

| Schedule | Cron value |
|---|---|
| Every weekday at 7 AM ET | `0 12 * * 1-5` |
| Every day at 7 AM ET | `0 12 * * *` |
| Every Monday at 9 AM ET | `0 14 * * 1` |
| Twice a day (7 AM and 2 PM ET) | `0 12,19 * * *` |

The times are in UTC. To convert: ET = UTC - 5, CT = UTC - 6, PT = UTC - 8.

## How It Works

Every morning on your schedule:

1. GitHub Actions starts a cloud server
2. Claude Code reads your `config.md`
3. It searches for the latest research using Valyu DeepSearch
4. It writes a structured report
5. It creates a Google Doc with the full report
6. It emails you the summary with a link to the Doc
7. The server shuts down (you're not charged for idle time)

You don't need to keep your computer on. Everything runs in the cloud.
