# Sponsor technology research: Visa, Metal, Coinbase

Researched 24 October 2026. This is technical due diligence, not a claim that every API is enabled for every hackathon account. Root's brief audit establishes prize eligibility separately. Primary documentation was preferred. Metal's docs failed in the web reader but were fetched successfully as public Markdown with curl; URLs below are the original primary sources.

## Most useful conclusions

- Visa TAP, Visa Intelligent Commerce (VIC), Airwallex issuing, and Airi are distinct integration surfaces. A Visa-branded card or a TAP-looking signature is not evidence of VIC access or prize eligibility by itself.
- Metal is **metalntwx.com**, operated by Nexus Networks, Inc., with Loong Wang and Catherine Porter. It is not metal.build, Metallicus, or Metal Blockchain. Its testnet has unusually useful programmable mandates and signed-order verification, not merely cryptocurrency transfers.
- Coinbase x402 can implement the economic decision to buy evidence, skills, or verification. Paying for an endpoint alone is already commodity functionality; originality must come from which evidence gets bought, why, and how it changes an Airwallex financial decision.
- Treat the bank ledger and each chain ledger as separate systems. A testnet faucet does not fund an Airwallex account. No verified atomic or self-serve production bridge between these environments was established.
- The strongest sponsor integrations enforce something the app otherwise cannot prove: payment authority, limited delegation, provenance of a purchase, transaction finality, or a bounded paid-information budget.

## Visa: trust, authorization, credentials, and payments

### Trusted Agent Protocol (TAP)

