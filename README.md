# Agilai

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Node.js Version](https://img.shields.io/badge/node-%3E%3D20.10.0-brightgreen)](https://nodejs.org)

## The Problem

**Building software with AI should be simple. Instead, it's overwhelming.**

You have an idea. You open Claude, ChatGPT, or Codex. Then what?

- Do you write a Product Requirements Document first?
- Should you create user stories?
- What about technical architecture?
- How do you break work into manageable pieces?
- Where do you even start?

**Most developers waste hours figuring out _how_ to ask AI for help** instead of actually building their project.

Meanwhile, professional teams use structured agile methodologies (analyst → PM → architect → developer → QA) that produce better results. But learning these frameworks takes weeks and adds friction you don't need.

## The Solution

**Agilai gives you professional agile workflows through natural conversation.**

Just talk about your project. The system:

✅ **Understands** what you're trying to build (no framework jargon needed)
✅ **Generates** professional deliverables automatically (PRD, architecture, user stories)
✅ **Guides** you through proven development phases (analyst → PM → architect → dev → QA)
✅ **Adapts** to complexity (quick templates for simple tasks, full workflows for complex features)

**You focus on your ideas. Agilai handles the methodology.**

## Why It Works

- **Zero learning curve** - Chat naturally, no methodology training required
- **Proven framework** - Built on BMAD-METHOD™, a battle-tested agile AI development process
- **Intelligent routing** - Automatically picks the right approach for each task
- **Professional output** - Generates documentation that matches industry standards
- **Local-first** - Works with Claude CLI, Codex CLI, or OpenCode - your choice
- **No API costs** - Runs through your existing CLI tooling

### ⚡ Supercharge Your AI in 30 Seconds

**Extend Agilai with any tool through MCP (Model Context Protocol) integration:**

```bash
# Add GitHub integration
npm run mcp:install github
# ✓ Your AI can now create issues, PRs, and review code!

# Add database access
npm run mcp:install postgres
# ✓ Your AI can now query and manage your database!

# Add filesystem access
npm run mcp:install filesystem
# ✓ Your AI can now read, write, and search files!
```

**Popular integrations** (15+ available):

- 🐙 **GitHub** - Create issues, manage PRs, review code
- 🗄️ **PostgreSQL** - Query databases, manage schemas
- 📁 **Filesystem** - Read, write, search project files
- 🌐 **Puppeteer** - Browser automation, E2E testing
- 🔍 **Brave Search** - Web search integration
- 💬 **Slack** - Team notifications and collaboration
- ☁️ **AWS** - Cloud resource management

**Or get smart suggestions:**

```bash
npm run mcp:suggest
# 🔍 Analyzing your project...
# 💡 Recommended: github, postgres, filesystem
# Install all? (y/n)
```

→ **See [MCP Management Guide](docs/mcp-management.md) for complete integration examples**

### 🚀 NEW: Dual-Lane Orchestration (v1.2+)

Agilai intelligently routes tasks between two development approaches:

- **Complex Lane**: Full multi-agent BMAD workflow for substantial features
- **Quick Lane**: Template-based rapid development for small, focused tasks

The orchestrator automatically selects the appropriate lane based on task complexity. Simple typos and config changes go through the fast Quick lane, while complex features get the full BMAD treatment. Both lanes output to the same `docs/` folder - the only difference is _how_ the artifacts are generated.

→ **See [DUAL_LANE_ORCHESTRATION.md](docs/DUAL_LANE_ORCHESTRATION.md) for details**

## 🔥 Quick Start

### Prerequisites

- Node.js ≥ 20.10.0
- npm ≥ 9.0.0

- At least one chat CLI installed locally:
  - **OpenAI Codex CLI**
  - **Claude CLI**
  - **OpenCode CLI**

### Installation

#### Option 1: NPX One-Command Setup (Easiest!)

```bash
# Just run this - it does everything!
npx agilai@latest start
```

> Prefer a specific CLI? Append `--assistant=claude`, `--assistant=codex`, or `--assistant=opencode` to skip the prompt. Add `--glm`
> (or the explicit `--llm-provider=glm`) to swap the orchestrator to ZhipuAI's GLM using the `ZHIPUAI_API_KEY`/`GLM_API_KEY`
> credentials. Use `--anthropic` (or `--llm-provider=claude`) anytime you want to switch back to the Anthropic defaults.

That's it! This command will:

- Create project structure
- Install all dependencies
- Prompt you to choose between Claude, Codex, or OpenCode
- Launch the selected chat interface

> **UI Tooling Opt-in**: If you enable the optional shadcn UI helpers during the
> wizard, the installer also writes a `components.json` in your project root.
> This file follows the [shadcn/ui schema](https://ui.shadcn.com/docs/installation)
> (`style`, `tailwind`, `aliases`, etc.) so downstream tooling like
> `npx shadcn@latest add button` can pick up your preferences without extra
> prompts.

> **💡 Tip**: Always use `@latest` to ensure you get the newest version!

#### Option 1b: NPX Step-by-Step

```bash
# Initialize in your project directory
npx agilai@latest init

# Install dependencies
npm install


# Start chatting through your preferred CLI
npm run bmad              # Prompts you to choose assistant
# Force GLM for the orchestrator (requires ZHIPUAI_API_KEY or GLM_API_KEY)
# npm run bmad -- --glm
# OR use explicit commands:
# npm run bmad:claude     # Claude front-end (respects --glm/--anthropic)
# npm run bmad:codex      # Codex front-end (respects --glm/--anthropic)
# npm run bmad:opencode   # OpenCode front-end (respects --glm/--anthropic)

```

#### Option 2: Global Installation

```bash
# Install globally
npm install -g agilai

# Initialize in any project
agilai init

# Build
agilai build

# Start chat (will prompt for assistant choice)
# Add --glm / --llm-provider=glm to default to ZhipuAI GLM
agilai start

```

#### Option 3: Local Development

```bash
# Clone the repository
git clone https://github.com/bacoco/Agilai.git
cd Agilai

# Install dependencies
npm install

# Build the MCP server
npm run build:mcp

# Start conversational interface (prompts for choice)
npm run bmad
# OR: npm run bmad:claude / bmad:codex / bmad:opencode
```

> **MCP assets are prebuilt**: The published package already includes `dist/mcp`, so installs without dev dependencies (for example on Windows or production hosts) can skip rebuilding during `npm install`. The optional postinstall step only re-runs the TypeScript build when `typescript` is available.

> **Note**: This uses the Model Context Protocol (MCP) so you can work locally without managing API keys.

#### Choosing Your LLM Provider (GLM vs Anthropic)

- Run any CLI command with `--glm` (or the explicit `--llm-provider=glm`) to switch the orchestrator to ZhipuAI's GLM stack.
- Provide credentials via environment variables – `ZHIPUAI_API_KEY` is preferred, but `GLM_API_KEY` is also detected automatically.
- Optional model overrides can be set with `--llm-model=<model>` or by exporting `LLM_MODEL`.
- Persist defaults in a `.env` file at your project root:

  ```bash
  # .env
  LLM_PROVIDER=glm
  ZHIPUAI_API_KEY=sk-...
  LLM_MODEL=glm-4-plus   # Optional custom model
  ```

- To switch back to Anthropic at any time, pass `--anthropic` on the CLI or set `LLM_PROVIDER=claude` in your environment.
- The launcher never mutates your shell environment; overrides are injected only into the spawned CLI process.

#### Codex CLI Integration

Interactive installs now auto-provision Codex CLI so you can run `codex` immediately after setup:

- Generates/updates `AGENTS.md` with BMAD agent context for Codex memory.
- Ensures `~/.codex/config.toml` exists with the `agilai` MCP server
  entry plus optional helpers for `chrome-devtools` and `shadcn` (disabled by
  default until you install them).
- Applies sensible defaults (`GPT-5-Codex` model, medium reasoning, automatic approvals) unless you have overrides.

Non-interactive environments (like CI) skip the global config step, but you can review and customize the defaults via [`codex-config.toml.example`](./codex-config.toml.example).

> **MCP Config Formats at a Glance**
>
> - **Claude / Claude Code** reads `.claude/mcp-config.json`. Entries are JSON
>   objects keyed by server name, and optional servers such as
>   `chrome-devtools` and `shadcn` simply set `disabled: true` until you toggle
>   them on.
> - **Codex CLI** reads `~/.codex/config.toml`. Each MCP server is declared in a
>   TOML table (`[mcp_servers.bmad_invisible]`, `[mcp_servers.chrome_devtools]`,
>   etc.) with `auto_start` flags mirroring the JSON `disabled` switches.

## 📖 How It Works

### The Invisible Flow

```
User: "I want to build an app"
  ↓
[Analyst Phase - Hidden]
  ↓
Assistant: "What problem are you trying to solve?"
  ↓
[Gathers requirements through conversation]
  ↓
Assistant: "Here's what I understand... [shows summary]"
  ↓
User: validates or iterates
  ↓
[PM Phase - Hidden]
  ↓
Assistant: "Here's the development plan..."
  ↓
[Architecture Phase - Hidden]
  ↓
Assistant: "Here's the technical approach..."
  ↓
[Continues through all phases invisibly]
```

## 💡 Usage Examples

Run `npm run bmad` to be prompted for your choice, or use explicit commands (`npm run bmad:claude`, `npm run bmad:codex`, `npm run bmad:opencode`). The experience looks like this:

### Example 1: Simple App Project

````bash
$ npm run bmad
Which assistant should we launch? (Claude / Codex / Opencode): claude

🎯 Starting Agilai Orchestrator...
📡 MCP Server: agilai-orchestrator
🤖 Agent: Agilai Orchestrator
💬 Type your project idea to begin!

Welcome! I'm here to help you build your project.
What would you like to create?

> I need an app for tracking family chores

Great! Let's figure this out together.
Who will be using this app?

> Parents and kids, ages 8 and up

Perfect. What does success look like?

> Everyone knows their tasks and chores actually get done

Makes sense. Any constraints I should know about?
(Budget, timeline, technical preferences?)

> Need it in 3 months, prefer mobile-first

📋 Let me summarize what I understand:

**Project**: Family Chore Tracking App
**Users**: Parents & children (8+)
**Goal**: Clear task visibility and completion
**Timeline**: 3 months
**Platform**: Mobile-first

Is this correct? (y/n/edit)

> y

Perfect! Based on this, here's a 12-week development plan:

**Phase 1 (Weeks 1-4): Core Features**
- Task creation and assignment
- User profiles (parent/child roles)
- Basic completion tracking

**Phase 2 (Weeks 5-8): Engagement**
- Reward points system
- Notifications
- Progress visualization

**Phase 3 (Weeks 9-12): Polish**
- Testing and refinement
- Performance optimization
- User onboarding flow

Does this approach work for you? (y/n/modify)

> y

Excellent! Now for the technical approach.

**Recommended Stack**:
- Mobile: React Native (iOS + Android from one codebase)
- Backend: Firebase (real-time sync, authentication)
- Database: Firestore (flexible, scalable)
- Hosting: Firebase Hosting

**Why this stack?**
- Faster development (built-in features)
- Real-time updates (perfect for family coordination)
- Lower cost to start
- Easy to scale later

Sound good, or prefer something else? (y/n/modify)

> Sounds perfect

Great! Let me break this into specific tasks.

**Epic 1: Task Management** (3-4 weeks)
Story 1.1: Create and edit tasks ← Let's start here
Story 1.2: Assign tasks to family members
Story 1.3: Mark tasks complete

**Epic 2: User System** (2-3 weeks)
Story 2.1: Family member profiles
Story 2.2: Parent/child permissions

**Epic 3: Rewards** (2 weeks)
Story 3.1: Point tracking
Story 3.2: Rewards redemption

Ready to start with Story 1.1? (y/n)

> y

Perfect! Here's your first feature to build:

**Story 1.1: Create and Edit Tasks**

**What users can do**:
- Tap "+" to create new task
- Enter: task name, description, points (1-5)
- Optionally set due date
- Save and see task in list immediately

**Technical Implementation**:

1. **Component**: `TaskForm.jsx`
   ```javascript
   // Key fields
   - taskName (required)
   - description (optional)
   - points (1-5, default: 3)
   - dueDate (optional)
````

2. **Firestore Structure**:

   ```javascript
   tasks/{taskId}
   {
     name: string,
     description: string,
     points: number,
     dueDate: timestamp,
     createdBy: userId,
     assignedTo: userId,
     status: 'pending' | 'in-progress' | 'complete',
     createdAt: timestamp
   }
   ```

3. **Implementation Steps**:
   - [ ] Create TaskForm component
   - [ ] Add form validation
   - [ ] Implement Firestore write
   - [ ] Add real-time listener
   - [ ] Show success/error feedback

**Acceptance Criteria**:

- ✓ Can create task with all fields
- ✓ Task appears instantly in list
- ✓ Empty names are prevented
- ✓ Handles offline gracefully

**Testing**:

- Create task with all fields → appears in list
- Try empty name → shows validation error
- Create while offline → syncs when back online

Want the complete code examples or ready to implement? (code/ready)

> ready

Awesome! When you're done, let me know and I'll help you:

- Review the implementation
- Add tests
- Move to the next story

Type 'done' when ready for review, or 'help' if you get stuck.

````

### Example 2: Adding a Feature to Existing Project

```bash
$ npx agilai chat --project ./my-app

I see you have an existing project. What would you like to add?

> I need to add push notifications

Perfect! Let me understand what you need.

What should trigger these notifications?

> When a task is assigned or due soon

Great. Who should receive them?

> The person assigned to the task

Makes sense. Any preferences on implementation?

> Use Firebase Cloud Messaging

📋 Here's what I'll help you build:

**Feature**: Push Notifications
**Triggers**:
  - Task assigned to user
  - Task due in 24 hours
**Recipients**: Assigned user only
**Technology**: Firebase Cloud Messaging (FCM)

Correct? (y/n)

> y

Perfect! This will integrate with your existing Firebase setup.

**Story: Push Notifications for Tasks**

**Implementation Plan**:

1. **FCM Setup** (30 minutes)
   - Add FCM to React Native
   - Request notification permissions
   - Store device tokens in Firestore

2. **Cloud Function Triggers** (1 hour)
   - Trigger on task assignment
   - Trigger on approaching due date
   - Send to user's registered devices

3. **In-App Handling** (30 minutes)
   - Handle notification tap
   - Navigate to task details
   - Update UI accordingly

**Files to Modify**:
- `src/services/notifications.js` (new)
- `functions/index.js` (add triggers)
- `src/screens/TaskList.jsx` (handle taps)
- `app.json` (FCM config)

Want detailed code for each step? (y/n)

> y

[Provides step-by-step implementation with code examples]

Once you're done, I'll help you test it thoroughly!
````

## ⚙️ Configuration

### GLM Provider Support

Agilai supports routing requests through GLM (or other Anthropic-compatible) endpoints. This allows you to use alternative LLM providers while maintaining compatibility with Claude, Codex, and OpenCode CLIs.

#### Environment Variables

Set `BMAD_ASSISTANT_PROVIDER=glm` to enable GLM routing. The system will automatically configure the environment for Anthropic-compatible GLM endpoints.

**GLM Configuration Priority** (first available value is used):

| Variable               | Priority | Description                              |
| ---------------------- | -------- | ---------------------------------------- |
| `BMAD_GLM_BASE_URL`    | 1        | GLM API base URL (BMAD-specific)         |
| `GLM_BASE_URL`         | 2        | GLM API base URL (standard)              |
| `ANTHROPIC_BASE_URL`   | 3        | Anthropic base URL (fallback)            |
| `BMAD_GLM_AUTH_TOKEN`  | 1        | GLM authentication token (BMAD-specific) |
| `GLM_AUTH_TOKEN`       | 2        | GLM authentication token (standard)      |
| `ANTHROPIC_AUTH_TOKEN` | 3        | Anthropic auth token (fallback)          |
| `BMAD_GLM_API_KEY`     | 1        | GLM API key (BMAD-specific)              |
| `GLM_API_KEY`          | 2        | GLM API key (standard)                   |
| `ANTHROPIC_API_KEY`    | 3        | Anthropic API key (fallback)             |

**Note:** At least one of `*_BASE_URL` or `*_API_KEY` must be set when using GLM mode.

When no GLM base URL variables are provided, requests default to `https://open.bigmodel.cn/api/paas/v4/chat/completions`. Custom
base URLs may include schemes, ports, and nested paths (e.g., `https://example.com:7443/custom/base`), and the client will append
the `/api/paas/v4/chat/completions` endpoint automatically.

#### Usage Example

```bash
# Set GLM provider and credentials
export BMAD_ASSISTANT_PROVIDER=glm
export BMAD_GLM_BASE_URL=https://your-glm-endpoint.com
export BMAD_GLM_API_KEY=your-api-key

# Start BMAD with GLM routing
npm run bmad:claude
# Output: 🌐 GLM mode active: routing Claude CLI through configured GLM endpoint.
```

GLM routing works with all three assistant CLIs:

- `npm run bmad:claude` - Routes Claude CLI through GLM
- `npm run bmad:codex` - Routes Codex CLI through GLM
- `npm run bmad:opencode` - Routes OpenCode CLI through GLM

## 🛠️ Current Status

**FULLY IMPLEMENTED AND PRODUCTION-READY** ✅

Agilai v1.2 is a complete, working system that combines:

- Full BMAD methodology integration (Complex lane)
- Template-based rapid development (Quick lane)
- Intelligent automatic routing
- Professional deliverable generation
- Natural conversational interface

### What's Working Right Now

✅ **MCP-based orchestration** with 10 tools
✅ **Dual-lane routing** - automatic complexity detection
✅ **BMAD integration** - full agent/template/task support
✅ **Quick lane** - template-based generation (2-3 min)
✅ **Quick lane graceful fallback** - automatically routes to complex lane if disabled
✅ **Complex lane** - complete BMAD workflow (10-15 min)
✅ **Deliverable generation** - PRD, architecture, stories
✅ **State persistence** - resume anytime
✅ **CLI interface** - `npm run codex`
✅ **Zero API costs** - powered by local OpenAI Codex CLI session

## 🏗️ Architecture

### Components

```
agilai/
├── agents/                    # Agent definitions
│   ├── invisible-orchestrator.md  # Main conversational interface
│   └── phase-detector.md          # Phase classification engine
├── commands/                  # Phase-specific commands
│   ├── auto-analyze.md        # Analyst phase execution
│   ├── auto-plan.md           # PM phase execution
│   ├── auto-architect.md      # Architecture phase execution
│   ├── auto-stories.md        # Story breakdown phase
│   ├── auto-dev.md            # Development guidance phase
│   ├── auto-qa.md             # Quality assurance phase
│   ├── auto-ux.md             # UX refinement phase
│   └── auto-po.md             # Product owner review phase
├── hooks/                     # Phase management
│   ├── phase-transition.js    # Handles phase transitions
│   └── context-preservation.js # Maintains context across phases
├── mcp/                       # Model Context Protocol server
│   └── server.ts              # StdIO entry point → shared runtime
├── src/mcp-server/            # Shared runtime + Codex bridge
│   ├── runtime.ts             # Orchestrator wiring
│   └── codex-server.ts        # Codex-aware entry point (routing & approvals)
└── test/                      # Test suite
    ├── phase-detector.contract.test.js
    └── phase-transition.safety.test.js
```

### Phase Flow

1. **Analyst**: Understand problem, users, goals
2. **PM**: Create plan, timeline, milestones
3. **Architect**: Design technical approach
4. **SM**: Break into epics and stories
5. **Dev**: Implementation guidance
6. **QA**: Testing and validation
7. **UX**: Usability refinement
8. **PO**: Final review and launch

All phases execute invisibly based on conversation context.

## 🏗️ Architecture

### MCP-Powered Design

```
User → Codex CLI → MCP Server → BMAD Agents → Deliverables
                     ↓
              Project State
              Phase Detection
              Context Preservation
```

**Key Components:**

- **MCP Server** (`mcp/server.ts`) - 10 orchestration tools
- **Project State** (`lib/project-state.js`) - Conversation & state tracking
- **BMAD Bridge** (`lib/bmad-bridge.js`) - Integration with BMAD agents
- **Deliverable Generator** (`lib/deliverable-generator.js`) - Creates docs automatically

**Low API Overhead** - Runs through your local CLI tooling. ZhipuAI's GLM only needs `ZHIPUAI_API_KEY`/`GLM_API_KEY`; Anthropic
defaults continue to work via the Claude CLI with no direct API billing.

## 🔧 Development Setup

```bash
# Install dependencies
npm install

# Build MCP server
npm run build:mcp

# Run tests
npm test

# Start standalone MCP server (optional)
npm run mcp
```

### Codex CLI MCP bridge

Register the Codex-aware MCP server with `npx agilai-codex` in your `~/.codex/config.toml`:

```toml
[[mcp]]
id = "agilai-codex"
command = "npx"
args = ["agilai-codex"]
autostart = true

  [mcp.env]
  # Optional: enforce guarded writes and approve individual operations
  CODEX_APPROVAL_MODE = "true"
  CODEX_APPROVED_OPERATIONS = "generate_deliverable:prd,execute_quick_lane"
  # Optional: override LLM routing per lane
  CODEX_QUICK_MODEL = "gpt-4.1-mini"
  CODEX_COMPLEX_MODEL = "claude-3-5-sonnet-20241022"
  # Observability knobs (JSON logs + optional metrics)
  CODEX_LOG_CONTEXT = '{"environment":"local"}'
  CODEX_METRICS_STDOUT = "true"
```

Refer to [`codex-config.toml.example`](codex-config.toml.example) for a ready-to-copy snippet and additional options.

#### Observability & metrics

- **Structured JSON logs** — The MCP server and Codex bridge now emit newline-delimited JSON to `stderr`. Every entry contains the event `msg`, timestamp, and metadata such as `lane`, `confidence`, `operation`, and measured `durationMs` so you can trace lane selection, approvals, and tool execution.
- **Context enrichment** — Provide a JSON blob via `CODEX_LOG_CONTEXT` to stamp shared fields (e.g., `environment`, `cluster`, `team`) onto every log entry without code changes.
- **Lightweight metrics** — Set `CODEX_METRICS_STDOUT=1` to mirror timing metrics (lane selection, workflow durations, tool runtimes) to `stdout` as JSON events. The helper supports adding additional sinks if you need to forward metrics to a collector.

Example log line:

```json
{
  "ts": "2024-07-16T12:34:56.789Z",
  "level": "info",
  "msg": "lane_selection_completed",
  "service": "bmad-codex",
  "component": "mcp-orchestrator",
  "operation": "execute_workflow",
  "lane": "quick",
  "confidence": 0.88,
  "durationMs": 142.3,
  "environment": "local"
}
```

## 🔌 MCP Integration: Extend Your AI with Any Tool

Agilai includes a comprehensive **Model Context Protocol (MCP) management system** for seamless AI tool integration. Add powerful capabilities to your AI in seconds, not hours.

### 🎯 Real-World Examples

#### Example 1: Add GitHub Integration

```bash
# Install GitHub MCP server
npm run mcp:install github

# Interactive prompts:
# ? GitHub Personal Access Token: ghp_****
# ✓ GitHub server configured!

# Now your AI can:
# • Create and manage issues
# • Review and create pull requests
# • Search repositories
# • Manage branches and releases
```

**Use it naturally:**

```
You: "Create a GitHub issue for the login bug"
AI: ✓ Created issue #42: "Fix login authentication error"
```

#### Example 2: Add Database Access

```bash
# Install PostgreSQL server
npm run mcp:install postgres

# Configure connection:
# ? Database URL: postgresql://localhost/myapp
# ✓ PostgreSQL server ready!

# Now your AI can:
# • Query your database
# • Generate SQL from natural language
# • Analyze schema and relationships
# • Suggest optimizations
```

**Use it naturally:**

```
You: "Show me all users who signed up this week"
AI: [Executes query and shows results]
    Found 47 users. The top registration day was Tuesday.
```

#### Example 3: Add Filesystem Access

```bash
# Install filesystem server
npm run mcp:install filesystem

# ? Root directory: /Users/me/projects/myapp
# ✓ Filesystem access configured!

# Now your AI can:
# • Read and write project files
# • Search across your codebase
# • Analyze file structure
# • Refactor code safely
```

**Use it naturally:**

```
You: "Find all TODO comments in the codebase"
AI: Found 23 TODO items across 8 files.
    The oldest is from 3 months ago in auth.js
```

### 📦 Available MCP Servers (15+)

**Development Tools:**

- 🐙 `github` - GitHub API integration
- 📁 `filesystem` - File system operations
- 🔧 `git` - Git repository management
- 🦊 `gitlab` - GitLab integration
- 🎭 `puppeteer` - Browser automation
- 🎬 `playwright` - E2E testing

**Databases:**

- 🐘 `postgres` - PostgreSQL database
- 💾 `sqlite` - SQLite database
- 🧠 `memory` - In-memory storage

**Cloud & Services:**

- ☁️ `aws-kb-retrieval` - AWS knowledge base
- 🌐 `cloudflare` - Cloudflare API
- 💬 `slack` - Slack integration
- 🐛 `sentry` - Error tracking

**Search & AI:**

- 🔍 `brave-search` - Web search
- 🌍 `fetch` - HTTP requests
- 🔎 `everything` - Local search

### 🚀 Quick Commands

```bash
# Browse all available servers
npm run mcp:browse

# Get smart suggestions for your project
npm run mcp:suggest
# 🔍 Analyzing project...
# 💡 Recommended: github, postgres, filesystem

# Install a server
npm run mcp:install <server-name>

# List configured servers
npm run mcp:list

# Health check all servers
npm run mcp:doctor

# Search for specific capabilities
npm run mcp:search "database"

# Manage environment profiles
npm run mcp:profile:create production
npm run mcp:profile:switch production

# Security
npm run mcp:secure     # Encrypt credentials
npm run mcp:audit      # Security audit
```

### 💬 Conversational Installation

The Agilai orchestrator can install MCP tools through natural conversation:

```
You: "I need to access my database"
AI: I can help with that! What database are you using?

You: "PostgreSQL"
AI: Great! I'll set up PostgreSQL access.
    What's your database connection string?

You: "postgresql://localhost/myapp"
AI: ✓ PostgreSQL MCP server configured and ready!
    You can now ask me to query your database naturally.

You: "Show me the users table schema"
AI: [Shows table schema with columns and types]
```

### 🎯 Common Workflows

**Full-Stack Development:**

```bash
npm run mcp:install filesystem github postgres puppeteer
# ✓ Complete development environment ready!
```

**API Development:**

```bash
npm run mcp:install filesystem postgres brave-search
# ✓ Backend API tools configured!
```

**Frontend Development:**

```bash
npm run mcp:install filesystem github puppeteer
# ✓ Frontend development tools ready!
```

**DevOps:**

```bash
npm run mcp:install git github aws-kb-retrieval slack
# ✓ DevOps automation configured!
```

**📖 Complete Documentation**:

- **[MCP Management Guide](docs/mcp-management.md)** - Detailed command reference and best practices
- **[MCP Examples](docs/mcp-examples.md)** - Real-world integration workflows
- **[Environment Profiles](docs/mcp-management.md#environment-profiles)** - Multi-environment setup
- **[Security Guide](docs/mcp-management.md#security)** - Credential management and encryption

## 📚 Documentation

- **[QUICKSTART.md](QUICKSTART.md)** - ⭐ Start here! Quick installation and first use
- **[docs/mcp-management.md](docs/mcp-management.md)** - ⚡ Complete MCP integration guide
- **[docs/mcp-examples.md](docs/mcp-examples.md)** - 🎯 Real-world MCP integration examples
- **[USAGE.md](USAGE.md)** - Complete usage guide with examples
- **[DUAL_LANE_ORCHESTRATION.md](docs/DUAL_LANE_ORCHESTRATION.md)** - 🆕 Intelligent routing system
- **[IMPLEMENTATION_COMPLETE.md](IMPLEMENTATION_COMPLETE.md)** - Complete feature list
- **[CLAUDE.md](CLAUDE.md)** - Guide for Claude Code development
- **[BMAD-METHOD™](https://github.com/bmadcode/bmad-method)** - Core framework

## ✅ Current Status

**FULLY IMPLEMENTED AND WORKING!**

### What Works Now

✅ MCP-based orchestration with 10 tools
✅ Codex CLI integration (no API costs)
✅ Natural conversation interface
✅ Phase detection and transitions
✅ Deliverable generation (PRD, architecture, stories)
✅ Project state persistence
✅ User validation checkpoints
✅ Full BMAD agent integration
✅ Quick lane gracefully disables and defers to complex lane when unavailable

### How to Use

```bash
# Start conversation (prompts for assistant choice)
npm run bmad

# Natural conversation
> I want to add user authentication

# System understands context, generates artifacts
# No need to know about PRDs, architectures, stories, etc.
```

### Generated Artifacts (Behind the Scenes)

```
my-project/
├── docs/
│   ├── brief.md               # From analyst phase
│   ├── prd.md                 # From PM phase
│   ├── architecture.md        # From architect phase
│   ├── epics/
│   │   └── epic-1-auth.md     # From SM phase
│   └── stories/
│       ├── story-1-1-login.md # From SM phase
│       └── story-1-2-signup.md
└── .agilai/
    ├── state.json             # Current phase, context
    └── conversation.log       # Full conversation history
```

### User Validation Points

After each major phase:

```
Assistant: "Here's what I've created... [summary]"
           "Does this look good?"

Options:
- y: Continue to next phase
- n: Let me refine this
- edit: Make specific changes
- back: Go to previous phase
```

## 🚀 Future Enhancements

While fully functional, potential improvements include:

**Short Term:**

- Additional test coverage
- More example workflows
- Custom template support

**Medium Term:**

- Web UI for non-CLI users
- Multi-project management
- Team collaboration features

**Long Term:**

- Git integration hooks
- CI/CD pipeline generation
- Analytics dashboard

## 🤝 Contributing

We welcome contributions! Agilai is production-ready but can always be enhanced.

Key areas for contribution:

- Additional lane selector test cases
- Custom template variations
- Integration examples
- Performance optimizations
- Documentation improvements

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## 🔗 Related Projects

- **[BMAD-METHOD™](https://github.com/bmadcode/bmad-method)** - The core framework
- **[Model Context Protocol](https://modelcontextprotocol.io/)** - State persistence layer

## 📄 License

MIT License - see [LICENSE](LICENSE) for details.

## 🙏 Acknowledgments

Built on [BMAD-METHOD™](https://github.com/bmadcode/bmad-method) by Brian (BMad) Madison.

BMAD™ and BMAD-METHOD™ are trademarks of BMad Code, LLC.

---

**Current Version**: v1.3.5 - Production Ready ✅

**Get Started**: `npx agilai@latest start`

**Questions?** Open an issue or check the main [BMAD repository](https://github.com/bmadcode/bmad-method).

<sub>Making AI-assisted development accessible to everyone through natural conversation</sub>
