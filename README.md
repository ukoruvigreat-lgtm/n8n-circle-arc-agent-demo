# n8n-circle-arc-agent-demo
An n8n workflow that pays for data automatically using Circle's USDC on Arc
# n8n + Circle + Arc: AI Agent That Pays for Data Automatically

A working n8n workflow that demonstrates the "agentic economy" — an AI agent
that looks up data and pays for it automatically using USDC, powered by
Circle's Wallets and settled on Arc, Circle's own blockchain.

## What it does
1. Looks up a piece of data (a "lead")
2. Talks to a Circle developer-controlled wallet
3. Sends a small USDC payment automatically
4. Returns proof: payment status and transaction ID

## How to try it
1. Create a free Circle developer sandbox account at console.circle.com
2. Get testnet USDC from faucet.circle.com
3. Import `workflow.json` into your own n8n instance
4. Add your own Circle API key and entity secret as credentials
5. Run the workflow

## Why this matters
Circle has been building toward AI agents that can hold and move money
on their own. This shows that automation tools like n8n can already plug
into that system today.