TAP authenticates agent requests to merchant infrastructure using HTTP message signatures based on RFC 9421. The merchant reconstructs the signature base, obtains the agent public key, checks the signature, and validates request context. This is useful for distinguishing verified agent traffic and binding browsing/payment intent to the merchant interaction. The protocol includes consumer-recognition and payment-related objects. A local proof of concept can implement the public protocol; it should identify its registry as a demo registry, not claim Visa has approved its agent. [Visa developer introduction](https://developer.visa.com/docs/trusted-agent-protocol)

Visa's official sample has an agent registry, merchant backend, CDN proxy, merchant frontend and TAP agent. This makes a working merchant-side demonstration accessible without obtaining tokenization credentials. It is a sample, not a complete production authorization service. Add application-level replay storage, policy checks and receipts; do not assume signature verification proves the goods were delivered, the model chose correctly, or the user authorized every future action. [Official TAP repository](https://github.com/visa/trusted-agent-protocol)

The proxy sample supports Ed25519/RSA-PSS-SHA256 signatures and key lookup. The TAP agent sample distinguishes browser and payer tags, and can use Playwright. **Quality caveat:** one sample README incorrectly labels Ed25519 post-quantum resistant; do not repeat that assertion. A public repository is still code to review. [Proxy sample](https://github.com/visa/trusted-agent-protocol/blob/main/cdn-proxy/README.md), [Agent sample](https://github.com/visa/trusted-agent-protocol/blob/main/tap-agent/README.md)

### Visa Intelligent Commerce (VIC)

VIC supplies tokenized credentials and an authorization workflow. The cardholder is verified, an instruction is authenticated with a passkey, and credential retrieval is checked against that instruction. Network controls can bind intended merchant and amount; transaction outcomes feed post-purchase handling. This is stronger than an LLM prompt saying “stay within budget.” It is still necessary to implement our product's evidence semantics, such as whether a replacement part matches the approved equipment. [Visa VIC technical overview](https://github.com/visa/ai/wiki/Visa-Intelligent-Commerce)

The official `visa/ai` repository contains TypeScript packages for token management, MCP and direct REST APIs; a LangGraph/Next.js demo covers tokenization and passkeys. Its documentation MCP endpoint is `https://sandbox.mcp.visa.com/mcp/doc`. A documentation MCP server does not execute payments. [Visa AI toolkit](https://github.com/visa/ai)

Execution examples require VIC and VTS credentials, MLE certificates/private key and signing keys. Tools include card enrollment, purchase instruction creation/update/cancel, payment credential retrieval and transaction-event confirmation. Public sample code therefore does **not** imply self-serve credentials. Confirm hackathon enablement before selecting a concept dependent on live VIC. A historical Visa announcement describes execution MCP and Acceptance Toolkit as pilots; current account eligibility should be confirmed rather than inferred from that old announcement. [MCP execution prerequisites](https://github.com/visa/ai/blob/main/apps/vic-mcp-examples/README.md), [Visa announcement](https://corporate.visa.com/en/sites/visa-perspectives/innovation/visa-mcp-server-agent-acceptance-toolkit.html)

### Airwallex Airi

The official Airi CLI authenticates by OAuth, lists payment methods, creates an order-specific mandate, obtains user approval through a passkey URL, retrieves a single-use tokenized credential, and reports the checkout result. It provides macOS/Linux binaries, so this Windows workspace would need WSL/Linux or a remote runtime. `--file` keeps credential contents out of stdout. Do not quote older command syntax if current CLI differs. [Official Airi CLI](https://github.com/airwallex/airi-cli)

The hackathon builder guide distinguishes Airi's allowlisted real-merchant shopper flow from separately enabled merchant-side sandbox commerce. Use that distinction in project feasibility. Access is a dependency, not a reason to pretend a sandbox card can buy arbitrary real goods. [Builder guide](https://airwallexdev.com/guide)

### Creative Visa compositions

1. **Authorization survives change only when semantics survive:** an agent replans a procurement mission after a backorder, then proves which material changes need a new instruction.
2. **Grant or incident budget enforcement:** parse funding restrictions, compile enforceable card controls, and record application checks for restrictions card networks cannot see.
3. **Post-purchase evidence continuity:** retain authorization, merchant acknowledgment and delivery evidence as distinct artifacts; select a refund, replacement or dispute based on their contradictions.

## Metal: programmable settlement authority

### Identity and access

Metal describes infrastructure for tokenized finance, institutional settlement, programmable policy and agent payment protocols, with Airwallex as a payment-rail partner. This does not establish immediate production availability of each marketed asset type or corridor. The docs and testnet provide a more concrete scope. [Metal company site](https://metalntwx.com)

Its agent quickstart supports a CLI/MCP setup, a funded testnet key and a demo x402 payment. Console registration supplies a personal RPC endpoint. The CLI MCP has payment/funding/status tools. `*USDZ` is a testnet token, not USDC or redeemable dollars. [Agent quickstart](https://docs.metalntwx.com/agents/quickstart), [RPC endpoints](https://docs.metalntwx.com/network/endpoints)

The public npm registry exposes `@metalntwx/metal-pay` version 0.3.3 at research time. It supports official x402 packages, Metal devnet/testnet, the `exact` scheme and native clearing. Testnet identifier is `eip155:63825`; the hosted facilitator is `https://x402-testnet.metalntwx.com/x402/facilitator`. The package checks asset/domain and payment caps before signing. Use its adapters rather than assuming an ordinary EVM integration covers Metal's gas-token differences. [Published package metadata and README](https://registry.npmjs.org/@metalntwx%2fmetal-pay)

### Mandates are the most differentiated primitive

An owner binds a credential to its Metal account. The agent receives its own P-256 key, while the owner's key stays separate. The account checks permitted payees, per-payment cap, lifetime budget, allowed payment count and expiry on settlement. Replacing a mandate carries previous spend into the new budget; renewing explicitly resets it; revocation prevents subsequent settlement under that mandate. A payment consumes authority atomically with the transfer. An auditor can verify the allowed payment from chain data and the credential, but that alone does not prove what was bought. [Mandates](https://docs.metalntwx.com/agents/mandates)

The practical workflow creates an account, funds it, issues/binds limits, pays and verifies. Limits are inclusive. The budget is lifetime, not an automatic daily reset. Testnet faucet grants are limited per client/IP/day; do not plan a many-wallet demo that assumes unlimited funding. Owner keys and agent keys must remain distinct even in the demo. [Spending-limits walkthrough](https://docs.metalntwx.com/agents/spending-limits)

### Signed orders and direct payouts

Metal's signed-order flow adds the agent signature over the exact purchase beside its payment authorization. This is useful evidence about agreed contents and price. It is not evidence that the vendor delivered a correct result. A product can preserve the signed order, independently assess delivery, then choose an acceptance, escalation or compensating payment. [Require a signed order](https://docs.metalntwx.com/agents/require-signed-order)

Mandate payouts can pay an address without a seller service. A stable payment ID supports retries under the same credential and local state. Changing the credential/state directory can create a new payment, so application idempotency remains essential. [Direct payouts](https://docs.metalntwx.com/agents/payouts)

### Clearing and finality

Metal clearing uses the custom x402 `bajillion` scheme. Payers deposit once and sign cumulative payments; services return receipts and certify epochs. Primary docs report about one payment per three seconds per wallet and say withdrawals can take **20 minutes or more**; an older builder guide says ten minutes. Design around current deployment policy rather than hard-coding either number. A receipt is preconfirmed until its epoch finalizes. Lost answers must be resolved by retrying the same pending request before paying another. Parallel jobs need separate durable wallets. This is unsuitable for pretending a five-minute demo includes immediate withdrawal. [Clearing mechanics and failure recovery](https://docs.metalntwx.com/agents/clearing)

### Creative Metal compositions

1. **Revocable supplier authority:** finite mandates allow a procurement agent to pay approved delivery partners, while a revised risk assessment revokes or narrows authority without exposing the treasury key.
2. **Joint budget with independent obligations:** a coalition coordinates work, but every participant's authority and spend remain independently verifiable. App-level optimization chooses contributions; mandates enforce each participant's limit.
3. **Evidence-conditioned settlements:** signed orders define accepted work, while a separate adjudication layer decides acceptance. Metal does not magically verify real-world delivery.
4. **Spend proof used in credit/risk:** verified mandate spend provides a bounded input to an Airwallex bridge/reserve decision. Neither testnet activity nor a signature proves creditworthiness.

## Coinbase: machine-readable prices and controlled payment

### x402 payment semantics

x402 makes payment part of a request: server advertises price/options, client signs a payment, facilitator verifies, the service performs work, facilitator settles, then resource/confirmation return. It is rail-agnostic at protocol level; actual network and scheme support depends on the facilitator and clients. A paid call does not guarantee data accuracy or useful output. [How x402 works](https://docs.cdp.coinbase.com/x402/how-it-works)

Coinbase offers hosted verification and settlement, transaction screening, `exact`, `upto` and batching on supported EVM networks; Solana supports `exact` and `upto`. The current support matrix includes Base/Base Sepolia and Solana/Devnet, among others, **but not Metal**. The `/supported` endpoint is the operational source of truth. Current published pricing is 1,000 monthly on-chain transactions free, then $0.001 each; batch vouchers can amortize on-chain activity. [CDP facilitator support and pricing](https://docs.cdp.coinbase.com/x402/seller/facilitator)

Use `upto` where the buyer must authorize a ceiling and pay actual metered usage. Use `exact` for a fixed report. Batch settlement is useful for many tiny purchases but introduces lifecycle complexity. Do not confuse a generic protocol specification with an end-to-end feature implemented by the chosen facilitator.

### Wallets, credentials and developer availability

Agentic Wallet has CLI and MCP surfaces. CLI can send/trade/pay; the MCP surface is oriented to discovering and paying for services. The CDP SDK provides the clearer route for a web product with explicit application logic, managed wallets and testnet funding. [Agentic Wallet](https://docs.cdp.coinbase.com/agentic-wallet/welcome)

Official SDK examples use CDP API credentials plus a wallet secret, Base Sepolia/Solana Devnet faucet funding, HTTP and MCP clients, and spending controls. Per-payment/rolling caps and network/payee/asset restrictions matter more than making payment automatic. The example matrix explicitly marks `auth-capture` as client-only/mock in that SDK example, so do not advertise it as a live complete settlement flow merely because a client can sign it. [Official x402 SDK examples](https://github.com/coinbase/cdp-sdk/blob/main/examples/typescript/x402/README.md)

AWS AgentCore Payments can compose with CDP wallets and bounded sessions, per root's independent review. This is a natural implementation for an agent buying an additional piece of evidence under a task budget. Metal integration requires its own adapter; no reviewed source establishes AgentCore or Coinbase support for Metal's custom settlement scheme. [AWS AgentCore Payments](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/payments.html)

### Creative Coinbase compositions

1. **Buy evidence only when it changes a decision:** compare the information price with expected reduction in a refund, reserve or payout mistake; stop when enough evidence exists.
2. **Independent verification with a declared budget:** buy a second assessment only when two evidence sources conflict, preserve the receipts, then execute the financial consequence through Airwallex.
3. **Output margin accounting:** connect each paid tool call to a customer job and settled revenue, prevent apparently successful agent businesses from spending more than they earn, and use Airwallex for conventional settlement/accounting.

## Feasibility gates before implementation

| Surface | What is verified | Remaining gate |
| --- | --- | --- |
| Visa TAP | Public specification and runnable sample | Confirm sponsor accepts chosen implementation; production registry/approval separate |
| Visa VIC | Official APIs, MCP toolkit and examples | Obtain actual VIC/VTS credentials and certificates |
| Airi | Official CLI, mandate/credential/result workflow | Allowlist, account, compatible OS, real-purchase testing authorization |
| Airwallex merchant commerce | Separate sandbox path in guide | Merchant enablement, catalogue schema and merchant MCP |
| Metal | Public testnet, faucet, npm package, agent docs | Create RPC endpoint; prove target primitive with one test transaction |
| Coinbase | CDP SDK, faucets, hosted facilitator | Credentials, verify supported testnet scheme, funded test wallet |
| Cross-rail bridge | No end-to-end sandbox bridge verified | Use separately funded ledgers and label simulated funding explicitly |

Suggested integration discipline: implement one strong Airwallex loop first, add one sponsor primitive that materially changes the product, and record the evidence of its real execution. Add a second sponsor only when it removes a concrete product limitation.
