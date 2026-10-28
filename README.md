# Frontpage for Claude Code

Read and edit existing Frontpage websites through the hosted Frontpage MCP service, then check the preview for the saved revision.

This public beta is available to Frontpage accounts with an existing Scale or eligible Internal site. Each site's plan and your current role apply to every operation. Installing this package grants no site access by itself. Claude directory submission is separate; no directory listing is claimed.

Read the [Frontpage setup guide](https://app.frontpage.host/connections/claude-code) for login, permissions, examples, troubleshooting and disconnect. See the [MCP developer guide](https://frontpage.host/developers/mcp), [MCP Server feature page](https://frontpage.host/mcp-server) and [release notes](CHANGELOG.md).

## Load the package

Download the ZIP from the [0.5.1 release](https://github.com/mkmccarty3/frontpage-claude/releases/tag/v0.5.1), verify it against SHA256SUMS, and extract it into a folder named `frontpage`, then run:

```sh
claude plugin validate --strict ./frontpage
claude --plugin-dir ./frontpage
```

In Claude Code, run `/mcp`, choose the Frontpage server, and authenticate. Sign in on `https://app.frontpage.host` with your existing Frontpage login. Choose all current and future eligible sites or selected sites, then read-only or read/edit access. Review the actual account, sites and permissions before allowing access.

Use `/frontpage:site-edit` for the guided site workflow. The plugin contains one skill and a remote HTTP configuration; it runs no local server, shell hook or background process.

For a direct connection without the plugin:

```sh
claude mcp add --transport http --scope user frontpage https://app.frontpage.host/api/mcp
claude mcp login frontpage
```

Use either setup path to avoid duplicate server entries. A browser callback returns to the local client that started the login. Keep codes, tokens and callback URLs private.

## Available tools

| Tool | Purpose |
|---|---|
| `frontpage_list_sites` | Discover covered sites and current availability |
| `frontpage_get_site_context` | Check current permissions and authoring rules |
| `frontpage_list_pages` | Find pages at a source revision |
| `frontpage_list_files` | List allowed source paths |
| `frontpage_read_file` | Read UTF-8 source with bounded continuation |
| `frontpage_search_files` | Search literal text in allowed source |
| `frontpage_list_history` | Inspect bounded revision history |
| `frontpage_get_deploy_status` | Check the exact revision's preview |
| `frontpage_apply_file_changes` | Save bounded text changes and request a preview |
| `frontpage_get_crm_docs` | Read current People or Mail operations without customer data |
| `frontpage_people_read` | Read contacts, groups, stages, rules and activity with CRM read consent |
| `frontpage_people_write` | Manage People through the shared service with CRM write consent |
| `frontpage_mail_read` | Read email content, series and delivery history with CRM read consent |
| `frontpage_mail_write` | Manage email drafts, campaigns and series with CRM write consent |

Read access needs viewer membership. Edits need editor/admin membership and a read/edit grant. Selected-site access does not include future sites; account coverage does. All modes retain current site permissions and plans.

People and email require separate `crm:read` / `crm:write` consent. Source-only grants do not share contacts. CRM access defaults to none; existing grants gain nothing. Request the required scopes from the client and approve the matching People/email access explicitly. Management requires an editor role and current plan, permission, version and receipt checks. Never send, enroll or activate without the user's instruction. Read `frontpage_get_crm_docs` first and follow its paging and uncertain-write guidance.

MCP does not publish, delete files, create the first site, or access billing, team administration or vendor credentials. Private inbox/order reads require separate business consent. The existing Frontpage CLI has a separate API-key connection and a broader command set.

## Review and disconnect

A saved revision may still be building. Wait for that exact revision to report ready, then open its preview link. Browser sign-in may be required. Review and publish in Frontpage.

Manage grants at [Workspace → Developers → Connected Apps](https://app.frontpage.host/workspace/account/developers#connected-apps). Expand Connection details to remove one connection, or disconnect the app to stop all its active connections. Signing out, uninstalling the plugin or removing a local server entry does not revoke a grant.

## Errors and limits

- `SITE_PLAN_REQUIRED`: the site needs Scale. Upgrade in Frontpage, then retry; account coverage needs no new connection.
- Permission/scope denial: request only approved operations; reconnect only if you choose to grant more access.
- Conflict: wait for an active Frontpage task or read the newer source before preparing another edit.
- Pending or uncertain write: keep the same operation ID/payload. Never blindly repeat an uncertain edit under a new ID.
- Failed/superseded preview: inspect the reported revision; do not call another build ready.
- Rate limit: wait for the supplied retry guidance.
- Temporarily unavailable: retry later or contact support. Do not send credentials to support.

Text edits allow 20 files, 256 KiB per file and 1 MiB total. Binary writes and deletes are outside this beta. Results use bounded pages and UTF-16 continuation offsets; follow the returned cursor/offset and revision.

## Compatibility and support

The service uses MCP SDK 2.3.1 and stateless Streamable HTTP. Claude Code 2.1.218 passed real OAuth and transport checks, a source edit with its exact ready preview, and sample People/email draft work. On October 27, hosted Claude and official MCP Inspector 2.12.0 each passed all 14 tools: source reads, create/update, exact ready preview, guides, an empty group and an email draft. Temporary pages and sample records were cleaned up without publishing. A separately approved MCP test email reached delivered; that was not part of hosted Claude's test. These samples do not certify every nested People/Mail operation. Current public-install checks belong in the release record. Codex, ChatGPT, Cursor and Grok need separate OAuth and client tests. No public directory listing exists yet.

See [review cases](review/README.md). [Privacy](https://app.frontpage.host/connections/privacy). Support: [support@frontpage.host](mailto:support@frontpage.host).

The MIT license covers only this integration package. The hosted service and Frontpage application remain separate. The icon identifies Frontpage; the license grants no endorsement or trademark rights.

Build sources follow [Anthropic's plugin manifest reference](https://code.claude.com/docs/en/plugins-reference) and [remote MCP setup](https://code.claude.com/docs/en/mcp). Validate against the client version you will ship.


## Business permissions

This release adds separate optional business read/manage permissions for
analytics, usage, forms/inbox, Store, Support and task/routine records. Source
and People/email permissions stay separate. Existing grants gain nothing;
reconnect and explicitly select the business access you want. Both choices
start off. Your current role and each site's eligible plan still apply.

Management can change the running catalog/form settings and send Support
replies, guidance or retries on your instruction. Payments stays read-only.
Website task start/retry, routine create/edit/run/resume, financial/account/
credential changes and unfinished Booking are excluded. Cancel and pause do
not start work. Public setup and limits: https://frontpage.host/developers/mcp.

Client packages contain only settings and guidance. They use the same hosted
MCP/OAuth services; no CLI, customer editor or internal agent changes are needed.

## Analytics reports

With business:read consent, use `frontpage_analytics_dashboard` for the existing
site-wide UI report and `frontpage_analytics_page_detail` with an exact `path`
for one page. The page report includes views, visitors, sessions, time/scroll,
trends, sources, next pages, audience, frustration, errors and performance.
Use days 1/7/30/90 (default 30), or both from and to. Page filters are device,
country, source, referrer, os and browser; path is a separate field. Retain
readAt, range, filters and version on continuations. Sparse samples remain null.

The existing query, summary, timeseries, funnel and compare tools remain. Filter
type=pageview for view counts. A funnel measures session overlap, not event
order. Raw SQL is unavailable through MCP. UI View all pagination and complete
labeled-click reporting remain separate coverage limits. Shared definitions:
https://frontpage.host/developers/analytics. MCP setup/tool limits:
https://frontpage.host/developers/mcp.
