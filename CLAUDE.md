# Daily Planner - Claude Code Integration

## "Refresh my planner" workflow

When the user says "refresh my planner" or "plan my day", do this:

1. Search Slack for recent DMs and group messages sent TO the current user (last 3 working days) where someone else sent the last message — these likely need a reply
2. Filter out bot messages (Jira, etc.) and conversations the user already replied to
3. Build a JSON payload:
```json
{
  "replies": [
    {
      "id": "unique-id",
      "sender": "Person Name",
      "preview": "First 100 chars of their message",
      "time": "Day time (e.g. Fri 4:03p)",
      "url": "Slack permalink if available",
      "source": "slack"
    }
  ]
}
```
4. Base64 encode the JSON and generate this URL:
```
https://abhinavrajendrakumarbhatt-lang.github.io/daily-planner/#data=<base64-encoded-json>
```
5. Give the user the link. When they click it, the planner loads their pending replies into the sidebar.

## How to search Slack for pending replies

Use the Fabric MCP Slack tools:
- `slack_search_public_and_private` with `filters: "to:<@USER_ID> after:YYYY-MM-DD"` to find messages sent to the user
- Cross-reference with messages FROM the user to see which conversations are already replied to
- The Slack tool auto-resolves the current user's ID

## Planner URL
- Planner: https://abhinavrajendrakumarbhatt-lang.github.io/daily-planner/
- Guide: https://abhinavrajendrakumarbhatt-lang.github.io/daily-planner/guide.html
