<div align="center">

<img src="assets/logo.png" alt="PaperOffice" width="120" />

# PaperOffice for Grok Build

Search, read, extract and organize the business documents in your PaperOffice account from Grok.

[Documentation](https://paperoffice.ai/en/developer/mcp/) · [PaperOffice](https://paperoffice.ai) · [API reference](https://api.paperoffice.ai/latest/docs/llms.txt)

</div>

## What this plugin does

This plugin connects Grok Build to the hosted PaperOffice MCP server at
`https://mcp.paperoffice.ai/grok`. Nothing runs on your machine. The server
lives in the PaperOffice data center in the EU and works on the documents in
your own PaperOffice account.

Every operation is listed as its own tool (52 tools), each with a
description, an input schema and annotations. Each tool is marked as
read-only, writes data or destructive, so Grok can ask you to confirm changes.
There is no generic tool that runs other, unlisted operations.

| Tool | Effect | What it does |
|------|--------|--------------|
| `po_workspaces_list` | Read-only | List workspaces |
| `po_documents_search` | Read-only | Search documents |
| `po_documents_get` | Read-only | Get document details |
| `po_extraction_invoice` | Writes data | Extract invoice data |
| `po_job_get` | Read-only | Get job status |
| `po_analytics_financial_summary_get` | Read-only | Summarize document amounts |
| `po_knowledge_search` | Read-only | Search knowledge base |
| `po_documents_create_from_content` | Writes data | Create PDF from text |
| `po_documents_rename` | Destructive | Rename document |
| `po_documents_text_get` | Read-only | Read document text |
| `po_knowledge_graph_ask` | Read-only | Ask across documents |
| `po_knowledge_get_article` | Read-only | Read knowledge article |
| `po_analytics_financial_overdue_get` | Read-only | List overdue invoices |
| `po_documents_process` | Destructive | Start AI processing |
| `po_documents_download` | Read-only | Get download link |
| `po_documents_update_index` | Destructive | Update index fields |
| `po_documents_upload` | Writes data | Upload document from URL |
| `po_extraction_receipt` | Writes data | Extract receipt data |
| `po_extraction_delivery_note` | Writes data | Extract delivery note data |
| `po_extraction_purchase_order` | Writes data | Extract purchase order data |
| `po_tasks_list_my_tasks` | Read-only | List my tasks |
| `po_tasks_get_task_details` | Read-only | Get task details |
| `po_tasks_claim_task` | Writes data | Claim task |
| `po_tasks_complete_task` | Destructive | Complete task |
| `po_tasks_reject_task` | Destructive | Reject task |
| `po_documents_move` | Writes data | Move document |
| `po_documents_copy` | Writes data | Copy document |
| `po_documents_tags_list` | Read-only | List document tags |
| `po_documents_tags_create` | Writes data | Add document tag |
| `po_documents_folders_list` | Read-only | List document folders |
| `po_documents_folders_create` | Writes data | Create document folder |
| `po_vat_validate` | Read-only | Validate EU VAT ID |
| `po_currency_convert` | Read-only | Convert currency |
| `po_pdfstudio_merge` | Writes data | Merge PDFs |
| `po_pdfstudio_split` | Writes data | Split PDF |
| `po_pdfstudio_compress` | Writes data | Compress PDF |
| `po_dataripper_office2pdf` | Writes data | Convert Office to PDF |
| `po_documents_versions_list` | Read-only | List document versions |
| `po_documents_audit_trail_get` | Read-only | Get change history |
| `po_documents_trash_list` | Read-only | List recycle bin |
| `po_documents_restore` | Writes data | Restore document |
| `po_documents_delete` | Destructive | Delete document |
| `po_knowledge_list_bases` | Read-only | List knowledge bases |
| `po_knowledge_list_articles` | Read-only | List knowledge articles |
| `po_knowledge_categories` | Read-only | List knowledge categories |
| `po_knowledge_get_base` | Read-only | Get knowledge base |
| `po_knowledge_add_article` | Writes data | Create knowledge article |
| `po_knowledge_update_article` | Destructive | Update knowledge article |
| `po_knowledge_translate` | Destructive | Translate knowledge article |
| `po_knowledge_create_base` | Writes data | Create knowledge base |
| `po_knowledge_update_base` | Destructive | Update knowledge base |
| `po_knowledge_delete_article` | Destructive | Delete knowledge article |

The tools have no password or credential fields. Protected workspaces are
unlocked in the PaperOffice app.

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
Find the latest invoice in my PaperOffice workspace and tell me the supplier and the total amount.
Create a PDF in my PaperOffice workspace from these meeting notes.
```

System keys (`po_sk_`) and publishable keys (`po_pk_`) are rejected by the
server.

## Network and credentials

- Endpoint called: `https://mcp.paperoffice.ai/grok` (Streamable HTTP).
- Credential: the OAuth access token issued by `https://mcp.paperoffice.ai`
  after sign-in, or the PaperOffice token you provide. It is sent as a bearer
  header to that endpoint only.
- No scripts, hooks, skills or local processes are part of this plugin.
- Your documents remain stored in your PaperOffice account; Grok receives only
  what a tool returns. Tool calls are billed in credits to that account
  according to your plan.

## License

MIT for the files in this repository. The PaperOffice service is governed by
the [PaperOffice terms](https://paperoffice.ai/en/terms/).
