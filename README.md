<img width="1917" height="960" alt="image" src="https://github.com/user-attachments/assets/39b7e242-f685-4530-81a1-89b86b11d351" /># n8n-circle-arc-agent-demo
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
3. Import `CIRCLE USDC AGENT DEMO.json` into your own n8n instance
4. Add your own Circle API key and entity secret as credentials
6. Run the workflow
7. 
## ⚠️ Important: Fix the "crypto module is disallowed" error
By default, n8n blocks Code nodes from using certain built-in tools for security reasons — including crypto, which this workflow needs to securely seal your Circle entity secret before every payment. If you import this workflow and see an error like Module 'crypto' is disallowed, follow the fix below based on how you're running n8n.
**If you're running n8n with Docker**
1. Stop your current n8n container
2. Start it again with this extra setting added: docker run -it --rm --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n -e NODE_FUNCTION_ALLOW_BUILTIN=crypto docker.n8n.io/n8nio/n8n. The important part is `-e NODE_FUNCTION_ALLOW_BUILTIN=crypto` — this tells n8n it's allowed to use the crypto tool.
### If you're running n8n with npx (no Docker)

1. Stop n8n if it's running (press Ctrl+C in your terminal)
2. Set the environment variable, then start n8n:
**On Windows (Command Prompt):** set NODE_FUNCTION_ALLOW_BUILTIN=crypto npx n8n
**On Mac/Linux:** export NODE_FUNCTION_ALLOW_BUILTIN=crypto npx n8n
3. Open `http://localhost:5678` again and re-test the Code node — the
error should be gone.

### If you're using n8n Cloud
You'll need to contact n8n support or check their docs, since Cloud
environments handle this setting differently and it can't be changed
from your own terminal.

## Common errors and fixes
**"Malformed API key"**
Make sure you copy your ENTIRE API key, including the `TEST_API_KEY:`
prefix at the start — it's part of the key, not just a label.

**"Fail to parse ID as UUID"**
Double check you're using the correct ID in the right place:
- Wallet **address** looks like `0xAbC123...` — used for sending/receiving
- Wallet **ID** looks like `c4d1da72-111e-4d52-bdbf-2e74a2d803d5` — used
when calling most Circle API endpoints
Run `list-wallets.js` (or call the List Wallets endpoint) to see both
side by side.

**"Cannot find target wallet in the system"**
You may have copied the `walletSetId` instead of the wallet's own `id`.
They look similar — double check which field you copied.

**Payment fails with an idempotency key error**
The `idempotencyKey` field must be a valid UUID (e.g.
`a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11`), not a timestamp. This workflow
generates one automatically in the Code node using `crypto.randomUUID()`.

## Why this matters

Circle has been building the infrastructure for AI agents to hold and
move money on their own. This project shows that automation builders —
not just professional crypto developers — can already build on top of
that infrastructure today, using accessible tools like n8n.

Built by [UKORUVI GREAT MARHO]. Feedback welcome — especially from anyone building
on Circle or Arc. 





