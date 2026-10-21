# Reviewer workflow

Use an owner-provided sample account and eligible disposable site. Obtain account access through the provider's private review channel. This package contains no test login, customer data or shared access token. Never use a real customer's site as a substitute.

Record package version/hash, client version, server release, account coverage mode, scope, site plan/role, observed source revision, saved revision and matching preview result. Keep credentials, codes, source and callback URLs out of shared evidence.

1. Load the package and complete OAuth. Check account and permissions on Frontpage's consent page. Cancel once and verify no connection appears; retry normally.
2. Read-only: ask “List the sites this Frontpage connection covers, then show the pages on the site I choose.” Verify the intended site and real source revision.
3. Edit: connect with read/edit permission. Ask “On my selected test site, change one paragraph after reading the current source. Preserve unrelated content, check that saved revision's preview, and give me the review link.” Verify the exact text in the authenticated preview.
4. New page: ask “Create a temporary About page on my selected test site using its existing layout and style. Check the matching preview and do not publish.” Inspect the real page, then restore through Frontpage's existing file controls/API. MCP beta has no delete tool.
5. Boundaries: try editing with read-only access, another unselected site, a protected secret/scaffold path, and a site on an ineligible plan. Each must deny without changing source. Try a stale observed revision and reuse an operation ID with different content; neither may force a new save.
6. Lifecycle: restart the client and verify its saved connection; verify normal refresh. Disconnect in Workspace → Developers, then verify requests and refresh fail. Remove local test configuration too.
7. Restore all fixture content and plan changes. Confirm published content and billing stayed unchanged. Record each actual pass/failure; never replace a client, persistence, preview or account test with a fabricated response.

A first-time user must finish Frontpage's normal signup/profile/site setup. MCP does not create that first site. Account-wide coverage can include future eligible sites without a new grant, but cannot bypass any site's current plan or membership.

Required before release: actual named-client edit/preview acceptance, clean install, failure matrix, working support/alerts, owner review and controlled beta approval. Provider submission and hosted-client certification remain separate steps.
