# Claude, AWS, T:0 and Base44: implementation research

Researched 24 October 2026. These are documentation findings and design recommendations; no authenticated services were tested. The hackathon's Product Partners image confirms all four partners. They are tooling/credit partners; the public prize panel does not establish four additional cash-prize tracks.

## Claude: interpretation and contingent planning

Claude can read documents and images, propose tool calls and produce schema-constrained outputs. For these ideas, its valuable job is identifying an invoice dependency, interpreting an unfamiliar contract exception, comparing conflicting fulfillment evidence or deciding which missing evidence to seek. Monetary arithmetic, spending ceilings and irreversible execution should live in application code. A schema-correct tool call is not proof that its facts or authorization are correct. [Structured outputs](https://platform.claude.com/docs/en/build-with-claude/structured-outputs), [Tool use](https://platform.claude.com/docs/en/agents-and-tools/tool-use/overview)

Use a structured decision record such as `evidence_ids`, `interpretation`, `alternatives`, `proposed_action`, `uncertainties`, `replan_trigger`. Ask for a short decision explanation, not hidden reasoning. Financial adapters then validate amounts, currencies, entity, payee, authorization version and current state before any call.

For many tools, tool search can reduce upfront schema volume; programmatic tool calling reduces intermediate round trips; caching helps repeated stable context; context editing removes obsolete tool results. These are useful implementation options, but they should not become the product's claimed innovation. [Managing tool context](https://platform.claude.com/docs/en/agents-and-tools/tool-use/manage-tool-context)

**Design inference:** model uncertainty should affect the next permissible action. A doubtful delivery document could justify buying a second verification, lowering a tranche, or seeking human review. An uncalibrated number emitted as `confidence` is not a validated probability. Use observable evidence completeness and benchmarked error rates where decisions depend on confidence.

## AWS: enforce, run, observe and evaluate

AgentCore provides runtime, identity, gateway, memory, browser/code tools, observability and evaluation services. Use only the services needed by the demo: for example, Runtime for the agent; Gateway for a narrow set of financial tools; Identity for provider credentials; Observability for a trace connecting evidence to action. Long-running money workflows also need persisted application state and recovery semantics. A runtime by itself does not establish exactly-once execution. [AgentCore overview](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/what-is-bedrock-agentcore.html)

AgentCore Policy can enforce rules outside the model at the MCP Gateway. Current docs describe Cedar-compatible policies, default-deny and forbid-wins semantics. Set enforcement to `ENFORCE`; `LOG_ONLY` is observability, not blocking. Policy applies to MCP tool calls, not automatically to every HTTP call an application makes. If direct Airwallex credentials bypass the gateway, application controls must still protect that route. [Policy getting started](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/policy-getting-started.html), [Gateway policy behavior](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/use-gateway-with-policy.html)

**Design inference:** the gateway can answer whether an actor may invoke a tool, while a transaction-safe ledger determines whether enough budget remains. A per-call maximum is not a cumulative budget, and two concurrent approvals must not both consume the same balance. Reserve the obligation in durable state before dispatch, use stable request IDs, and reconcile an uncertain response before attempting a replacement.

Current AgentCore Payments documentation supports x402 and MPP, Coinbase CDP and Stripe/Privy wallet providers, PaymentSession budgets/expiry and payment observability. It can help an agent pay for a piece of information within an explicit research budget. This does not prove support for Metal's chain, custom payment scheme or asset. [AgentCore Payments](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/payments.html)

**Best composition:** Airwallex determines the business's actual spendable treasury; the application earmarks a research budget; AWS constrains tool execution; Coinbase pays a compatible data supplier; Claude interprets the resulting evidence; Airwallex performs the justified financial action. Testnet funding is separate unless an actual bridge has been enabled and tested.

## T:0: the accounting context and closing journal

The official hackathon panel advertises T:0 accounting, documentation, MCP and a sandbox. The public site describes bookkeeping, reconciliation and financial reporting. Its primary documentation is accessible at `docs.t0.ai`, although the browsing tool could not retrieve it; the markdown pages were downloaded directly and preserved in this folder. [T:0](https://t0.ai/), [Official docs index](https://docs.t0.ai/llms.txt)

The documented MCP setup currently points to `https://mcp.scalar.com/mcp/f5272265-5f85-4ec5-b4eb-a44e4f05d957`, authenticated with the T:0 API key. Do not substitute a documentation-directory listing's guessed `docs.t0.ai/mcp` URL. The setup page lists invoice, vendor-bill, payment, counterparty and line-item reads, plus API discovery tools. [MCP setup](https://docs.t0.ai/docs/getting-started/connect-to-our-mcp-server/index.md)

The customer API exposes invoice/bill/payment records, chart of accounts, journal entries and financial statements. An API key resolves to one entity. OAuth can read authorized entities across the organization but is read-only. Record reads can lag by an export cycle, including nightly updates; list results include `as_of`. GL reports read the ledger directly and reflect posted entries immediately. Consequently, T:0 is valuable accounting context, but a stale invoice list is not evidence of current Airwallex liquidity. [API introduction](https://docs.t0.ai/api/t0-api/description/introduction/index.md), [API index](https://docs.t0.ai/api/t0-api/index.md)

Posting a manual journal requires an appropriately permissioned key, matching debit/credit totals, actual GL account identifiers and `X-Idempotency-Key`. The documented duplicate protection window is one hour, so keep application deduplication for the entire workflow lifetime. Foreign-currency entries must balance in both transaction and functional currency. Amount fields use currency atoms: for example, USD has 100 atoms per unit. This differs from Airwallex's major-unit convention and Metal's token base units. [Journal entry API](https://docs.t0.ai/api/t0-api/post/v1/journal-entries/index.md)

Record submission is all-or-nothing within a batch and returns 202 for accepted processing, not completed posting. Identical records are deduplicated; the key needs a Custom API connection. T:0 lists an Airwallex OAuth connection. Hackathon sandbox provisioning and which write permissions participants receive still need to be established. [Record submission](https://docs.t0.ai/api/t0-api/post/v1/records/index.md), [Available connections](https://docs.t0.ai/docs/connections/available-connections/index.md)

**Best composition:** read the accounts-payable context from T:0; fetch present cash and transfer status from Airwallex; execute; then post or prepare a reconciled journal using the resulting financial IDs. If Airwallex syncing already creates the entry, match that entry instead of creating a duplicate. During a demo, display accounting freshness and pending synchronization explicitly.

## Base44: the review and operations application

Base44 supplies a managed backend, authentication, entities, row/field permissions, TypeScript/Deno functions and hosting. It is a credible way to build the operator's evidence screen, approval queue, tenant workspace and decision timeline quickly. Its documented entity schemas are not enforced by the database; validate financial data in the backend. [Backend features](https://docs.base44.com/developers/backend/overview/features)

Functions can call external APIs with protected credentials, receive webhooks and run from scheduled/database events. The documented execution limit is five minutes. Direct HTTP webhook invocations lack an authenticated app-user context, so verify the provider signature and derive ownership before using service privileges. Use persisted jobs rather than holding an HTTP request open while waiting for a bank transfer or Metal withdrawal. [Backend functions](https://docs.base44.com/developers/backend/resources/backend-functions/overview)

Current developer docs describe code editing and GitHub workflows; paid-plan requirements apply to code editing in the app editor. Confirm what the hackathon credit allocation unlocks. A separate backend/CLI offering is documented as beta. Base44's role in a finance demo is the accessible product interface and supported backend features, not an assumed banking ledger. [Developer tools](https://docs.base44.com/documentation/building-your-app/developer-tools), [Backend introduction](https://docs.base44.com/developers/backend/overview/introduction)

## Existing products raise the novelty bar

Ramp already markets AI policy review and procurement research agents. Airwallex already exposes AI dispute recommendations and AgentOS financial workflows. Therefore PDF policy interpretation, a chat window over balances, generic challenge-or-accept chargeback logic and cards with spending caps are weak standalone novelty claims. [Ramp Policy Agent](https://support.ramp.com/policy-agent-overview/), [Ramp procurement agents](https://support.ramp.com/getting-started-with-ramp-procurement-policies/), [Airwallex dispute automation](https://www.airwallex.com/docs/payments/payment-operations/disputes/dispute-automation), [Airwallex AgentOS](https://www.airwallex.com/docs/developer-tools/ai/agentos)

The proposed ideas should instead expose a specific neglected decision: which dependency to fund, how much evidence is worth buying, whether an approval still covers a changed order, who owns a delayed payment, or how a return changes a seller's reserve. These are novelty hypotheses relative to the reviewed examples, not claims that no competing product exists.
