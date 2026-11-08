# Typeform MCP server

List forms and explicitly create a new empty form for later review.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `TYPEFORM_ACCESS_TOKEN`



Credential help: https://www.typeform.com/developers/create/reference/retrieve-forms/

## Provider setup

Use your own Typeform personal access token with forms:read and forms:write permissions. Creating a form is a real workspace change; this tool does not publish, distribute or collect responses by itself.

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call typeform_list_forms '{"page":1,"page_size":10}'
```

## Use with an MCP client

Launch `node /absolute/path/typeform-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| typeform_list_forms | Read | List a bounded page of accessible forms. |
| typeform_create_form | Explicit approval required | Create an empty form with a title; review sharing and visibility in Typeform before use. |

## Concrete workflow

List forms and explicitly create a new empty form for later review.

1. typeform_list_forms
2. typeform_create_form

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Import with PipMCP](https://pipmcp.com/github/start?integration=openapi-to-mcp&utm_source=github&utm_campaign=github-typeform-mcp&utm_content=readme) when you want the hosted service. This provider is not currently listed as a managed template. Import selected-openapi.json (REST) or the official GraphQL schema linked in provenance, configure authentication, and review the tools before execution. Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/typeform/).

## Provenance and maintenance

- https://www.typeform.com/developers/create/reference/retrieve-forms/
- https://www.typeform.com/developers/create/reference/create-form/

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
