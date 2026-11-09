---
name: nicelydone-mcp
description: Research real SaaS screens, UI components, and user flows with the Nicelydone MCP. Use it to find design references, compare captured interfaces, or work with the user's Nicelydone favorites and collections.
---

# Nicelydone MCP

## Connect

If the client already has a working Nicelydone connection, use it and skip setup.

Connect over Streamable HTTP at `https://mcp.nicelydone.club/mcp`. The user signs in through browser OAuth with an eligible paid Nicelydone account. The client gets its access token through OAuth.

### Claude Code

```bash
claude mcp add --transport http nicelydone https://mcp.nicelydone.club/mcp
```

Then run `/mcp` and finish the browser login.

### Codex

```bash
codex mcp add nicelydone --url https://mcp.nicelydone.club/mcp
codex mcp login nicelydone
```

For other clients, use the setup guide. [Nicelydone MCP setup](https://nicelydone.club/mcp)

Use the tools and input schemas your client exposes. If you are building an MCP client, connect to the same endpoint with an MCP SDK and discover operations with `tools/list`. [OAuth and API setup](https://nicelydone.club/help/integrations/mcp)

## Research workflow

1. Start with the user's design question. Note the criteria that must hold, such as a product type, pattern, or step.
2. Pick the right search tool.
   - `search-screens` finds full screens, such as dashboards or pricing pages.
   - `search-components` finds focused UI elements, such as tables or dialogs.
   - `search-flows` finds multi-step journeys, such as onboarding or cancellation.
   - `search-apps` finds products by name or category.
3. Search with `query` and optional `limit` and `offset`. Only `search-apps` accepts an empty query. Exact taxonomy filters work in `search-screens` only.
4. If results are sparse, try shorter queries for individual concepts. Check the shortlist against all the user's required criteria.
5. Use `get-screen-detail` with `screen_uuid` for detailed screen metadata and a screenshot. Use `get-flow-detail` with `flow_uuid` for ordered steps and their images. Pass the UUIDs from search results.

These tools need the `library:read` scope, which is the default.

## Evidence rules

- Give the app name and link to the exact reference `url` from each result.
- Open the returned images before describing visual details. If an image is unavailable, say which claims come from tool metadata.
- Separate observed steps from inferred behavior. Mark gaps in the capture, such as an unshown branch or an unknown skip option.

## Saved work

Use `list-collections` to find collections. Use `list-favorite-apps`, `list-favorite-screens`, `list-favorite-components`, or `list-favorite-flows` for the matching saved references. These tools require `saved:read`.

## Collection changes

Only change collections when the user explicitly asks. These tools need the `collections:write` scope.

- `create-collection` with `title`
- `update-collection` with `collection_uuid` and `title`
- `add-screens-to-collection` with `collection_uuid` and `screen_uuids`

Use collection and screen UUIDs from tool results. If a create response is lost, use `list-collections` to check for the collection before retrying. If you cannot verify whether the collection exists, report the uncertain result and stop the write.

## Connection errors

If authorization expires, ask the user to reconnect. If a scope is missing, ask them to approve the scope needed for the task. If the account lacks MCP access, explain that it requires an eligible paid plan. Check the tool result for `isError` even when the HTTP request succeeds.

## Example

The user asks how SaaS products handle onboarding with team invites and email verification.

Call `search-flows` with `{"query":"onboarding team invite email verification","limit":4}`. Open promising flows with `get-flow-detail` and inspect the step images. Compare when each step appears, which wording the screen uses, and whether the capture shows an option to skip it. Link to the source flows and flag any missing steps.
