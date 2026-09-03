# YouTube Comments Downloader MCP

Use YouTube Comments Downloader from an MCP-compatible AI client. The server is a thin adapter over the existing YouTube Comments Downloader API: it does not create a second export system, export storage layer, queue, or file format.

## What it can do

- Create video, Short, live, playlist, channel, community, and bulk comment exports.
- Check and list existing exports.
- Return the existing public-by-ID export URL in JSON, CSV, HTML, XLSX, TXT, or ZIP format.
- Cancel or restart an existing export.
- Run the existing channel-details and community-images tools.

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

Open the [installation configurator](https://youtubecommentsdownloader.com/tools/mcp/install) for platform-specific steps.

## Authentication

OAuth 2.1 with PKCE S256 is the default for clients that support remote MCP authorization. The server also accepts an existing YCD API key in the `x-api-key` header. API keys are created in the [API keys dashboard](https://youtubecommentsdownloader.com/dashboard/api-keys).

Quota, plan, and billing checks remain in the existing API. A successful OAuth connection does not bypass product usage rules.

## Example prompts

- Export comments from this YouTube video and give me the JSON download URL.
- List my latest finished exports.
- Check this export and tell me whether it is ready.
- Get channel details for this YouTube channel.

## Development

The MCP endpoint is implemented in `api/src/routes/mcp`. Enable it in a deployment with `MCP_ENABLED=true`. Create the PocketBase collection before enabling the endpoint:

```bash
cd web
bun run migrate:mcp
```

The collection is server-only. OAuth codes and tokens are stored only as SHA-256 hashes in the single `mcp` collection. Public export URLs continue to use the existing API route and ID contract.

## Publishing checklist

1. Confirm the GitHub organization and create the public `youtube-comments-downloader-mcp` repository.
2. Copy this directory without the monorepo history.
3. Replace the xAI marketplace placeholder with the full lowercase commit SHA of the public repository.
4. Validate the Codex manifest and test the remote OAuth flow with a reviewer account.
5. Submit the package to each marketplace using the links in the documentation page.

## License

MIT. See [LICENSE](./LICENSE).
