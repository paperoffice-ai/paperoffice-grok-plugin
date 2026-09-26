<div align="center">

<img src="assets/logo.png" alt="PaperOffice" width="120" />

# PaperOffice for Grok Build

Search, read and create documents in your PaperOffice account from Grok.

[Documentation](https://paperoffice.ai/en/developer/mcp/) · [PaperOffice](https://paperoffice.ai) · [API reference](https://api.paperoffice.ai/latest/docs/llms.txt)

</div>

## What this plugin does

This plugin connects Grok Build to the hosted PaperOffice MCP server at
`https://mcp.paperoffice.ai/grok`. Nothing runs on your machine. The server
lives in the PaperOffice data center in the EU and works on the documents in
your own PaperOffice account.

The tool list is small on purpose. A few core tools are listed directly:

| Tool | Effect |
|------|--------|
| `po_workspaces_list` | Read-only. Lists the workspaces the token can see. |
| `po_documents_search` | Read-only. Searches documents by keyword, file name and extracted fields. |
| `po_documents_get` | Read-only. Document identity, processing state and extracted data. |
| `po_documents_text_get` | Read-only. OCR text of a document. |
| `po_documents_folders_list`, `po_documents_tags_list` | Read-only. Folders and tags of a workspace. |
| `po_documents_create_from_content` | Writes data. Creates a PDF from Markdown or HTML in a workspace. |
| `po_documents_upload_url_get` | Writes data. Upload slot for a file. |
| `po_extraction_invoice` | Read-only. Invoice field extraction. |
| `po_job_get` | Read-only. Status of a background job. |

Everything else in the Documents Operations catalog (import, classification,
signatures, storage, webhooks, audit) is reached through four discovery tools:
`po_mcp_tools_search` finds a tool, `po_mcp_tools_schema` shows its contract,
`po_mcp_tools_call_read` runs read-only tools and `po_mcp_tools_call_write`
runs tools that create, change, delete or send. Every tool description starts
with `READ-ONLY.`, `WRITES DATA.` or `DESTRUCTIVE.` so the agent knows the
effect before it calls.

## Setup

1. Install the plugin from the xAI plugin marketplace.
2. On the first request Grok opens the PaperOffice sign-in page (OAuth 2.1).
   Sign in with your PaperOffice account, or paste a **user token**
   (`po_ut_…`) or **group token** (`po_gt_…`) created at
   [app.paperoffice.ai](https://app.paperoffice.ai) under *Account → API*.
   A group token limits the plugin to the workspaces of that group.
3. Ask, for example:

```text
List my PaperOffice workspaces and the number of documents in each one.
Find the latest invoice in workspace 1408 and tell me the total amount.
Create a PDF in workspace 1408 from these meeting notes.
```

System keys (`po_sk_`) and publishable keys (`po_pk_`) are rejected by the
server.

## Network and credentials

- Endpoint called: `https://mcp.paperoffice.ai/grok` (Streamable HTTP).
- Credential: the OAuth access token issued by `https://mcp.paperoffice.ai`
  after sign-in, or the PaperOffice token you provide. It is sent as a bearer
  header to that endpoint only.
- No scripts, hooks, skills or local processes are part of this plugin.
- Documents stay in your PaperOffice account. Requests are billed to that
  account according to your plan; rejected requests cost nothing.

## License

MIT for the files in this repository. The PaperOffice service is governed by
the [PaperOffice terms](https://paperoffice.ai/en/terms/).
