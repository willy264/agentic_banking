# Twelve differentiated ideas: financial-operations starter kits

Research and ideation date: 24 October 2026. Exact kit names verified against the HackerEarth track images saved in this workspace. These are product proposals and demo designs, not claims that integrations have been built. All example amounts and outcomes are synthetic. A suggested sponsor pairing indicates technical relevance, not guaranteed prize eligibility.

The common foundation is explained in [Airwallex technology research](airwallex-technology.md). All four kits should finish with a sandbox financial action or a clearly justified human escalation. A changed fact must cause a changed decision. The LLM interprets evidence; code owns arithmetic, limits, idempotency, ownership and state transitions.

**Verified T:0 composition.** The companion research now confirms invoice/bill/payment reads, accounting-record submission, journal posting and balance-sheet/P&L/cashflow reports, plus a native Airwallex OAuth connection. API keys scope one entity; OAuth can read accessible entities but does not authorize writes. Crucially, invoice/payment reads are eventually consistent and can lag by a nightly export; lists expose `as_of`. Use Airwallex's current balances and financial events as the money truth, and T:0 as accounting context with visible freshness. Posted GL reports update immediately. Journal posting needs its own permission and idempotency key; retain application deduplication beyond the API's limited deduplication window. Sponsor sandbox provisioning is still an access dependency. [T:0 API introduction](https://docs.t0.ai/api/t0-api/index.md), [T:0 MCP setup](https://docs.t0.ai/docs/getting-started/connect-to-our-mcp-server/index.md)

## Starter kit 01 — Adaptive Treasury Controller

### 01A. CashProof — treasury that releases spending only when cash is real

**User/problem.** A cross-border merchant sees strong sales but cannot distinguish spendable proceeds from captures, reserves, refunds and FX movements. The resulting false confidence can cause a payroll or supplier failure.

**Non-obvious mechanism.** Build an evidence graph linking each expected receipt to its order, capture, settlement and ledger entries. Reconciliation confidence becomes an input to the treasury policy: uncertain receipts cannot support autonomous commitments. Instead of merely reporting a discrepancy, resolving it changes which invoice can be funded.

**Why an agent.** Remittance emails, customer credit notes and settlement explanations use inconsistent references. The agent proposes document-to-transaction matches and explains contradictions; deterministic reconciliation verifies totals and the planner calculates feasible transfers.

**Real Airwallex actions.** Read current balances, payment/settlement records and financial transactions; obtain an FX quote; convert; pay a validated supplier; confirm remaining available balances. Use a deposit simulation to stage new funding. No Yield API assumption.

**Sponsor composition.** Claude interprets evidence; T:0 accounting MCP, if its supplied tools support the needed journal/reconciliation operations, provides an independent books comparison; AWS runs the agent and event handler. Base44 is useful for the evidence-to-cash UI. No blockchain is necessary.

**Changed-evidence demo.** The dashboard shows a $12,000 sale but only $7,500 usable. T:0's `as_of` reveals stale accounting context, so the agent checks Airwallex before committing. It postpones a EUR invoice. A settlement event resolves $2,000 of uncertainty; a new customer credit note offsets $500. It changes the funded subset and executes precisely the now-feasible conversion/payout while preserving a $3,000 floor.

**MVP and proof.** One merchant, three currencies, five obligations and six deliberately messy evidence objects. Show the money trail, before/after decision and zero reserve-floor breaches. Main risk is reconciliation scope creep; support a fixed set of transaction types. Ordinary sandbox suffices; T:0 remains optional until its exact tool schema is verified.

### 01B. Continuity Capital — pay the bottleneck that unlocks the business

**User/problem.** A small importer or manufacturer cannot pay all invoices during a supply disruption. Invoice amount and due date alone do not reveal that a cheap repair, certification or component payment unlocks much larger revenue.

**Non-obvious mechanism.** Combine a business dependency graph with a cashflow optimizer. Each obligation has prerequisite work, unlockable receipts, deadline penalties and evidence uncertainty. Paying a prerequisite can be more valuable than paying a large overdue invoice; a shipment delay can destroy that value and change the plan.

**Why an agent.** It extracts dependencies from purchase orders, supplier messages and delivery notices, then proposes graph revisions. Optimization, reserve floors and risk limits are code. The product can explain the causal path: this payment keeps these two orders possible.

**Real Airwallex actions.** Balances, FX quotes/conversions, beneficiary validation and transfers. A changed graph causes the agent to replace an unexecuted plan, never reverse an already sent payout by assumption.

**Sponsor composition.** Claude for documents and plans, AWS for event-driven execution and traceability, T:0 for obligation/book reconciliation where available. A paid weather or logistics endpoint via Coinbase x402 is an optional meaningful input, not needed for the core demo.

**Changed-evidence demo.** Five obligations compete for $18,000 with a $5,000 floor. Initially a EUR calibration bill unlocks shipment. A credible notice says the customer cannot accept delivery for three weeks; the agent drops that near-term revenue assumption, funds an alternative repair and adjusts FX. A late deposit then unlocks one previously deferred obligation.

**MVP and proof.** One factory, six dependency nodes, two shocks and a small enumerative optimizer. Compare with due-date sorting on fulfilled committed orders, not invented profit guarantees. No external enablement beyond funded sandbox. Supply-chain forecasts are supplied demo assumptions, visibly labelled.

### 01C. FlexTreasury — price the right to keep cash uncommitted

**User/problem.** Agencies and seasonal businesses receive attractive early-payment discounts and annual prepayment offers just before uncertain customer collections. A naive savings optimizer buys discounts and loses its ability to survive a delay.

**Non-obvious mechanism.** Model the option value of delaying a commitment. The agent extracts cancellation windows, refundable portions, supplier price-lock expiries and collection uncertainty; a scenario planner compares discounted prepayment with preserving cash under downside cases. It can choose a partial payment, minimum FX conversion or wait-for-evidence rule.

**Why an agent.** The difficult input is contractual optionality buried in prose and conditional promises in customer correspondence. A model can identify the relevant clauses; the probability assumptions, scenario arithmetic and approval boundaries remain explicit and editable.

**Real Airwallex actions.** Read balances; obtain fresh quotes; convert only the approved amount; schedule or execute a supplier transfer. If native transfer approval is unavailable, application approval gates creation.

**Sponsor composition.** Claude contract reasoning, AWS persistent execution, T:0 reconciliation of commitments versus paid invoices. Base44 can make a compelling slider-driven scenario review. Avoid adding financial-investment APIs merely for sponsor coverage.

**Changed-evidence demo.** Paying a vendor early saves $900 but creates a $4,000 shortfall if the client pays late. The agent keeps monthly/partial terms. A verified deposit then arrives before the discount expires; it recomputes and accepts the remaining discount without breaking the floor. A second version introduces a non-refundable clause and shows why the answer differs.

**MVP and proof.** Three agreements, three cash scenarios, one conversion and payout. Measure reserve survival across scenarios and discount captured, both on synthetic data. This remains treasury because the decision allocates cash across obligations; card-based purchasing is not the core.

## Starter kit 03 — Payment Ops Incident Commander

### 03A. OneDebt — distinguish a new payment request from the same unpaid obligation

**User/problem.** A supplier resends an invoice with a new reference after a delayed transfer. AP uploads it again; the bank's idempotency protection cannot help because the new request has a different ID.

**Non-obvious mechanism.** Introduce an obligation identity above transfer identity. The agent relates original invoices, reissued invoices, partial deliveries and credit notes into a proposed debt graph. An execution lock is attached to the economic obligation, so a fresh transfer ID cannot silently bypass duplicate protection.

**Why an agent.** Exact-string matching misses rewritten invoice numbers and changed descriptions. Semantic matching is useful, but ambiguity must escalate; the model cannot declare two debts identical and write off a real supplier claim without evidence.

**Real Airwallex actions.** Query transfer IDs/request IDs, validate a replacement, create a corrected beneficiary if necessary and execute only after original-payment disposition is resolved. Reconcile both original and replacement. Status and amount checks remain deterministic.

**Sponsor composition.** Claude document matching, T:0 invoice/payment ledger matching if supported, AWS durable locks and incident traces. Base44 supplies a concise caseboard. Visa and blockchain are unnecessary here.

**Changed-evidence demo.** A $6,000 transfer is delayed; the supplier sends invoice `INV-841-R` rather than `INV-841`. The agent blocks a second $6,000 payment. A later bank return plus a $1,000 credit note proves only $5,000 remains due. It executes the verified replacement once, preserving lineage and showing that a repeated webhook cannot trigger another payment.

**MVP and proof.** Three invoices, two references, one partial credit, one delayed transfer and one replacement. Measure duplicate obligations caught and overpayment prevented. Ordinary sandbox is enough; use synthetic remittance/credit documents rather than a full ERP integration.

### 03B. Beneficiary Repair Desk — fix failed payments without trusting the correction blindly

**User/problem.** After an international transfer is returned, a supplier emails new banking instructions under deadline pressure. The change might be legitimate, malformed or malicious. Blindly fixing the fields can turn a payment incident into a redirected payment.

**Non-obvious mechanism.** The agent separates three hypotheses: banking-format error, legitimate counterparty change and unverified redirection. It compares bank return data, previously approved counterparty identity and the new instruction. It proposes the smallest correction and binds human approval to the changed fields and supporting evidence.

**Why an agent.** Bank return language and supplier explanations are semistructured. The model can assemble a clear correction case; authoritative beneficiary schemas and independent approval decide what can execute. An email cannot self-verify its own change.

**Real Airwallex actions.** Read the original transfer, query beneficiary schema, validate corrected data, create a new beneficiary where appropriate and initiate one replacement after the original is resolved and funds are accounted for.

**Sponsor composition.** Claude for evidence synthesis; AWS tool identity, isolated credentials and traces; T:0 for vendor master/payment-record reconciliation where its API permits. Do not misuse Visa TAP as proof of a supplier bank account.

**Changed-evidence demo.** A returned transfer cites account detail mismatch. A new invoice changes both the branch code and account owner. The agent escalates. A synthetic, independently verified vendor-master update then confirms only the branch correction, so it rejects the owner substitution and replaces the transfer to the approved beneficiary.

**MVP and proof.** One corridor, two corrected-instruction scenarios, one approval and replacement. Show field-level differences and how execution authority changes. This is not automatic fraud detection; the result is a defensible, bounded repair workflow. Ordinary sandbox suffices.

### 03C. Corridor Control Room — stop incident retries from consuming the cash needed to recover

**User/problem.** A finance team sees many delayed payouts during a bank or corridor incident. Each caseworker independently retries, creating fee leakage, cash reservations and a backlog that makes urgent payments harder to resolve.

**Non-obvious mechanism.** Correlate incidents into shared-cause groups and allocate a recovery budget across them. The agent distinguishes corridor-wide evidence from a single bad beneficiary, then proposes waiting, controlled cancellation, a verified alternative rail or escalation per case. A deterministic scheduler limits concurrent replacements and preserves recovery liquidity.

**Why an agent.** It synthesizes provider notices, bank reasons and supplier deadlines; fixed codes alone cannot judge which communication changes the operational cost of waiting. It explains a group action without assuming all transactions share the same final state.

**Real Airwallex actions.** List/retrieve affected transfers, validate rail-specific beneficiary details, cancel only cancellable transfers and create replacements only after original-state checks. LOCAL versus SWIFT support must come from the actual corridor schema, not inference.

**Sponsor composition.** Claude for incident diagnosis and prioritization; AWS for event processing and observable workflows; T:0 to reconcile fees and suspense entries if supported. Coinbase stablecoin payout is not a default fallback: Airwallex sandbox cannot directly demonstrate that bridge.

**Changed-evidence demo.** Four EUR payouts appear stuck. Three share a banking incident while one has a beneficiary error. The agent holds the group, repairs the isolated error and reserves enough fees for its replacement. New evidence confirms one original completed and two returned; it replans without paying the completed case twice.

**MVP and proof.** Four transfers, a synthetic provider notice and two lifecycle injections. Show no duplicate obligations, constrained replacement spend and fewer unnecessary retries. Ordinary sandbox; alternative rails are conditional on verified corridor support.

## Starter kit 04 — Dispute Response Agent

### 04A. EvidenceDesk — buy the next fact only when it can change the decision

**User/problem.** Merchants waste effort fighting weak disputes and buy expensive evidence for low-value claims. The missing information varies: signature proof, fulfillment history or confirmation that a refund already settled.

**Non-obvious mechanism.** Turn evidence gathering into a bounded decision process. The agent identifies the uncertainty that could flip accept/challenge, compares the cost of another fact with a transparent case-value model, obtains the most useful evidence, and stops when further work cannot justify itself. A small paid API marketplace makes the cost tangible.

**Why an agent.** Different reason codes and contradictory documents require different investigative paths. The model chooses useful evidence questions; code enforces a per-case evidence budget, deadlines and approved action types. Demo estimates must be presented as assumptions, not calibrated win probabilities.

**Real Airwallex actions.** Read disputes and linked payments/refunds, upload evidence, accept a weak case, challenge a supported case and handle a later rejection. Native sandbox dispute simulations supply state changes; the application separately models fees missing from sandbox.

**Sponsor composition.** Strong Coinbase CDP/x402 pairing: pay a self-hosted testnet evidence API and retain its receipt. Metal is an alternative payment substrate if the provided protocol fits; avoid implementing both merely to collect logos. Claude investigates, AWS runs it, T:0 reconciles financial impact where available.

**Changed-evidence demo.** A $25 case is accepted without buying evidence. A $1,400 case justifies a $0.50 synthetic signed-delivery query; that result supports a challenge. A conflicting warehouse timestamp then arrives and changes the next response to escalation. All purchased facts include provenance.

**MVP and proof.** Three disputes, two deterministic evidence endpoints, one actual testnet payment and one Airwallex challenge. Keep testnet and sandbox funding distinct. The key metric is useful evidence cost per resolved case, not a claimed chargeback win-rate uplift.

### 04B. RemedyLedger — stop refund, replacement and chargeback from compensating the same loss twice

**User/problem.** Support promises a refund while finance contests a chargeback and fulfillment sends a replacement. Separate teams can give three remedies for one failed order, or deny a customer because one team falsely assumes another completed the remedy.

**Non-obvious mechanism.** Build an order-level remedy ledger that distinguishes promised, submitted, settled and reversed compensation. The agent reconstructs the chronology from support messages and payment records. It chooses a consistent dispute response based on the actual delivered remedy, not just a refund-request flag.

**Why an agent.** Human messages contain conditional promises and ambiguous wording; the agent connects these to authoritative payment events. Code constrains refundable amounts and prevents an independent second refund while the first is unresolved.

**Real Airwallex actions.** Retrieve linked refunds and disputes, accept or challenge according to supported stage, upload chronology/evidence and verify subsequent refund status. Stage-specific behavior matters: do not assume every dispute acceptance automatically refunds in every stage.

**Sponsor composition.** Claude for chronology; T:0 for the receivable/refund/dispute account reconciliation if exposed; AWS for persistent per-order state. Base44 makes the cross-team case timeline. Blockchain adds little.

**Changed-evidence demo.** A customer disputes non-receipt; support has already submitted a refund. The agent pauses a duplicate compensation request. A refund-failed event arrives, so the customer remains owed and the response changes. Another case shows an actually settled refund, producing a different evidence-backed response. A third genuine failed-delivery case is accepted.

**MVP and proof.** Three orders, a refund state change and one evidence challenge. Show net compensation versus obligation and the customer-facing next action. This exceeds Airwallex's existing AI dispute recommendation by solving cross-system financial consistency.

### 04C. Delegation Forensics — investigate what an AI shopper was actually authorized to buy

**User/problem.** Merchants accepting agentic purchases receive a dispute: the consumer says the agent bought the wrong item, exceeded permission or accepted a substitution. A conventional checkout receipt cannot explain the delegated decision.

**Non-obvious mechanism.** Preserve an authorization-to-fulfillment evidence chain: approved product/terms, authenticated agent interaction, final checkout, payment and delivery. The dispute agent identifies where these diverged. A valid cryptographic agent signature is one evidence component; it is not proof of correct fulfillment or an automatic liability shift.

**Why an agent.** It compares semantic constraints, such as an allergy exclusion, warranty requirement or exact device compatibility, with the item actually supplied. Code verifies signatures, timestamps and exact amount/merchant fields; the model interprets differences and generates an honest case narrative.

**Real Airwallex actions.** Retrieve a payment dispute, link the original payment, upload evidence and accept/challenge/escalate. A synthetic merchant checkout can supply the authorization records, while the Airwallex dispute action remains real sandbox behavior.

**Sponsor composition.** The clearest Visa TAP pairing in these four tracks: implement a verifier with Visa's published sample and appropriate test keys; actual Visa-approved identity requires the sponsor's onboarding. Claude handles semantic comparison; AWS stores/verifies evidence; T:0 reconciles the outcome if available.

**Changed-evidence demo.** A signed agent approved a specific replacement part. The merchant silently substitutes a cheaper incompatible version: accept, despite valid agent identity. A second exact-match delivered order is challenged. When issuer feedback reveals a missing approval event in a third case, the agent escalates rather than inventing authorization.

**MVP and proof.** Three cases, one verifier, a tamper test and one sandbox dispute submission. Treat locally signed samples as test identities, never Visa-certified agents. Measure evidence completeness and false-acceptance prevention, not promised liability protection.

## Starter kit 07 — Portfolio Lending Agent

All three ideas preserve the required revenue-share repayment and reserve-constrained funding loop. Borrowers are already admitted under an explicit preapproved policy; the hackathon agent is not claimed to be a licensed lender or to automate unrestricted credit decisions. All lending amounts are sandbox simulations. Connected-account/platform access is required.

### 07A. RevenueProof — do not collect a revenue share from money that is not revenue

**User/problem.** Revenue-based lenders can mistake owner top-ups, transfers between related accounts, repeated invoice payments or temporarily unsettled sales for actual borrower revenue. They collect too much and then overestimate the cash available for another advance.

**Non-obvious mechanism.** Build a provenance graph for incoming cash. The agent proposes classifications from remittance documents and transaction relationships; confirmed external trading revenue drives the repayment base, while ambiguous money remains unclassified. The platform's available reserve uses actual collected repayments, not forecasted ones.

**Why an agent.** Payment descriptions and invoices often do not agree verbatim. The model helps resolve source and business context; code calculates repayment percentage, remaining obligation and borrower affordability. It does not infer a universal fraud score.

**Real Airwallex actions.** Connected-account balances and incoming-deposit records; platform charges for authorized repayments; connected-account transfers for advances; portfolio report/reconciliation. A charge must not exceed the borrower's available funds.

**Sponsor composition.** Claude provenance reasoning; T:0 accounting classification/reconciliation if its toolkit supports it; AWS durable audit and tenant-scoped execution. An optional paid accounting-verification API could use x402, but local evidence is sufficient for a focused MVP.

**Changed-evidence demo.** Borrower A receives $10,000, initially appearing to support a $1,000 revenue share. A linked document shows $7,000 is an owner capital injection, leaving a $300 repayment under the demo's policy. That $700 difference forces the platform to resize Borrower C's preapproved advance while preserving the floor.

**MVP and proof.** Three borrowers, six incoming transactions and one ambiguous classification requiring approval. Show repayment-base correctness and reserve reconciliation. Do not claim duplicate-invoice detection proves the absence of pledges to unrelated lenders; external registries/data would be needed.

### 07B. ShockGraph — recognize when apparently diverse borrowers depend on the same payer

**User/problem.** Three businesses look independent in a lending dashboard but depend on the same marketplace, enterprise customer or shipping corridor. A common disruption delays all their revenue simultaneously, making independent risk assumptions dangerously optimistic.

**Non-obvious mechanism.** Use invoices and settlement references to build a shared-dependency graph. A shock updates a portfolio cash scenario rather than only the borrower whose message arrived first. The funding decision considers concentration and correlated repayment timing, not just individual wallet balances.

**Why an agent.** Counterparty aliases, platform subsidiary names and contract relationships require document interpretation. Code owns concentration caps and scenario allocation. A plausible shared identity is flagged for review rather than silently merging unrelated counterparties.

**Real Airwallex actions.** Read borrower balances, simulate revenue arrivals, collect permitted repayments, execute a smaller/shifted approved advance and generate the portfolio snapshot. Airwallex supplies cash movements, not a built-in dependency-risk model.

**Sponsor composition.** Claude entity/evidence reasoning, AWS event processing and graph-backed traces, T:0 debtor and ledger context if exposed. Optional paid company verification through Coinbase x402 can be justified if it resolves an uncertain shared debtor.

**Changed-evidence demo.** Two borrowers have unrelated trading names but one dominant payer. An authenticated synthetic payer notice delays both receipts. The agent lowers expected recoveries, delays the full third advance and funds only the safe tranche. A deposit later restores capacity and triggers a second decision.

**MVP and proof.** Three borrowers, five invoices, one shared payer and one shock. Compare portfolio reserve outcomes with a planner that treats expected repayments independently. Access blocker is platform/connected-account enablement; the graph can be built while waiting.

### 07C. Milestone Capital — allocate the next dollar to the smallest complete revenue unlock

**User/problem.** A preapproved borrower's full funding request exceeds portfolio liquidity. A pro-rata partial advance may be useless: half of a required machine repair produces no additional revenue, while fully funding a smaller verified milestone can unlock a customer payment.

**Non-obvious mechanism.** Model advances as discrete, evidence-backed funding milestones rather than a smooth dollar amount. The agent identifies minimum viable uses of capital from purchase orders and supplier quotes; a planner selects complete milestones under the reserve floor. Partial funding is chosen only when it can produce a real outcome.

**Why an agent.** The borrower must explain what each funding tranche accomplishes, and the model tests that account against documents. Deterministic rules enforce preapproved borrower limits, verified use, reserve floors and repayment terms. Treat projected receipts as scenarios, not guaranteed collateral.

**Real Airwallex actions.** Collect revenue-share repayments from existing borrowers; distribute one approved tranche via connected-account transfer; reconcile platform and borrower balances. Optional supplier payout is a separately approved extension, not a requirement for the core kit.

**Sponsor composition.** Claude milestone extraction and contradiction analysis; AWS for persistent approval/execution; T:0 for funding/repayment entries if supported. A later procurement extension can combine controlled cards, but that is beyond the two-week MVP.

**Changed-evidence demo.** Borrower C seeks $12,000; only $6,000 can be lent above the floor. The documents show a $4,500 certified repair unlocks a confirmed customer acceptance, whereas a $1,500 marketing spend does not solve the bottleneck. After Borrower A repays less than expected, the safe capacity drops below $4,500; the agent waits rather than sending an ineffective $3,000. A later actual repayment enables the complete milestone.

**MVP and proof.** Three borrowers, three milestones and two repayment events. Show why partial funding can be economically meaningless and measure completed funded milestones under the cash constraint. Do not frame an additional loan as a way to conceal an existing default; the use-of-funds and independently supported outcome must stand on their own.

## Best candidates from this set

| Candidate | Why it stands out | Build/access risk | Natural sponsor depth |
|---|---|---|---|
| CashProof | Connects accounting certainty to real treasury execution; excellent visual evidence graph | Low to medium | Claude + T:0 + AWS |
| OneDebt | Prevents a real failure that ordinary API idempotency does not solve | Low | Claude + T:0 + AWS |
| EvidenceDesk | Agent chooses whether information is worth purchasing; clear multi-sponsor composition | Medium | Claude + Coinbase x402 or Metal + AWS |
| Delegation Forensics | A new operational need created by agentic commerce itself | Medium; Visa onboarding limits | Visa TAP + Claude + AWS |
| RevenueProof | Repayment provenance changes actual portfolio capacity | Medium/high due to platform enablement | Claude + T:0 + AWS |
| ShockGraph | Novel portfolio-level response to shared dependencies | Medium/high due to platform enablement | Claude + T:0 + AWS |

These ratings are qualitative judgments, not official judging weights.

## Sources for the integrations and boundaries

- [Airwallex balances](https://www.airwallex.com/docs/api/core_resources/balances), [payment data model](https://www.airwallex.com/docs/payments/about-airwallex-payments/payments-data-model), [financial transactions](https://www.airwallex.com/docs/api/finance/financial_transactions): cash versus settlement and source-level reconciliation.
- [Airwallex transfer API](https://www.airwallex.com/docs/api/payouts/transfers), [transfer lifecycle](https://www.airwallex.com/docs/payouts/transfers/create-a-transfer/transfer-statuses): replacement, idempotency and late failure boundaries.
- [Payment dispute API](https://www.airwallex.com/docs/api/payments/payment_disputes/api), [dispute flow](https://www.airwallex.com/docs/payments/manage-payments/disputes/dispute-flow): case actions, existing AI features and stage-specific outcomes.
- [Connected-account funds flow](https://www.airwallex.com/docs/connected-accounts/about/wallets-and-funds-flow), [sandbox access](https://www.airwallex.com/docs/developer-tools/sandbox-environment): customer ownership and platform enablement.
- [Visa TAP specifications](https://developer.visa.com/docs/trusted-agent-protocol/trusted-agent-protocol-specifications), [Visa's sample implementation](https://github.com/visa/trusted-agent-protocol): request signature verification and the distinction between a test identity and an onboarded agent.
- [Coinbase CDP x402 examples](https://github.com/coinbase/cdp-sdk/blob/main/examples/typescript/x402/README.md): funded testnet wallet, payment client, facilitator and spending controls. Use the current SDK rather than hand-coding a possibly stale protocol version.
- [T:0 API](https://docs.t0.ai/api/t0-api/index.md), [T:0 MCP setup](https://docs.t0.ai/docs/getting-started/connect-to-our-mcp-server/index.md): accounting tools and authentication. API introduction and connections documentation were independently retrieved in the root research; their local snapshots are `t0-api-introduction.md` and `t0-connections.md`.
- AWS, Claude, Metal and Base44 are named in the hackathon sponsor image. Their exact sponsor-specific API availability and prize criteria require the companion sponsor research; the proposals above intentionally make no unsupported API-method claims for them.
