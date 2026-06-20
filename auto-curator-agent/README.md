# 🤖 DGX Spark Auto-Curator Agent

A Nemotron-powered Docker agent that automatically discovers new NVIDIA DGX Spark
resources every morning at **9:00 AM UTC** and submits pull requests to keep the
[awesome-dgx-spark](https://github.com/ajeetraina/awesome-dgx-spark) list current.

> Adapted from [collabnix/awesome-nvidia-nemotron](https://github.com/collabnix/awesome-nvidia-nemotron)
> and powered by **NVIDIA Nemotron Super 49B** running on [build.nvidia.com](https://build.nvidia.com).

---

## How It Works

```
Every morning at 9 AM UTC
         │
         ▼
  ┌─────────────────┐
  │  GitHub Actions │  (.github/workflows/daily-curator.yml)
  │  cron: 0 9 * * *│
  └────────┬────────┘
           │  docker agent run dgx-spark-curator.yaml
           ▼
  ┌─────────────────────────────────────────────────────┐
  │              ROOT AGENT (Nemotron Super 49B)        │
  │  Coordinator — orchestrates the full curation flow  │
  └──────┬──────────┬───────────┬──────────┬────────────┘
         │          │           │          │
         ▼          ▼           ▼          ▼
    ┌─────────┐ ┌──────────┐ ┌───────┐ ┌──────────┐
    │ FETCHER │ │DISCOVERER│ │VALID- │ │PUBLISHER │
    │         │ │          │ │ATOR   │ │          │
    │ Today's │ │ GitHub   │ │ Check │ │ Create   │
    │  DGX    │ │ HF Models│ │ URLs  │ │ branch + │
    │  news   │ │ arXiv    │ │ QA    │ │   PR     │
    │         │ │ Blogs    │ │       │ │          │
    └─────────┘ └──────────┘ └───────┘ └──────────┘
           │          │           │          │
           └──────────┴───────────┴──────────┘
                          │
                          ▼
              ┌───────────────────────┐
              │  PR: curator/daily-   │
              │  YYYY-MM-DD [agent]   │
              │  → adds new resources │
              │    to README.md       │
              └───────────────────────┘
```

### Agent Roles

| Agent | Model | Responsibility |
|---|---|---|
| **root** | Nemotron Super 49B | Coordinator — orchestrates the full curation flow |
| **fetcher** | Nemotron Super 49B | Fetches today's DGX Spark news from NVIDIA, Reddit, GitHub |
| **discoverer** | Nemotron Super 49B | Searches for new blogs, repos, models, papers, videos |
| **validator** | Nemotron Nano 8B | Validates URLs, checks content quality and relevance |
| **publisher** | Nemotron Super 49B | Creates dated branch and opens PR on GitHub |

---

## Prerequisites

### 1. NVIDIA API Key (free)

Get a free API key at [build.nvidia.com](https://build.nvidia.com):
1. Sign up for a free NVIDIA Developer account
2. Navigate to **build.nvidia.com → API Keys**
3. Generate a new key — the free tier includes enough credits for daily runs

### 2. GitHub Personal Access Token

Create a PAT at [github.com/settings/tokens](https://github.com/settings/tokens):
1. Click **Generate new token (classic)**
2. Give it a name: `awesome-dgx-spark-curator`
3. Select these scopes:
   - ✅ `repo` (full repo access — needed to push branches and open PRs)
4. Copy the token — you won't see it again

### 3. Docker with AI Agent support

```bash
# Install Docker Desktop (includes AI Agent CLI)
# https://docs.docker.com/desktop/

# Verify docker agent is available
docker agent --version
```

---

## Setup: GitHub Actions (Automated Daily Run)

### Step 1: Add repository secrets

Go to your fork → **Settings → Secrets and variables → Actions → New repository secret**:

| Secret Name | Value |
|---|---|
| `NVIDIA_API_KEY` | Your NVIDIA API key from build.nvidia.com |
| `GH_PAT` | Your GitHub Personal Access Token (with `repo` scope) |

### Step 2: Enable GitHub Actions

GitHub Actions is enabled by default on public repos. The workflow at
`.github/workflows/daily-curator.yml` will run automatically at **9:00 AM UTC every day**.

### Step 3: Verify the workflow

1. Go to the **Actions** tab in your repo
2. You should see **"Daily DGX Spark Curator"** listed
3. To test immediately: click the workflow → **Run workflow** → **Run workflow**

### Step 4: Review and merge PRs

The agent creates PRs like `curator/daily-2026-06-21`. Review each PR and
merge if the content looks good. The agent is conservative — it only adds
resources it is confident are high quality and DGX Spark-specific.

---

## Setup: Manual / Local Run

### Install dependencies

```bash
# Clone the repo
git clone https://github.com/ajeetraina/awesome-dgx-spark.git
cd awesome-dgx-spark

# Set environment variables
export NVIDIA_API_KEY=nvapi-your-key-here
export GITHUB_PERSONAL_ACCESS_TOKEN=ghp_your-token-here
```

### Run the agent

```bash
# Daily morning run — fetch news and add new resources
docker agent run ./auto-curator-agent/dgx-spark-curator.yaml \
  "Good morning! Fetch today's latest DGX Spark news and add any new resources to the awesome list"

# Find new tutorials and tools from the last week
docker agent run ./auto-curator-agent/dgx-spark-curator.yaml \
  "Find new DGX Spark tutorials, tools, and community projects from the last week"

# Check all links for broken URLs
docker agent run ./auto-curator-agent/dgx-spark-curator.yaml \
  "Check all links in the awesome list README.md for broken URLs"

# Search for new Nemotron models optimized for DGX Spark
docker agent run ./auto-curator-agent/dgx-spark-curator.yaml \
  "Search for new models and benchmarks published for DGX Spark on HuggingFace and GitHub"

# Find new academic papers featuring DGX Spark
docker agent run ./auto-curator-agent/dgx-spark-curator.yaml \
  "Find new research papers on arXiv that feature DGX Spark or GB10 Grace Blackwell"

# Create a PR with everything found
docker agent run ./auto-curator-agent/dgx-spark-curator.yaml \
  "Find new resources, validate them, and create a PR adding them to the awesome list"
```

---

## File Structure

```
awesome-dgx-spark/
├── README.md                          # The awesome list itself
├── auto-curator-agent/
│   ├── README.md                      # This file — setup instructions
│   └── dgx-spark-curator.yaml        # Docker agent definition (Nemotron-powered)
└── .github/
    └── workflows/
        └── daily-curator.yml          # GitHub Actions — runs at 9 AM UTC daily
```

---

## Models Used

| Task | Model | Why |
|---|---|---|
| Coordination, discovery, publishing | [Nemotron Super 49B](https://huggingface.co/nvidia/Llama-3.3-Nemotron-Super-49B-v1) | Best accuracy/throughput ratio for complex agentic tasks |
| Validation, link-checking | [Nemotron Nano 8B](https://huggingface.co/nvidia/Llama-3.1-Nemotron-Nano-8B-v1) | Fast, low-cost for simpler classification tasks |

Both models are accessed via the **NVIDIA API** at [build.nvidia.com](https://build.nvidia.com) —
an OpenAI-compatible endpoint. Free tier is sufficient for daily runs.

---

## Customization

### Change the schedule

Edit `.github/workflows/daily-curator.yml`:
```yaml
on:
  schedule:
    # Change '0 9 * * *' to your preferred time (UTC)
    # Examples:
    #   '0 9 * * *'   — 9:00 AM UTC daily
    #   '0 6 * * *'   — 6:00 AM UTC daily
    #   '0 9 * * 1'   — 9:00 AM UTC every Monday only
    - cron: '0 9 * * *'
```

### Change the model

Edit `dgx-spark-curator.yaml` under the `models:` section:
```yaml
models:
  smart:
    provider: nvidia
    # Options: nvidia/llama-3.3-nemotron-super-49b-v1
    #          nvidia/llama-3.1-nemotron-ultra-253b-v1   (more powerful, higher cost)
    #          nvidia/llama-3.1-nemotron-nano-8b-v1      (faster, lower cost)
    model: nvidia/llama-3.3-nemotron-super-49b-v1
```

### Add new search sources

Edit the `discoverer` agent's instruction section in `dgx-spark-curator.yaml`
to add new websites, GitHub topics, or HuggingFace search queries.

---

## Troubleshooting

| Problem | Solution |
|---|---|
| `NVIDIA_API_KEY not set` | Add the secret in repo Settings → Secrets → Actions |
| `docker agent: command not found` | Install Docker Desktop with AI Agent support |
| Agent creates PR with wrong content | Review the PR and close it; adjust discoverer instructions |
| Workflow not triggering | Check Actions tab is enabled; GitHub cron can delay up to 1 hour |
| Rate limit errors | NVIDIA free tier has daily limits; upgrade or reduce frequency |

---

## Credits

- Inspired by [collabnix/awesome-nvidia-nemotron](https://github.com/collabnix/awesome-nvidia-nemotron) auto-curator agent
- Powered by [NVIDIA Nemotron](https://www.nvidia.com/en-us/ai-data-science/products/nemotron/) models
- Built with [Docker AI Agent](https://docs.docker.com/ai-agent/) runtime
