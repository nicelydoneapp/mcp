# Nicelydone

Find real web app screens, UI elements, and user flows for design research.
This plugin connects to the hosted [Nicelydone MCP](https://nicelydone.club/mcp).

## Requirements

- A Nicelydone account with active premium access.
- A client that supports remote HTTP MCP servers and OAuth.
- Internet access to `https://mcp.nicelydone.club/mcp`.

Connect your own account through the client's OAuth flow. The plugin package
contains no credentials. Authentication and access checks run on the hosted
service.

## What you can do

- Search apps, screens, UI elements, and user flows.
- Open screen details and ordered flow steps with images and source links.
- Read your favorite apps, screens, UI elements, flows, and collections.
- Create or rename a collection and add screens to it when requested.

Collection changes apply to the connected Nicelydone account. The tools do not
delete collections or favorites. Search requests are recorded in Nicelydone's
activity journal. The tools search Nicelydone's library and do not browse or
modify the source apps.

The requested permissions are `library:read`, `saved:read`, and
`collections:write`. Review these permissions before you connect.

## Example requests

- Find UI and UX references for a workspace app like Notion.
- Find examples of pricing pages with quarterly billing plans.
- Find best practices for two-factor authentication and write a specification
  with UI examples and source links.
- Find onboarding flows and explain the steps in a useful example.
- Show my saved screens and collections.

## Install in Claude Code

Run these commands in your terminal:

```sh
claude plugin marketplace add nicelydoneapp/mcp
claude plugin install nicelydone@nicelydone
```

Start a new Claude Code session. Open `/mcp`, select the Nicelydone connection,
and complete OAuth with your Nicelydone account. Ask Claude to check the
connection, then try an example request above.

The GitHub marketplace provides direct installation. It does not mean that
Anthropic has approved a directory listing.

For a local check before publishing an update, run:

```sh
claude plugin validate .claude-plugin/plugin.json --strict
claude plugin validate .claude-plugin/marketplace.json --strict
```

## Install in Cursor

For local testing in Cursor, copy this package to
`~/.cursor/plugins/local/nicelydone`, reload Cursor, and check the MCP connection
in Customize. Complete OAuth, call `test`, and run a read-only search.
Availability can depend on the account's plugin policy. Complete these checks
before relying on the connection.

## Package

- `.claude-plugin/plugin.json` declares the Claude plugin and its remote HTTP
  MCP connection.
- `.claude-plugin/marketplace.json` lists the plugin for direct installation
  from this repository.
- `.cursor-plugin/plugin.json` declares the Cursor plugin.
- `mcp.json` contains the Cursor remote MCP connection.

Both formats connect to the same hosted endpoint. The package contains no
local commands, hooks, agent definitions, or bundled skills.

## Support and policies

- [MCP overview](https://nicelydone.club/mcp)
- [Support](https://nicelydone.club/contact)
- [Privacy policy](https://nicelydone.club/legals#privacy)
- [Terms](https://nicelydone.club/legals#terms)

## License

The plugin configuration and documentation use the [MIT license](LICENSE).
The Nicelydone name and logo remain brand assets. Use of the hosted service and
its library content is covered by the linked Nicelydone terms.
