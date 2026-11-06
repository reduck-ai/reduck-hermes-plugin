# Reduck for Hermes

[Reduck](https://reduck.ai) lets your agent use any website through tested browser scripts. The scripts run in your own Chrome, signed in as you, or on a browser that Reduck hosts. When no script does the task, the agent can make a new one.

This plugin adds the Reduck MCP server to Hermes.

## Install

1. Make a Reduck account at [reduck.ai](https://reduck.ai). To run scripts in your own Chrome, add the Reduck extension and pair it.
2. Create an API key at [reduck.ai/api-keys](https://reduck.ai/api-keys).
3. Install and enable the plugin:

   ```bash
   hermes plugins install reduck
   hermes plugins enable reduck
   ```

4. Give Hermes the key. In Hermes Desktop, enter it in the settings of the Reduck plugin. In the terminal, add this line to `~/.hermes/.env`:

   ```bash
   REDUCK_API_KEY=your-key
   ```

5. If the Hermes gateway is running, restart it so it connects to Reduck: `hermes gateway restart`.

## Try it

> Use Reduck to get me the weather in Paris for the next two weeks.

The agent finds a script for the site, runs it and gives you the result. The [script catalogue](https://reduck.ai/explore/scripts) shows the scripts that exist.

## Sign in with OAuth instead of a key

A Hermes plugin can send only a key to a remote server. To sign in with your browser, add the server yourself. A server in your `config.yaml` replaces the server of this plugin:

```bash
hermes mcp add reduck --url https://mcp.reduck.ai --auth oauth
hermes mcp login reduck
```

## What this plugin does

- Each tool call goes to `https://mcp.reduck.ai` with your `REDUCK_API_KEY`.
- A run acts on websites as you, in your paired Chrome. It can send forms, post or buy if the script does that. Each script states its side effects.
- Your runs, their traces and your scripts are kept on your Reduck account.
- Runs on a Reduck-hosted browser use the credits of your plan.
- The Reduck server gives the list of tools when Hermes connects. The commit that the catalog pins does not contain that list.
- The plugin has no local code. It does not read files and does not run commands on your computer.

## Known issue

On Hermes 0.22.7 and older, the Reduck tools can stop after a reconnect, with the message `MCP server 'reduck' transport is down`. Hermes then sends `${REDUCK_API_KEY}` as text instead of your key. Restart Hermes to connect again. Hermes has fixed this for its next release.
