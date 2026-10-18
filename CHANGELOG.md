# Changelog

## 0.1.5

- Uses the WorkBuddy Agent 0.1.7 release, whose package entry point disables Codex conversation restoration by default.
- Continues to pin a single stdio MCP server and disables the five unsupported attachment/video/audio tools.

## 0.1.4

- Uses the WorkBuddy Agent 0.1.6 release and requests Codex conversation restoration be disabled in the WorkBuddy-launched Agent.
- Keeps market descriptions within the currently verified canvas inspection scope.

## 0.1.0

- Initial WorkBuddy connector package using one local stdio MCP Server and a
  WorkBuddy Skill.
- Pins the shared SupDance Canvas Agent to the `v0.1.2` source release.
- Adds connection, canvas reading, prompt-flow guidance, privacy, and
  troubleshooting documentation.

## 0.1.3

- Pins the MCP server to the compact WorkBuddy Agent tarball at Agent version
  0.1.5, built from the shared Agent source. The WorkBuddy runtime package no
  longer downloads the Codex app-server dependency.
- Updates the MCP TypeScript SDK to 1.32.1 and locks its production dependency
  tree with npm-shrinkwrap.json after security audit.
- Pins Zod to a complete published build (3.25.76) and verifies the clean
  install can import the MCP tool schema.
- Resizes the supplied logo to the WorkBuddy recommended 64×64 PNG size.
