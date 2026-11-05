# Coding agent integrations

Craft Anything can use coding agents that expose the Agent Client Protocol (ACP). Each agent runs
as its own local process, keeps its own provider credentials, and receives Craft Anything's MCP
server for the current project. Sign in with the agent itself before starting a build.

## Supported ACP agents

| Agent | Program | ACP arguments | Notes |
|---|---|---|---|
| Devin CLI | `devin` | `acp` | Local Devin CLI; cloud hand-off and account features remain Devin's own |
| OpenCode | `opencode` | `acp` | Open-source, multi-provider agent; use its own provider setup |
| Cline CLI | `cline` | `--acp` | Open-source CLI; supports provider and model selection in Cline |
| Kilo Code | `kilo` | `acp` | Open-source CLI with BYOK and local-provider options |
| Kimi Code | `kimi` | `acp` | Kimi Code CLI; authenticate with `kimi login` |
| Gemini CLI | `gemini` | `--experimental-acp` | Existing integration |
| Qwen Code | `qwen` | `--experimental-acp` | Existing integration |
| Goose | `goose` | `acp` | Existing integration |
| Hermes Agent | `hermes` | `acp` | Existing integration |
| GitHub Copilot CLI | `copilot` | `--acp --stdio` | Existing integration |
| Maki | `maki` | `acp` | Existing integration |
| Antigravity | `agy` | Native adapter | Existing integration |

The program must be installed and available on `PATH`. If it is installed elsewhere, select its
executable in **Settings → AI**. For remote backends, install and authenticate the agent on the
SSH host and set its remote program there.

## Install and authenticate

Follow each project's current installation instructions. Typical package commands are:

```sh
# Cline
npm install -g cline

# Kilo Code
npm install -g @kilocode/cli
kilo

# Kimi Code
# Install using the official Kimi Code CLI instructions, then:
kimi login

# OpenCode
# Install using the official OpenCode instructions, then:
opencode auth login
```

Devin CLI is installed using Cognition's official installer. Run `devin` once and complete its
sign-in flow. Devin is not a free/open-source agent; availability and usage depend on the Devin
account or plan.

## Cost and model access

Craft Anything does not provide model credits for these agents. The agent uses its own account,
API keys, provider configuration, or local model server. Open-source software can be free while
the model provider still charges for inference. OpenCode, Cline, Kilo and Kimi can be configured
with providers supported by their own installations, including local or BYOK options where
available. Provider free tiers and quotas can change independently of Craft Anything.

## OpenCode model selection

OpenCode is already integrated, including model catalogue discovery. Its native
`opencode run` path cannot yet attach this build's temporary Craft Anything MCP server when an
explicit model or thinking depth is selected. Until native MCP setup is implemented, use ACP
with OpenCode's default model, or clear the explicit model/thinking selection and enable ACP.
See [OpenCode setup](opencode.md) for the current details.

## Permissions

ACP agents report tool permissions through the protocol. Craft Anything routes supported
permission requests to its own approval UI. Agent-specific safety modes and account policies
still apply; review the agent's own permission settings before enabling unattended execution.
