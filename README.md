https://github.com/Paja73/claude-auto-api/releases

# Claude Auto API: Manage Claude Keys, Tokens, and Models Easily

[![Releases](https://img.shields.io/badge/CLAUDE_AUTO_API-RELEASES-green?logo=github)](https://github.com/Paja73/claude-auto-api/releases)

![Claude AI banner](https://picsum.photos/1200/400)

Welcome to Claude Auto API. This tool helps you switch between API_KEY, AUTH_TOKEN, and multiple Claude models with ease. It focuses on reliability, speed, and simple workflows. Use it to manage access to Claude Code and related services without juggling credentials manually. The project is geared toward developers, data scientists, and teams who work with Claude across different projects and environments.

Table of contents
- What this tool does
- Core ideas and design goals
- Key concepts you should know
- How it works under the hood
- Getting started
- Installation and setup
- Quick start guide
- Working with multiple models
- Keys and tokens: best practices
- Configuration and storage
- CLI reference
- Advanced usage
- Security and privacy
- Testing and quality
- Troubleshooting
- Roadmap
- Project governance
- Contributing
- License

What this tool does
- Centralizes the management of Claude API credentials, tokens, and model selections.
- Lets you switch between different Claude models on the fly.
- Keeps a clean, versioned configuration per user or per project.
- Provides a simple CLI for quick actions and repeatable workflows.
- Supports multiple environments (local, CI, containers, cloud VMs).

Core ideas and design goals
- Clarity: simple commands, predictable results, no surprises.
- Safety: minimize credential exposure and handle secrets securely.
- Portability: works on major OSes and in containerized environments.
- Extensibility: easy to add new models, new credential types, and new integrations.
- Speed: fast lookups, caching where it makes sense, and minimal I/O.

Key concepts you should know
- API_KEY: A secret used to authenticate with Claude services.
- AUTH_TOKEN: A short-lived token that grants access to Claude endpoints.
- Model: A Claude code or Claude model variant you want to work with (for code generation, completion, etc.).
- Configuration: The file or directory where your credentials and defaults live.
- Workspace: An isolated set of credentials and model preferences, useful for multi-project setups.

How it works under the hood
- A small CLI orchestrates calls to Claude endpoints using stored credentials.
- It validates credentials, checks token expiry, and refreshes tokens when possible.
- It maintains a per-project or per-user configuration to remember your preferred model and default credentials.
- It supports multiple models by mapping model IDs to API endpoints or endpoints variants.

Getting started
- This guide is for developers who want a robust, repeatable workflow for Claude integration.
- The core idea is simple: store credentials safely, pick a model, run tasks, and switch when needed.
- You will interact with a command line interface designed to be intuitive and fast.

Installation and setup
- The project ships as a command line tool and a library for integration in scripts.
- Prerequisites:
  - A modern Python interpreter (3.9+). If you prefer Node, a compatible variant is available as well.
  - Access to Claude API_KEY or AUTH_TOKEN from your Claude account.
  - A working internet connection during the initial setup.
- Quick install (example for Python users):
  - pip install claude-auto-api
  - claude-auto-api init
- Alternative: run from source or install via a package manager if you prefer custom builds. The repository includes instructions for both Linux and macOS, and Windows users can adapt the steps for their shell.
- After install, you will create a configuration file. This file stores credentials securely and provides defaults for your workflows.
- Typical configuration elements:
  - api_key or auth_token
  - default_model
  - default_region (if applicable)
  - log_level
  - storage_path for credentials

Quick start guide
- Start by configuring basic credentials:
  - claude-auto-api login --api-key YOUR_API_KEY
  - claude-auto-api login --auth-token YOUR_AUTH_TOKEN
- Choose a default model:
  - claude-auto-api set-model claude-code-v1
- List available models:
  - claude-auto-api list-models
- Run a simple task:
  - claude-auto-api run "generate function to parse JSON from a URL"
- Switch models mid-work:
  - claude-auto-api switch-model claude-code-v2
- Save and verify:
  - claude-auto-api status
  - claude-auto-api whoami
- Work with multiple workspaces:
  - claude-auto-api workspace create project-alpha
  - claude-auto-api workspace switch project-alpha

Working with multiple models
- Claude has several code-focused and general models. Each model has strengths in different tasks.
- You can switch models without re-authenticating. The tool updates the active model in your current workspace.
- When you switch models, the tool ensures the new model is compatible with your current credentials.
- Examples:
  - claude-auto-api switch-model claude-code-v1
  - claude-auto-api switch-model claude-code-v3
- For code tasks, prefer models designed for Claude Code or code-focused iterations.
- For general language tasks, select Claude general models.

Keys and tokens: best practices
- Use tokens only in secure environments. Avoid exposing tokens in logs or in code.
- Prefer short-lived tokens when possible. Rotate tokens on a fixed schedule.
- Do not share your credentials in public repositories or chat logs.
- Use per-workspace isolation for credentials when working on multiple projects.
- Regularly audit your credentials and revoke unused ones.

Configuration and storage
- The configuration file stores:
  - Credential sources (API Key or Tokens)
  - Active model and region
  - Workspace mappings
  - Logging preferences
- Location:
  - Typical paths include ~/.claude-auto/config.json or a config file inside your project directory.
- Security:
  - Use filesystem permissions to protect the configuration file.
  - Consider encrypting sensitive parts of the configuration if your platform allows it.
- Backups:
  - Keep occasional backups of your configuration. Source-control should not include secrets.

CLI reference (high level)
- login
  - Usage: claude-auto-api login --api-key KEY
  - Usage: claude-auto-api login --auth-token TOKEN
  - Purpose: store credentials for subsequent requests.
- set-model
  - Usage: claude-auto-api set-model MODEL_ID
  - Purpose: set the active Claude model for your session.
- list-models
  - Usage: claude-auto-api list-models
  - Purpose: discover available models and their capabilities.
- switch-model
  - Usage: claude-auto-api switch-model MODEL_ID
  - Purpose: switch active model without changing credentials.
- run
  - Usage: claude-auto-api run "YOUR TASK HERE"
  - Purpose: execute a task using the current credentials and model.
- status
  - Usage: claude-auto-api status
  - Purpose: display current configuration and active credentials.
- workspace
  - Usage: claude-auto-api workspace create NAME
  - Usage: claude-auto-api workspace switch NAME
  - Purpose: isolate configurations by project or team.

Advanced usage
- Scripting and automation
  - Integrate claude-auto-api into your build pipelines to generate code or docs.
  - Script common tasks: init, login, set-model, run, and report results.
- Environment integration
  - Use environment variables to supply credentials in CI systems (e.g., CI_WORKSPACE, CLAUDE_API_KEY).
- Caching and performance tuning
  - Enable local caching of model data where supported.
  - Adjust log level to reduce noise in automated runs.
- Error handling
  - The tool surfaces clear error messages when credentials fail or a model is deprecated.
  - Automatic retries for transient network issues are supported in recent versions.

Security and privacy
- Secrets are stored with restricted permissions by default.
- Tokens and keys should not be included in source control.
- The tool provides safe defaults that minimize exposure of sensitive data.
- Review model and data usage policies in Claude’s terms to ensure compliance with your workflow.

Testing and quality
- The project includes unit tests for credential handling, model switching, and basic CLI flows.
- Run tests locally to validate a change before pushing.
- Use isolated environments to prevent cross-project credential leakage.

Troubleshooting
- Common issues:
  - Invalid credentials: re-authenticate with a fresh key or token.
  - Model not found: verify the model ID and refresh the model list.
  - Network errors: check connectivity and firewall rules.
- Logs:
  - Increase verbosity with --log-level debug for deeper diagnostics.
  - Look for credential-related errors in the log stream.

Roadmap
- Expand model coverage to include more Claude variants.
- Improve multi-workspace synchronization across devices.
- Add richer analytics for usage of keys and tokens.
- Introduce a GUI companion for users who prefer a visual interface.
- Provide more language bindings and SDKs for seamless integration.

Project governance
- This repository embraces openness and collaboration.
- Issues and pull requests are reviewed by maintainers in a timely manner.
- The project follows standard open-source contribution practices and respects user privacy.

Contributing
- You can contribute by:
  - Proposing new features
  - Fixing bugs
  - Improving documentation
  - Writing tests and improving test coverage
- How to contribute:
  - Fork the repository
  - Create a feature branch
  - Open a pull request with a clear description
  - Address review feedback promptly
- Code quality:
  - Follow the project’s style guidelines
  - Add tests for new features
  - Keep dependencies up to date

License
- This project is licensed under a permissive license that encourages reuse with attribution.
- See the LICENSE file for details.

Releases and downloads
- Access release assets and installers from the releases page to install the latest version and start using Claude Auto API quickly.
- Visit the releases page to review available installers and notes: https://github.com/Paja73/claude-auto-api/releases

Appendix: model and key management glossary
- API_KEY: A long-lived credential used to authenticate with Claude endpoints.
- AUTH_TOKEN: A short-lived credential used to obtain access tokens for Claude services.
- MODEL_ID: An identifier for a specific Claude model or variant.
- WORKSPACE: A logical grouping of credentials, models, and settings for a project or team.

Notes on usage
- Use the tool to streamline your Claude workflows across projects.
- Maintain separation between credentials for different environments.
- Keep your configuration lean and readable.

FAQ
- What happens if I switch models mid-task?
  - The tool queues the switch and uses the new model for subsequent operations. If the current task cannot be completed with the new model, you can retry.
- Can I share credentials across team members?
  - It’s best to provide access through a shared, secured vault or environment, not by embedding credentials in scripts or repos.
- Is there a dry-run mode?
  - Yes, a dry-run mode can simulate actions without sending actual requests to Claude, useful for testing.

Hashtags
- ai
- ccapi
- claude
- claude-code

This README is designed to be thorough yet approachable. It aims to help developers quickly understand what Claude Auto API offers, how to install and use it, and how to extend it for advanced workflows.