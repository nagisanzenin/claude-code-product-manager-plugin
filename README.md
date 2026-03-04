# Product Manager Plugin for Claude Code

AI Product Manager that interviews stakeholders, writes BRDs/PRDs, and autonomously verifies engineering implementation against business requirements.

## What it does

- **Interviews you as CEO** — 3-5 focused questions to nail down requirements
- **Writes BRD/PRD docs** — Creates a `BRD/` folder in your project with structured requirement docs
- **Researches the domain** — Uses web search when the domain is unfamiliar
- **Verifies implementation** — Autonomously spawns agents to check code against acceptance criteria
- **Tracks multiple features** — Each feature gets its own doc, all tracked via `BRD/INDEX.md`

## Installation

### Via Marketplace (Recommended)

```bash
# Add the marketplace (one time)
/plugin marketplace add nagisanzenin/nagisanzenin-plugins

# Install the plugin
/plugin install product-manager@nagisanzenin
```

### Org-Wide Auto-Install

Add to your project's `.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "nagisanzenin": {
      "source": {
        "source": "github",
        "repo": "nagisanzenin/nagisanzenin-plugins"
      }
    }
  },
  "enabledPlugins": {
    "product-manager@nagisanzenin": true
  }
}
```

Everyone on the project gets the plugin automatically.

### Load Directly (for testing)

```bash
claude --plugin-dir /path/to/product-manager-plugin
```

## Usage

The skill triggers automatically when you describe a new feature or business requirement:

```
> I want to add a payment system to my SaaS app
> We need user authentication with SSO
> New feature: export reports to PDF
```

Or invoke directly:

```
/product-manager:product-manager
```

## Workflow

1. **Interview** — Quick focused questions to understand the feature
2. **Research** — Online research if domain is unfamiliar
3. **Write BRD** — Structured doc with acceptance criteria and business rules
4. **Approve** — CEO reviews and approves the BRD
5. **Verify** — Autonomous agents check implementation against BRD

## Output

Creates in your project root:

```
BRD/
  INDEX.md                       # Living table of contents
  YYYY-MM-DD-feature-name.md     # One doc per feature
```

### BRD Document Sections

Each feature doc includes:

- **Problem Statement** — What problem and for whom
- **Proposed Solution** — High-level approach
- **User Stories** — As a [role], I want [action] so that [benefit]
- **Acceptance Criteria** — Testable Given/When/Then format
- **Business Rules** — Unambiguous logic for engineers
- **Out of Scope** — What this feature does NOT include
- **Research Notes** — Competitor analysis, domain context

### Verification

The PM autonomously spawns verification agents that compare your implementation against BRD acceptance criteria, reporting:

- **PASS** — Criterion met (cites the code)
- **FAIL** — Criterion not met (explains what's missing)
- **PARTIAL** — Partially implemented (explains gap)

BRD status tracks through: `Draft` → `Approved` → `In Progress` → `Verified` → `Done`

## License

MIT
