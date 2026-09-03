---
name: youtube-audience-research
description: Turn YouTube comment exports into structured audience research questions, summaries, and follow-up analyses.
---

# YouTube audience research

Use the YouTube Comments Downloader MCP tools as the data collection step for audience research.

## Workflow

1. Ask for a YouTube URL and the intended research question.
2. Use `create_youtube_comments_export` with the narrowest matching `contentType`.
3. Use `get_youtube_export_status` until the export is finished or has an error.
4. Use `get_youtube_export_file` to return the existing public file URL in the format the user requested.
5. Keep collection facts separate from interpretation. State when a conclusion is based on a sample or an export limit.

## Useful research prompts

- What recurring needs, objections, and questions appear in the comments?
- Which themes are positive, negative, or unresolved?
- What audience segments are implied by the language and use cases?
- Which comments should inform the next video, product, or support article?

Do not claim that the MCP server searches comments or bypasses YCD quota. Search is not a v1 tool, and quota and billing remain enforced by the existing API.
