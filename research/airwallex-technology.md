# Airwallex technology research for the Agentic Banking Hackathon

Research date: 24 October 2026. This is documentation research, not a claim that any authenticated API calls were executed. Verified capabilities below come from Airwallex's current documentation. Product ideas and architectural recommendations are our inferences. Availability depends on account, region, API version and enablement.

## The useful distinction: developer tools versus the product's runtime

Airwallex provides a public documentation MCP at `https://mcp.sandbox.airwallex.com/docs` and an OAuth-authenticated sandbox Developer MCP at `https://mcp.sandbox.airwallex.com/developer`. They help a coding agent discover schemas and test integrations. The Developer MCP exposes selected sandbox endpoints and simulations, not a guarantee of every API operation. [Developer connectors](https://www.airwallex.com/docs/developer-tools/ai/developer-mcp)

AgentOS is a different toolkit: production MCP, CLI, skills and plugins. Its production MCP is `https://mcp.airwallex.com/mcp`; the CLI supports sandbox and production. Its documented workflows already include contract-to-billing, beneficiary creation, card provisioning and cashflow management. The docs explicitly state AgentOS components do not initiate transfers, FX conversions or payouts. Therefore a hackathon autonomous execution demo should use its own scoped sandbox REST tools and policy gates, rather than assume the production MCP performs money-out. [AgentOS](https://www.airwallex.com/docs/developer-tools/ai/agentos)

## Capability map

| Primitive | Verified capability | Design implication |
|---|---|---|
| Current balances and history | Per-currency available, pending, reserved and total amounts; account types include cash, yield and credit | The agent should reason about spendable cash and timing, not a converted grand total. |
| Global Accounts | Receive bank transfers using local account details and supported payment methods | Give customers or business flows traceable collection destinations, then reconcile incoming funds. |
| FX | Quotes and executable conversions; fixed buy or sell amount; scheduled and settled states | Compare paying in the invoice currency, preserving liquidity and waiting for expected receipts. |
| Transfers | Validate, create, retrieve, cancel, schedule and confirm funding; saved or inline beneficiaries | Execute an approved obligation with explicit identity and lifecycle tracking. |
| Issuing | Virtual cards, configurable limits and restrictions, card updates, authorization/capture simulation | Turn an approved plan into constrained purchasing capability. |
| Payments | Intents, attempts, consent, capture, refunds, disputes and settlement records | Separate a purchase succeeding from its proceeds becoming spendable. |
| Connected accounts | Independent customer wallets, platform charges and distributions, on-behalf-of API calls | A platform can operate customer financial workflows without treating customers' funds as interchangeable. |
| Funds splits | Allocate and release captured proceeds; reverse splits separately from refunds | Release money as fulfillment confidence changes, while preserving a traceable money trail. |
| Webhooks and reports | Asynchronous event notifications, balances and transaction reporting | Build an agent that revises a plan after actual financial events. |

Sources and precise constraints follow.

## Balances, collection and reconciliation

`GET /api/v1/balances/current` returns distinct balance types per currency; history includes source IDs, request IDs and transaction categories. Pending FX funds and reserved outgoing funds cannot be treated as immediately free cash. The presence of `yield` balances does **not** prove there is a generally available sandbox Yield subscription API. No such public self-serve action was verified in this research. [Balances API](https://www.airwallex.com/docs/api/core_resources/balances)

Global Accounts expose bank details and supported currency/rail combinations. Their creation uses country, required currency/transfer features and a request ID. A platform can call on behalf of a connected account. Crucially, multiple Global Accounts should not be presented as isolated cash pots: wallet accounting is separate from collection-account identifiers. [Global Accounts](https://www.airwallex.com/docs/accounts/get-started/global-accounts), [Wallets and funds flow](https://www.airwallex.com/docs/connected-accounts/about/wallets-and-funds-flow)

Financial transactions, payment attempts and settlements provide an unusually rich basis for a causal reconciliation agent. The model can interpret remittance documents; deterministic matching and accounting preserve principal, fees, FX and reserves. A succeeded PaymentIntent is not proof of wallet settlement. [Payments data model](https://www.airwallex.com/docs/payments/about-airwallex-payments/payments-data-model), [Financial Transactions API](https://www.airwallex.com/docs/api/finance/financial_transactions)

The balance activity report v1.2.0 can reconcile available balance, including authorization holds and releases. The transaction reconciliation report contains operational IDs, references, FX and separate fee movements; its record date and settlement date are distinct. This makes discrepancy explanations testable against ledger events, rather than guesses from bank descriptions. [Balance activity report](https://www.airwallex.com/docs/global-treasury/reporting/financial-reports/balance-activity-report), [Transaction reconciliation report](https://www.airwallex.com/docs/global-treasury/reporting/financial-reports/transaction-reconciliation-report)

## FX and payouts

`POST /api/v1/fx/conversions/create` converts wallet balances. A conversion uses both currencies and exactly one fixed amount; a supplied quote must agree with the conversion parameters. The documented statuses include scheduled, settled, overdue and cancelled. Expired quotes and insufficient amounts must be treated as execution exceptions. Some currencies require FX to accompany a payout. [Conversion API](https://www.airwallex.com/docs/api/transactional_fx/conversion)

Transfers can be created against saved beneficiaries, validated before execution and scheduled up to 180 days. For foreign-currency transfers, rate locking and funding choices affect liquidity. Funds for an approval-submitted transfer are not deducted until approval. Availability of approval submission must be requested; it is not safe to assume an out-of-the-box native approval workflow. An application approval screen can gate when the backend calls the transfer API. [Create a transfer](https://www.airwallex.com/docs/payouts/transfers/create-a-transfer), [Transfers API](https://www.airwallex.com/docs/api/payouts/transfers)

Transfer status is a state machine, not a boolean. Even `PAID` can later fail because a local clearing system or recipient bank rejects the transfer. `FAILED` transitions rapidly to `CANCELLED`, and cancellation can follow failure rather than user action. A replacement payment must wait for authoritative disposition and funding reconciliation; simply retrying with a new ID risks a double payment. Native approvals introduce recalled, blocked and rejected states. [Transfer statuses](https://www.airwallex.com/docs/payouts/transfers/create-a-transfer/transfer-statuses)

## Cards and spend controls

Issuing supports virtual cards, single or multiple use, amount limits by interval, activation windows, allowed transaction currencies, merchant brands, categories and countries. The card API can update controls and retrieve remaining limits. Empty/null allowlists can mean unrestricted access, not deny-all. API versions differ, and the documentation warns some card APIs are incompatible with Business Account card/expense products; pin and test a version. None of these controls proves the purchased SKU is authorized. Product-level intent must be checked in the application before checkout. [Cards API](https://www.airwallex.com/docs/api/issuing/cards)

Merchant brand controls offer finer granularity than merchant category codes. The same merchant can generate differently categorized transactions; brand identity and transaction category are distinct signals. Use documented IDs rather than labels as policy keys. [Merchant brand controls](https://www.airwallex.com/docs/issuing/card-controls/authorization-controls/merchant-brand-transaction-categories)

Remote card authorization has a **2.5-second** response deadline; on timeout, the configured default action applies. Airwallex can still reject an application-approved transaction through its internal checks. Do not put open-ended LLM planning on the synchronous authorization path. Have the agent precompute a signed purchasing envelope, then let a fast deterministic service evaluate the transaction. [Remote authorization exceptions](https://www.airwallex.com/docs/issuing/card-controls/remote-authorization/handle-exceptions)

Authorization reserves funds; capture/clearing debits them. FX can change between authorization and capture, and the final billing amount can differ. This supports a valuable travel or procurement product that budgets commitments as well as cash. [Card auto-conversion](https://www.airwallex.com/docs/issuing/transactions/auto-conversion)

## Platforms, liquidity and customer isolation

Connected-account wallets belong to the respective customer. Platform charges and distributions move funds between explicitly identified wallets. This supports payout, payroll, marketplace and lending workflows, but connected-account enablement is a prerequisite. [Wallets and funds flow](https://www.airwallex.com/docs/connected-accounts/about/wallets-and-funds-flow)

The Platform Liquidity Program allows cards for multiple connected accounts to draw on a designated central funding pool, using Program Spending Accounts and funding-source IDs. The API exposes deposits, withdrawals and spending-limit adjustment. It requires a platform account, connected accounts and account-executive setup; it is not a permissionless credit facility and does not imply Airwallex lends to the demo's customers. [PLP setup](https://www.airwallex.com/docs/issuing/get-started/set-up-platform-liquidity-program), [PLP API](https://www.airwallex.com/docs/api/2021-02-28/scale/platform_liquidity_programs)

Funds splits can use manual release, for example after fulfillment. Split reversal and customer refund are different operations. This is a useful foundation for performance-based marketplace settlement, but avoid calling it regulated escrow without a verified legal/product basis. [Manage funds split](https://www.airwallex.com/docs/payments-for-platforms/airwallex-gateway/manage-funds-split)

## Disputes and revenue protection

Merchant-side dispute APIs can retrieve cases, accept them or submit evidence. OAuth integrations need dispute read/write and file-upload scopes; sandbox simulations are available. [Dispute integration](https://www.airwallex.com/docs/developer-tools/partner-connections/integration-guides/dispute-management)

Airwallex already includes `ai_dispute_automation` recommendations and evidence suggestions in PaymentDispute. Consequently, a generic agent that summarizes evidence and decides challenge/accept duplicates an existing feature. Differentiation needs to come from evidence provenance, exception investigation, cross-transaction root causes, avoiding double compensation, or the treasury consequences of dispute clusters. [Payment Disputes API](https://www.airwallex.com/docs/api/payments/payment_disputes/api)

Issuer-side disputes are another distinct surface: an issued card purchase can have a draft dispute, event-level capture reference, evidence files and later submission. This could power a purchasing agent that also recovers money when fulfillment fails, with user approval. [Create issuing disputes](https://www.airwallex.com/docs/issuing/transactions/handle-transaction-disputes/create-disputes)

## Sandbox, enablement and implementation limits

Self-serve sandbox is separate from production and uses simulated funds. Ordinary accounts are instant; Connected Account API testing requires contacting Airwallex. Sandbox REST authentication uses client ID and API key to obtain a bearer token. The sandbox API host is `https://api.sandbox.airwallex.com`. [Sandbox overview](https://www.airwallex.com/docs/developer-tools/sandbox-environment)

Default provisioning includes test wallet funds, beneficiaries and card-issuing API access. PCI access, advanced payment settings, special pricing and many other features need manual setup. Defaults are not guarantees for every account. [Sandbox settings](https://www.airwallex.com/docs/developer-tools/sandbox-environment/sandbox-settings)

Payout state transitions can be simulated; issuing simulation supports authorization, failed authorization, incremental authorization and capture. These are ideal for deliberately injecting the event that forces the demo agent to revise a decision. [Payout simulations](https://www.airwallex.com/docs/developer-tools/sandbox-environment/payouts), [Issuing simulations](https://www.airwallex.com/docs/developer-tools/sandbox-environment/issuing)

Webhooks may repeat and arrive out of order. Validate signatures, deduplicate stable event IDs, persist before acknowledging, and reconcile current object state before an irreversible follow-up. Retries continue for roughly three days. [Webhooks](https://www.airwallex.com/docs/developer-tools/webhooks/webhooks-overview)

Stablecoin payout is an early-access API feature requiring account-manager setup. The documented example uses USDC on Ethereum, and documentation explicitly says sandbox stablecoin-transfer simulation is unavailable. A Coinbase/Base or Metal testnet wallet is therefore **not** automatically fundable from an Airwallex sandbox wallet. Demonstrate separate funded environments and an explicitly simulated bridge unless organizers provide a working demo integration. [Stablecoin payouts](https://www.airwallex.com/docs/payouts/transfers/transfers-via-stablecoin/ui-requirements-for-stablecoin-payout-disclosures)

## Existing examples to exceed

The developer-lab guide contains twelve kits spanning adaptive treasury, incident handling, purchase policy, multi-account spend/payroll, lending, settlement, disputes and agentic commerce. It also identifies gated buyer/merchant commerce access and Metal testnet examples. It explicitly disclaims being official Airwallex documentation; use official docs to resolve conflicts. Its examples are useful baselines, but merely reproducing them is weak originality. [Developer-lab guide](https://airwallexdev.com/guide)

## Non-obvious product directions inferred from the primitives

These are original design proposals, not claims about existing products or guaranteed sponsor eligibility.

1. **Settlement Truth Engine.** A treasury agent detects that apparent revenue is actually a partial capture plus FX fee plus pending reserve, then revises which supplier commitments it can fund. Its evidence graph explains every dollar from order to wallet. Demo a misleading successful payment, then the real settlement event, and show a specific payout becoming permissible. The novel value is turning reconciliation into actionable liquidity certainty. MVP needs one account and no connected-account enablement.

2. **Obligation Graph for Production Continuity.** In manufacturing or cross-border operations, invoices form dependencies: a low-value repair unlocks a high-value shipment, while an early-payment discount is optional. The agent reads contracts and delay notices, builds a dependency graph, then an optimizer selects a feasible payment/FX schedule under reserve and deadline constraints. A new customs delay changes the graph and the agent redirects liquidity. This goes beyond sorting invoices by due date. Sponsor hooks: Claude document reasoning, AWS durable workflows and T:0 accounting reconciliation, subject to the provided sandbox schema.

3. **Commitment-Aware Travel Rescue.** Travel agents face old hotel holds, replacement bookings and uncertain refunds during disruptions. The product models authorized, captured, disputed and refundable commitments separately, frees or contains spending authority, and issues a replacement card restricted to the revised itinerary. A cancellation confirmation changes the spending envelope without pretending the refund is already cash. The demo can use issuing simulations rather than real travel sites. Sponsor hooks: Visa-oriented issuing/intent, with qualification contingent on the actual Visa brief.

4. **Evidence-Priced Supplier Advance.** A platform releases a preapproved advance in tranches as independent shipment or completion evidence becomes consistent. A contradictory document reduces the next tranche, not money already transferred. The platform exposure model and cash floor live in code; the model assesses document contradictions. This differs from generic revenue-based lending by making the funded purpose and evidence lineage visible. Requires connected accounts or an explicitly simplified single-business sandbox demonstration. Do not claim an Airwallex lending-underwriting API was verified.

5. **Buyer–Merchant Remedy Coordinator.** A commerce agent tracks a failed delivery, an already-initiated refund and an open dispute together. It prevents simultaneous refund plus chargeback compensation, selects the viable remedy, and follows the money back into the ledger. Evidence is linked to the actual order and capture, with clear customer approval. The creative angle is financial repair after agentic purchases, rather than another shopping assistant.

6. **Customer-Funds Isolation Auditor with Execution Repair.** A multi-employer or marketplace platform notices a batch planner would use one tenant's liquidity to cover another's shortfall. It produces a valid tenant-separated plan, pays the feasible subset and escalates the remainder. Pair unstructured customer instructions with provable ledger invariants. Demo a seductive aggregate balance that is sufficient while one customer is insolvent. Requires connected-account access for a fully live platform demonstration.

7. **Procurement Capability Compiler.** A model translates a repair ticket, technical specification and procurement policy into a purchase plan. Code binds approval to merchant, product, amount and terms, then provisions only the card authority the plan needs. A seller substitution or changed warranty invalidates the approval even if price stays below the budget. Card controls enforce the available financial dimensions; the application enforces SKU and contract semantics. This is a clear place where probabilistic reasoning and deterministic rails complement each other.

8. **AI Service Margin Governor.** For a business selling AI-powered work, each agent has an order-level revenue envelope, an evidence threshold and paid external tools. The governor decides when buying another verification/API result is economically justified, reduces subagent budgets when provider prices change and reconciles receipts to customer margin. Airwallex funds the business treasury; x402/Metal/Coinbase handles separately funded machine-payment legs where supported. Never imply a native fiat-to-testnet bridge without one. Differentiate from a simple model router through revenue, confidence and liability accounting per customer order.

## Recommended architecture for any finalist

Use the model to interpret documents, surface contradictions and propose contingent decisions. Use deterministic code for money arithmetic, tenant ownership, reserve floors, limit checks, quote expiry, state transitions and duplicate protection. Store a versioned decision object containing the evidence, proposed action, exact payee/amount/currency, policy result and approval. Execute through small backend tools, then verify status and ledger impact. Replan only when relevant evidence changes. A strong demo should make a changed decision visible and finish with an actual sandbox financial-state change.

The strongest low-access-risk directions are Settlement Truth Engine, Obligation Graph and Procurement Capability Compiler. The highest-upside gated directions are Commitment-Aware Travel Rescue with full commerce access, Evidence-Priced Supplier Advance with connected accounts, and AI Service Margin Governor with meaningful sponsor-native machine payments.
