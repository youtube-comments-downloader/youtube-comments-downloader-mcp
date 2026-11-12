[![YouTube Comments Downloader MCP on AI Agents Listing](https://aiagentslisting.com/youtube-comments-downloader-mcp/badge.svg?claim=6f0707344e287de53622e17444b02a94)](https://aiagentslisting.com/mcp/youtube-comments-downloader-mcp)

# YouTube Comments Downloader MCP

Use YouTube Comments Downloader from an MCP-compatible AI client. The server is a thin adapter over the existing YouTube Comments Downloader API: it does not create a second export system, export storage layer, queue, or file format.

## What it can do

- Download comments from videos, Shorts, live streams, playlists, channels, and community posts.
- Check and list your downloads.
- Get the download file in JSON, CSV, HTML, XLSX, TXT, or ZIP format.
- Get video transcripts.
- Get channel details.

There is intentionally no `search_youtube_comments` tool in v1 because the main API does not yet expose a matching endpoint.

## Install

Use the public MCP URL:

```text
https://api.youtubecommentsdownloader.com/mcp
```

For Cursor and compatible JSON clients, add:

```json
{
  "mcpServers": {
    "youtube-comments-downloader": {
      "type": "http",
      "url": "https://api.youtubecommentsdownloader.com/mcp"
    }
  }
}
```

For Claude Code, add the marketplace and install the plugin:

```text
/plugin marketplace add youtube-comments-downloader/youtube-comments-downloader-mcp
/plugin install youtube-comments-downloader-mcp@youtube-comments-downloader
```

For Gemini CLI:

```bash
gemini extensions install https://github.com/youtube-comments-downloader/youtube-comments-downloader-mcp
```

Open the [installation configurator](https://youtubecommentsdownloader.com/tools/mcp/install) for platform-specific steps.

## Authentication

OAuth 2.1 with PKCE S256 is the default for clients that support remote MCP authorization. The server also accepts an existing YCD API key in the `x-api-key` header. API keys are created in the [API keys dashboard](https://youtubecommentsdownloader.com/dashboard/api-keys).

Credits are charged by the existing API, the same as in the app.

## Example prompts

- Download the comments from this YouTube video and give me the JSON file URL.
- List my latest finished downloads.
- Check this download and tell me whether it is ready.
- Get the transcript of this video and summarize it.
- Get channel details for this YouTube channel.

## Maintenance

This repository contains only the installable plugin package. The hosted MCP adapter remains in the main YouTube Comments Downloader application and consumes its existing API, exports, queues, PocketBase, and Redis services. The deployment that serves the endpoint must run the YCD API and have the PocketBase collection created:

```bash
cd web
bun run migrate:mcp
```

The collection is server-only. OAuth codes and tokens are stored only as SHA-256 hashes in the single `mcp` collection. Public export URLs continue to use the existing API route and ID contract.

## Publishing checklist

1. Pin the public repository commit in the xAI marketplace catalog.
2. Validate the Codex manifest and test the remote OAuth flow with a reviewer account.
3. Submit the package to each marketplace using the links in the documentation page.

## License

MIT. See [LICENSE](./LICENSE).
