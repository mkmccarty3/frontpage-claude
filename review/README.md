# Reviewer workflow

Use an owner-provided sample account and eligible disposable site. Obtain account access through the provider's private review channel. This package contains no test login, customer data or shared access token. Never use a real customer's site as a substitute.

Record package version/hash, client version, server release, account coverage mode, scope, site plan/role, observed source revision, saved revision and matching preview result. Keep credentials, codes, source and callback URLs out of shared evidence.

1. Load the package and complete OAuth. Check account and permissions on Frontpage's consent page. Cancel once and verify no connection appears; retry normally.
2. Read-only: ask “List the sites this Frontpage connection covers, then show the pages on the site I choose.” Verify the intended site and real source revision.
3. Edit: connect with read/edit permission. Ask “On my selected test site, change one paragraph after reading the current source. Preserve unrelated content, check that saved revision's preview, and give me the review link.” Verify the exact text in the authenticated preview.
4. New page: ask “Create a temporary About page on my selected test site using its existing layout and style. Check the matching preview and do not publish.” Inspect the real page, then restore through Frontpage's existing file controls/API. The named delete tool needs expanded management consent and the inspected current revision; use it only on this disposable fixture.
5. Boundaries: try editing with read-only access, another unselected site, a protected secret/scaffold path, and a site on an ineligible plan. Each must deny without changing source. Try a stale observed revision and reuse an operation ID with different content; neither may force a new save.
6. Lifecycle: restart the client and verify its saved connection; verify normal refresh. Disconnect in Workspace → Developers, then verify requests and refresh fail. Remove local test configuration too.
7. Restore all fixture content and plan changes. Confirm published content and billing stayed unchanged. Record each actual pass/failure; never replace a client, persistence, preview or account test with a fabricated response.

A first-time user must finish Frontpage's normal signup/profile/site setup. MCP does not create that first site. Account-wide coverage can include future eligible sites without a new grant, but cannot bypass any site's current plan or membership.

Required before release: actual named-client edit/preview acceptance, clean install, failure matrix, working support/alerts, owner review and controlled beta approval. Provider submission and hosted-client certification remain separate steps.

## People and email acceptance

These five existing tools need their own current-release acceptance: `frontpage_get_crm_docs`, `frontpage_people_read`, `frontpage_people_write`, `frontpage_mail_read` and `frontpage_mail_write`. Source-only consent must deny CRM reads and writes. CRM read-only consent must deny writes. CRM write access still requires the site's eligible plan and editor role.

Use only owner-approved sample records. Page both public operation guides to completion; list sample People groups, create a clearly named temporary manual group with a stable request key, read it back, replay the identical request, then archive it. Read mail drafts; save a clearly named temporary draft with `save_mail_editor`, read it back, replay the same save key/payload and soft-delete only that draft. Neither flow may send, activate a rule or enroll anyone. Confirm no duplicate record exists.

A real send, scheduling or activation test needs a separately approved recipient and sample audience. Do not send to a customer's address or claim delivery from provider acceptance. Record untested operations explicitly. Fourteen successful tool calls do not prove every operation inside the People/email tools.

## Private reviewer login

Frontpage supplies the dedicated review account and password through the provider's private credential fields. Open `https://app.frontpage.host/auth/reviewer`, sign in, then start the normal OAuth connection. The review account has ordinary Editor access only to the prepared sample site. Normal plan, membership, consent, revision and send restrictions apply; the login grants no administrative bypass. Keep the password out of issues, recordings and this repository.

## Analytics read acceptance

With separate business-read consent, compare `frontpage_analytics_dashboard` and `frontpage_analytics_page_detail` against the existing UI services using the same fixed range, exact path and audience filters. Verify read continuations keep the returned version/readAt, missing consent and an unselected site deny, and revoked tokens stop working. These reports change no source or customer records. Raw SQL remains absent from discovery and execution. See https://frontpage.host/developers/analytics for metric definitions and known top-N limits.
