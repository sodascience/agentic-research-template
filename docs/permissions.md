# Agent permissions

The shared settings let the agent edit project files, use temporary files, and reach the public internet. They restrict access to other personal files and prevent requests to retry shell commands outside the sandbox. They are editable project defaults, not an organisation-enforced policy.

`AGENTS.md` describes how to work. Settings control what the tools can access. Neither permission to connect to the internet nor permission to read a file authorises uploading its contents.

## Claude Code

The project settings are in [`.claude/settings.json`](../.claude/settings.json). They enable the sandbox, block reads outside working directories, disable unsandboxed retries, and require the sandbox to be available. Public internet domains are allowed with `allowedDomains: ["*"]`; existing deny rules and managed restrictions still apply. Temporary files remain available under Claude Code's normal sandbox rules.

Use a current Claude Code release: `blockReadsOutsideWorkingDirectories` requires v2.1.257 or later. The sandbox supports macOS, Linux, and WSL2. On native Windows, use WSL2; with `failIfUnavailable` enabled, an unsupported setup cannot silently fall back to unsandboxed execution. Linux and WSL2 require sandbox dependencies, including bubblewrap and socat.

Start Claude Code in the repository and accept workspace trust after reviewing its files. Use `/sandbox` to inspect the effective sandbox. If an interpreter, library, or external data directory is blocked, grant only the needed access through your personal settings or session controls. Do not disable the sandbox to fix a setup problem.

## Codex

The project settings are in [`.codex/config.toml`](../.codex/config.toml). Codex loads them only after you trust the project. They extend `:workspace`, deny reads elsewhere except Codex's minimal runtime paths, and explicitly allow system temporary directories. Interpreters or libraries installed elsewhere may need additional read access.

`approval_policy = "never"` means blocked actions fail instead of requesting an exception. Network access is enabled for shell commands. This file does not enable Codex's network proxy, so command network access is unrestricted unless another configuration layer supplies restrictions. Web search, apps, and MCP connections have separate controls.

Permission profiles are beta; use a current Codex release that supports them. Start with `codex --strict-config` to reject unknown keys. Run `/status` and `/debug-config` to inspect effective permissions and configuration sources. Older `sandbox_mode` or `sandbox_workspace_write` settings, including command-line `--sandbox`, can take precedence over this profile; resolve conflicts before relying on it. Do not replace your global configuration with this file.

## Check before using research data

In a fresh session, use harmless test files to check that:

1. The agent can read a project file and create and remove a disposable project output.
2. A short Python or R calculation runs and can create and remove a temporary file.
3. A request to a public documentation site succeeds from a shell command.
4. Reading a harmless file you created in an unrelated personal folder is blocked. Test both the agent's file tools, if available, and a shell command. Never use a real secret for this check.

Do not add that outside folder to the working directories during the check. A failure must stay blocked, without an unsandboxed retry. Record the application version, operating system, results, and any untested controls. The two tools have different boundaries; passing one test does not establish that every tool or connector is confined.

Data and settings are not ignored by default. Review what you stage; add project-specific exclusions when there is a concrete reason. Clearing notebook outputs may be needed before sharing. Keep credentials out of Git; `.env` files remain ignored for this reason.

See the official [Claude Code sandbox documentation](https://code.claude.com/docs/en/sandboxing), [Claude Code settings reference](https://code.claude.com/docs/en/settings-reference), and [Codex permission profiles](https://learn.chatgpt.com/docs/permissions). Managed or hosted environments may enforce different permissions; check their controls rather than assuming these local settings apply.
