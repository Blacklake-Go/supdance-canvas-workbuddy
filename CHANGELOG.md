# Changelog

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
