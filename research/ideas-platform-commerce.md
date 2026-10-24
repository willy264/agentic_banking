# Twelve differentiated concepts for official tracks 02, 05, 06 and 08

These are original design proposals, not existing sponsor features. They extend the stated starter-kit decision and end in a real Airwallex sandbox state change. They deliberately avoid making the product merely a chat window around a starter kit. All business data, contract terms and operational events can be synthetic. Sponsor feasibility and links are in [sponsor-technology.md](sponsor-technology.md); Airwallex API details are in [airwallex-technology.md](airwallex-technology.md).

The highest-potential concepts in this group are **Evidence Dividend** (08A), **Cold-Chain Continuity** (05A), **GrantClock** (02B), and **One Worker, Three Employers** (06A). Rankings are design judgments, not predictions of judges' preferences. After considering access gates, my best overall build choice from this group is **GrantClock**; my strongest deliberate **Metal Award** build is **Evidence Dividend**, conditional on obtaining Airwallex platform access early. Detailed reasoning is below.

**Sponsor and evidence honesty.** Sponsor names below describe possible product roles, not automatic award eligibility or a recommendation to integrate everyone. Only a functioning integration with the required sponsor plus Airwallex can support an award claim. A Visa-branded issued card alone is not a demonstrated Visa toolkit integration. T:0 supplies accounting context that may lag; Airwallex balances and transaction state remain the source for executable cash. A self-hosted x402 evidence API with synthetic records proves payment, budget controls and the decision workflow; it does **not** prove an independent third-party evidence network, real delivery verification, or validated predictive accuracy. State that clearly in the submission and video.

## 02 — Intent-Bound Purchase Agent

Track obligation: choose SaaS terms and make the choice enforceable through a virtual card. A fresh idea still needs to show actual card issuance/limits and an authorization the policy rejects.

### 02A. ExitPlan — a software buyer that prices the cost of leaving

**User and problem.** A small company changing its data stack must decide whether to renew its current SaaS provider annually, monthly, or temporarily operate two systems. The apparently cheapest renewal can lock the company into data-export fees, a notice period or a migration dependency that makes cancellation operationally expensive.

**Unexpected composition.** Treat a software subscription as both a cash commitment and a dependency in a migration plan. Claude extracts cancellation terms and export requirements; a small dependency graph and cash simulator calculate the total cost of each viable sequence. T:0 supplies accounting context and commitments; Airwallex supplies current executable balances and creates separate cards for the old and new provider with controls reflecting the chosen overlap period. Visa TAP can authenticate the agent to the demo vendor; VIC can bind the purchase instruction if enabled.

**Decision change.** Initially choose a one-month overlap and the new vendor's annual discount. Then a migration test reveals that the old system's export requires a premium tier. Recompute: buy one month of premium access, switch the new subscription to monthly, preserve the cash floor, and delay cancellation until export checks pass. A scope change must invalidate the original purchase approval.

**Financial/demo outcome.** Show two cards, a valid monthly charge, a rejected attempted annual charge, and the remaining reserve. Later freeze the obsolete card when the migration evidence meets an explicit acceptance rule.

**Small MVP.** Two SaaS products, three subscription terms, five dependency steps, one changed export condition. No actual migration engine. Measure avoidable committed spend, cash-floor breaches and unsupported assumptions.

**Critical boundary.** Card controls enforce amount/currency/category and available supported restrictions; they cannot themselves prove export completion or cancel a vendor contract. Those are application checks and a human/vendor workflow. Avoid marketing a frozen card as cancellation of a legal obligation.

**Why it is differentiated.** The agent optimizes the cost of retaining reversibility, rather than only comparing annual discount with monthly cash flow.

### 02B. GrantClock — purchase the right SaaS term for money that expires

**User and problem.** A research lab or funded accelerator has unrestricted operating money plus grants whose eligible service periods and categories differ. The grant may expire next month, while an annual software bill covers the following year. Choosing the longest prepaid term can spend the right amount for the wrong purpose.

**Unexpected composition.** T:0 accounting records and supplied grant agreements feed an application funding ledger. Claude extracts the supplied grant's service-date and category conditions; deterministic code allocates eligible and ineligible portions and reconciles the accounting context to Airwallex's current balances. Airwallex issues a virtual card sized to the permitted purchase. Optional Visa TAP authenticates the agent to a demo vendor, or VIC provides the purchase-authorization flow if credentials are enabled; neither is required for the core track. Without VIC, use an application approval receipt and label it accordingly: TAP does not replace purchase authorization. AWS can store the evidence and decision trace.

**Decision change.** A vendor offers monthly and annual terms. Under the original funding window, the annual discount is affordable and eligible. Before purchase, an approved grant amendment shortens the eligible service period: the annual subscription now extends beyond it, while one immediate monthly subscription lies wholly inside it. The agent purchases that eligible month, asks for approval to use unrestricted money for later service, and blocks the annual authorization. Supplied grant terms explicitly determine whether future coverage or partial allocation is permitted; the demo must not infer a universal grant rule.

**Financial/demo outcome.** A correct card charge and journal allocation, one rejected charge, no grant overspend, and an explicit funding source for each service month. The before/after view makes restricted cash distinguishable from spendable cash.

**Small MVP.** Two supplied grants, one unrestricted pool, three SaaS offers, two sample invoices. No legal/tax rule engine. Measure eligible cash preserved and allocation correctness against a hand-checked fixture.

**Critical boundary.** Eligibility follows synthetic terms approved for the demo. A model's interpretation is a proposal until verified; issuing a restricted card does not enforce service dates or grant law at the network. If T:0 sandbox tagging is limited, keep the restricted subledger locally and reconcile to its journal entries.

**Why it is differentiated.** It explains why a business with ample cash can still be unable to buy a particular subscription, then executes an appropriate alternative.

### 02C. SeatRescue — temporary software access that ends with the incident

**User and problem.** An operations team urgently needs extra SaaS seats during a security incident, production launch or customer migration. Emergency purchases often become permanent renewals, while cancelling too early can destroy the evidence or access needed to complete the work.

**Unexpected composition.** An incident's evidence checklist becomes the lifecycle of the purchase. Claude reads the vendor terms and incident runbook; code compares temporary, monthly and annual offers against projected incident duration and reserve needs. Airwallex issues a card for the approved short-term purchase. A signed purchase instruction can tie authority to the incident and exact terms.

**Decision change.** The initial plan buys ten monthly seats. A vendor support response says audit-log export requires its enterprise add-on; the agent evaluates whether to extend five seats, buy the add-on or preserve access while seeking approval. Once the export is verified, it freezes the emergency purchase card and opens the vendor cancellation task, rather than silently assuming the subscription has ended.

**Financial/demo outcome.** Show the emergency purchase, a changed approval, a blocked renewal attempt, and evidence that the necessary export remained available until closure.

**Small MVP.** One incident, two providers, three terms, a synthetic export artifact and one attempted renewal. Measure days of unnecessary exposure avoided and whether closure conditions were satisfied.

**Critical boundary.** The demo validates artifact presence/hash and declared acceptance criteria, not the technical completeness of a real forensic investigation. Cancellation remains distinct from payment blocking.

**Why it is differentiated.** Spend authority is tied to an operational outcome, with a deliberate rule for when temporary access must remain available.

## 05 — Platform Spend Controller

Track obligation: issue customer cards and allocate scarce platform bridge funds when deposits arrive late. Customers remain distinct connected accounts; the platform's bridge capital is its own money. A proposal should include at least one customer that is refused or deferred.

**Common execution spine.** Fund each customer separately, issue cards on its behalf, simulate valid/declined authorizations, allocate only the platform's bridge capital, collect the platform's monthly fee with `POST /charges/create`, and reconcile the bridge and fee after delayed customer deposits. Include fees in available-cash tests. Demonstrate card declines using supported controls such as amount, currency or merchant category. A card network does not know the purchase's SKU, project, repair purpose or grant eligibility; enforce those conditions before execution in the application and do not claim the network can block every off-purpose purchase.

### 05A. Cold-Chain Continuity — bridge the repair that saves the shipment

**User and problem.** A card platform serves small refrigerated-logistics operators. Three customers have late incoming deposits and urgent card expenses, but the platform can bridge only one or two. A flat rule such as oldest customer first can fund routine fuel while a time-sensitive repair goes unpaid and a shipment spoils.

**Unexpected composition.** Operational evidence is converted into a bounded capital-allocation decision. Claude reads a repair quote and delivery contract. Code compares the declared cost of delay, available evidence, repayment sources and concentration limits. An x402 purchase buys a temperature-log assessment only if its value could change which customer gets funded. In the MVP this is our own synthetic verifier; a real independent assessment provider is a future integration, not an accomplished fact. Airwallex transfers platform money to the selected connected account and sets the customer's repair card controls. T:0 records the advance and recovery.

**Decision change.** Initially bridge the largest customer. Then the smaller operator's temperature evidence shows a shorter intervention window while the large customer's expected deposit is contradicted by its payer. Reallocate the uncommitted bridge budget, fund the small repair, defer the large one and preserve a platform reserve.

**Financial/demo outcome.** One bounded bridge, a valid repair authorization, an attempted charge in an excluded merchant category declined, an unfunded customer clearly escalated, and repayment collected after its delayed deposit arrives. A different-purpose charge within an allowed category remains an application-review case.

**Small MVP.** Three operators, one repair quote each, two synthetic sensor traces and one paid verifier endpoint. Show money and decisions, not a logistics dashboard. Metrics: platform reserve, bridge amount recovered and forecast loss under declared assumptions.

**Critical boundary.** Sensor data and projected spoilage loss are synthetic scenarios, not validated credit scores. Approve bridge risk with explicit policy; the model cannot invent repayment certainty. Coinbase or Metal buys the evidence, while the bank bridge is Airwallex; any cross-rail funding is represented separately.

### 05B. MarginFence — agency cards backed by collectible client work

**User and problem.** Marketing agencies pay ad platforms and production tools before clients reimburse them. A platform issuing cards to agencies must decide whose late deposit to bridge, but a large campaign is not necessarily a healthy one: revisions, credit notes and disputed pass-through costs can erase the margin.

**Unexpected composition.** T:0 invoices, credit notes and billable commitments feed job-level margins. Claude identifies whether a client statement actually accepts the reimbursable work or merely forecasts approval. Code grants bridge capacity against configured, evidenced receivables and keeps unrelated campaigns isolated. Airwallex funds the selected agency and constrains its campaign card. Metal mandates are a meaningful optional extension for an agency's paid agent tools; both card and tool spend consume the same application budget.

**Decision change.** Two campaigns look equally profitable. One client withdraws approval for a video deliverable and disputes the invoice. The agent reduces that campaign's remaining authority, declines its bridge, and funds a smaller accepted campaign instead. Already incurred costs remain recorded rather than being erased by the revised plan.

**Financial/demo outcome.** A connected-account bridge and permitted campaign charge, a declined charge exceeding the supported card amount limit, a receivable correction, and a recovery when the client pays. Campaign-purpose validation stays in the application because card limits do not inspect the underlying creative work.

**Small MVP.** Three agencies, one campaign each, an invoice/approval/dispute packet and a limited bridge pool. Metrics: funded collectible exposure, reserve preserved and no spend allocated twice.

**Critical boundary.** A client email is evidence to evaluate, not a guarantee of collection. If Metal is included, one agent mandate represents actual tool-spend controls; do not pretend Metal can directly enforce a card-network transaction.

### 05C. CorrelationBrake — stop bridge funding from following one bad payer

**User and problem.** A vertical card platform sees ten apparently independent customers awaiting deposits. In fact, several depend on the same wholesaler, marketplace or insurer. Funding each account under an individual limit can concentrate the platform's entire bridge pool on one delayed upstream payer.

**Unexpected composition.** Use T:0 invoice counterparties and remittance data to build an evidence-backed payer dependency graph. Claude resolves naming variants with confidence and sources; deterministic limits cap aggregate exposure to a common payer. Airwallex still manages each customer's card and wallet separately. AWS supports event-driven recalculation and an audit trail. Visa TAP is relevant only if the suppliers accept authenticated agent purchase requests; it is not needed for the core risk model.

**Decision change.** Three customers qualify independently. A new remittance message reveals that two receipts originate from the same stalled settlement batch. The agent treats them as correlated, funds one critical customer within a group cap, allocates the remaining bridge to an independent payer, and defers the third.

**Financial/demo outcome.** Show connected-account transfers and constrained card use, plus individual and payer-group exposure after execution. Duplicate payer aliases should not create additional capacity.

**Small MVP.** Three tenants, two real-world-counterparty identifiers in synthetic documents, two alias strings and one late batch. Metrics: largest upstream-payer concentration, preserved reserve and customer-fund isolation.

**Critical boundary.** Entity matching can be ambiguous; uncertain merges need review. The product is not an automated real-world underwriting decision engine. This adds portfolio structure to the existing bridge-funding task without requiring a production credit bureau.

## 06 — Multi-Employer Payroll Executor

Track obligation: run payments for at least three employer connected accounts, handle a shortfall and prove one employer never funds another. The concepts below use contracted gross payable amounts already supplied/approved; they do not infer tax or employment law.

**Common execution spine.** Read each employer's current balance, price its approved payroll including payout/FX costs and the platform payroll fee, convert on its behalf, validate beneficiaries, send and verify its transfers, collect that employer's fee with `POST /charges/create`, and reconcile independently. Employer identity must be present on every scoped call. Replanning cannot omit fees or use another employer's deposit to satisfy the shortfall.

### 06A. One Worker, Three Employers — one payslip view with three separate obligations

**User and problem.** A staffing platform coordinates a contractor who works for several employers in the same week. The contractor wants one clear view of earnings, while the platform needs to preserve who owes each amount and whose funds can pay it. Aggregating the worker's earnings must not turn employers' wallets into a common pool.

**Unexpected composition.** Build a graph of accepted work units, employer approvals and payable lines; keep the employee-facing summary separate from settlement ownership. Claude extracts references from timesheets and client acceptance notes; code computes approved pay and links every line to one employer. T:0 stores employer-level payables and reports. Airwallex runs FX and transfers on behalf of each employer, even when multiple transfers share a beneficiary.

**Decision change.** Employer A is funded, B is short and C receives a deposit mid-run. The contractor's dashboard shows the total earned, but the executor pays only the lines each employer can fund and explains B's unresolved amount. Then an imported timesheet reassignment arrives: already paid work is not silently re-billed to another tenant; it becomes a correction requiring approval.

**Financial/demo outcome.** Three distinct settlement trails, one unresolved obligation, no cross-employer cash movement, and a consolidated worker statement that still identifies each payer.

**Small MVP.** Three employers, two contractors, six work units, one duplicate timesheet and one correction. Metrics: zero misallocated funds, no duplicate work-unit payment and statement-to-transfer reconciliation.

**Critical boundary.** Do not withhold legally owed wages based on a model decision. Use synthetic contractor invoices with approved amounts; disputed or underfunded lines are escalations. The signature proves approval provenance, not labor-law compliance.

### 06B. NetPromise — payroll that preserves the amount the contractor was promised

**User and problem.** Different employers promise contractors different payment terms: one pays a fixed foreign-currency amount, another pays a source-currency amount, and a third pays fees so the contractor receives a specified net amount. A single “convert and pay” function can quietly break one of those promises when exchange rates or payout fees change.

**Unexpected composition.** Claude extracts the supplied contract's currency/fee promise into a typed instruction; an employer approves it once. Code distinguishes gross amount, recipient amount, fee payer and allowed timing. Airwallex obtains quotes and executes employer-scoped FX/transfers. T:0 reconciles actual costs to the specific promise; AWS event processing catches expired quotes or late funding.

**Decision change.** A quote changes and the third employer can no longer cover net pay plus fees while preserving its required reserve. The agent uses another available currency belonging to that same employer if allowed, or stops and escalates. A surplus in employer A's account never becomes a solution for C.

**Financial/demo outcome.** Two fulfilled payment promises, one well-defined shortfall, a refreshed quote and a ledger that distinguishes contractor pay from employer FX/fee expense.

**Small MVP.** Three employers, one promise type each, two currencies, one quote expiry and one delayed receipt. Metrics: promise variance, fully accounted fees and no stale-quote execution.

**Critical boundary.** Recipient-net amounts and fees must be supported by the actual corridor/API; where fees are not guaranteed, show a quote/estimate and escalate rather than claim guaranteed receipt. This is not an FX-prediction product.

### 06C. Payroll Lockstep — stop a last-minute correction from producing two payrolls

**User and problem.** A payroll platform receives an approved pay run, then amended bank details or corrected timesheets while payments are already in flight. Operators need to know which lines can still change, which have become immutable, and which require a separate adjustment run.

**Unexpected composition.** Use versioned, employer-signed payroll manifests: each line binds employer, contractor, currency, amount and beneficiary version. Claude compares amendments and explains their scope; code controls revision and settlement. Airwallex executes the approved manifest, tracks transfer states and permits a new adjustment only after checking the original. T:0 records the original obligation and separate adjustment rather than overwriting accounting history.

**Decision change.** Employer B submits a corrected run while A is paid and C is awaiting funds. A bank-detail change affects only one unpaid B line; the previous approval cannot authorize its new beneficiary. A late C deposit restarts only C. A duplicate webhook neither reopens A nor sends B's superseded instruction.

**Financial/demo outcome.** A paid original, a reapproved corrected line, one deferred employer and an adjustment trail. The user sees precisely what changed and why only a subset of the run was replanned.

**Small MVP.** Three employers, six pay lines, two manifest versions and an intentionally repeated webhook. Metrics: exactly one settlement per authorized obligation/version, approval invalidation correctness and tenant isolation.

**Critical boundary.** This includes payment-incident mechanics, so keep the demo centered on versioned multi-employer payroll, not generic retries. Do not promise cancellation of a transfer after it is irrevocable. Metal is optional for a separate signed subcontractor acknowledgment, not necessary to prove bank settlement.

## 08 — Marketplace Settlement Agent

Track obligation: choose seller reserves, revise them when evidence changes, pay net proceeds and reconcile retained liabilities. Reserve release must not be confused with new income, and on-chain test tokens cannot be counted as Airwallex cash.

### 08A. Evidence Dividend — buy a little certainty to release trapped seller cash

**User and problem.** A marketplace retains seller reserves because delivery or acceptance evidence is incomplete. Small sellers suffer long cash delays, but releasing every reserve exposes the platform to refunds. The missing product is an agent that decides when it is economically worthwhile to investigate and release cash early.

**Unexpected composition.** Claude identifies the specific evidence gap in a disputed order. Code compares the price and likely decision impact of a verification with reserve exposure and seller liquidity needs. Coinbase x402 or Metal pays for a bounded verification call; its response is evaluated against declared evidence rules. Airwallex releases a revised net payout through connected accounts, and T:0 preserves the remaining liability. The MVP verifier is self-hosted and returns synthetic evidence: the live integration proves a paid workflow, not access to independent delivery truth.

**Substantive Metal variant.** Select Metal rather than integrating two interchangeable payment rails. Bind a mandate that permits two verifier addresses, a small per-call cap and one total investigation budget. Give every evidence order an immutable, versioned resource route that maps to the exact order ID, evidence product and terms hash, then require its signed offer at the quoted price. Metal's native signature covers resource, price, payee and network; it does not automatically bind arbitrary query/body fields. Demonstrate an allowed payment, a rejected unapproved payee, and a provider price increase that exceeds remaining authority; only the owner can replace the mandate. The verifier response remains a separate, potentially inconclusive artifact. After evaluating it, release a sandbox Airwallex reserve through a real connected-account transfer. The on-chain record proves spending authority and the referenced purchase; the immutable application mapping proves which terms that resource represented; the Airwallex ledger proves the financial consequence. Use `exact` payments to avoid clearing withdrawal timing in the MVP.

**Decision change.** A delivery scan suggests completion, but a customer complaint conflicts with it. The agent buys a signed recipient-confirmation assessment for this order instead of paying for checks on every order. Positive evidence releases only its attributable reserve; inconclusive evidence leaves the reserve and escalates. A later carrier incident affects different orders separately.

**Financial/demo outcome.** Show a real testnet paid call, the new evidence, an actual sandbox seller transfer, and the reserve equation before and after. Include one case where the agent refuses to buy evidence because the price exceeds its modeled value.

**Small MVP.** Three sellers, six orders, two deterministic verifier endpoints, one conflicting claim. Metrics: verification spend, reserve released, unresolved exposure and comparison to a fixed-reserve baseline.

**Critical boundary.** A signed verifier response proves provenance, not truth. Use a clearly synthetic evaluation set and show uncertainty. The expected-value estimate is a tunable policy assumption, not a claim of calibrated refund prediction. Keep bridge/faucet funding distinct.

**Why it stands out.** Sponsor micropayments become working-capital infrastructure: the output is demonstrably more cash released for justified reasons, not merely an API call paid with crypto.

### 08B. RescueSplit — settle a rescued order across the original and replacement seller

**User and problem.** A marketplace seller cannot finish an order after part of the work has been accepted. Refunding everything loses the buyer and harms the performing part of the supply chain; paying the original seller in full leaves no funds for a replacement.

**Unexpected composition.** Represent the order as separately accepted milestones and explicit replacement terms. Claude compares the failure report with the buyer's original acceptance criteria and proposed rescue quote. Code computes earned proceeds, replacement cost and reserves without paying beyond collected funds. Airwallex settles the authorized shares to two connected accounts; T:0 reconciles the split against the original customer payment. Metal is an optional extension only if a distinct paid quote or assessment service is useful: its buyer agent countersigns the seller's offered order alongside a mandate-backed payment. Do not describe that as the seller signing a fiat replacement payout, and do not pay the replacement's full price on both rails.

**Decision change.** Original seller A has earned one accepted milestone but cannot deliver the second. Agent compares refund versus rescue; when a replacement quote rises, it declines an over-budget rescue and asks for revised buyer approval. Seller B is paid only after the specified acceptance event; seller A keeps only the undisputed earned amount and appropriate reserve.

**Financial/demo outcome.** One customer payment, two seller payouts, a retained reserve and a balanced settlement equation. Include a rejected attempt to pay both sellers for the same milestone.

**Small MVP.** One two-milestone order, three sellers, two replacement offers and two approval events. Metrics: avoided duplicate payout, retained coverage and recovered completion under scenario assumptions.

**Critical boundary.** Contractual permission to reassign work and offset proceeds must be explicit demo inputs. This is a marketplace ledger and conditional payout workflow; do not call it regulated escrow or claim cross-chain atomic settlement.

### 08C. CommonCause Reserves — follow a defect across sellers without freezing everyone

**User and problem.** Several marketplace sellers use the same upstream manufacturer, fulfillment warehouse or software component. A defect can spread across their orders, while a blanket reserve increase for every seller unfairly traps unrelated cash.

**Unexpected composition.** Build an order-to-supplier dependency graph from invoices, SKU/batch identifiers and fulfillment records. Claude resolves document references with evidence, while code computes exposed orders and bounded reserve changes. A paid x402 verification can confirm a batch identifier when it would materially change coverage. Airwallex pays unaffected proceeds and retains reserves for affected obligations; T:0 tracks liability by seller and cause.

**Decision change.** A recall-like defect alert first appears to affect seller A. New evidence ties a subset of seller B's orders to the same batch, while seller C uses a different batch. Agent increases A/B reserves only on exposed orders, releases C's normal payout and records what evidence would permit release later.

**Financial/demo outcome.** A visible cause-to-order map, revised reserves for two sellers, an unaffected payout for the third and a balanced platform ledger. Ambiguous batch IDs remain in review rather than being confidently merged.

**Small MVP.** Three sellers, two suppliers, eight orders, a synthetic defect notice and one uncertain identifier. Metrics: exposure covered, unaffected cash released, false attribution and reserve conservation.

**Critical boundary.** Use a declared reserve policy and synthetic defect information; do not imply certification of real product safety. The innovation is precise financial propagation of evidence, not a general fraud score or a blanket carrier-failure rule.

## Comparison for choosing a submission

| Concept | Distinctive mechanism | Sponsor with substantive role | Main access dependency | Relative build complexity |
| --- | --- | --- | --- | --- |
| ExitPlan | Price migration reversibility and overlapping terms | T:0; Visa if enabled | Basic cards; VIC optional | Medium |
| GrantClock | Separate restricted cash from eligible SaaS purchase | T:0; Visa optional | Basic cards; grant inputs | Medium |
| SeatRescue | End purchase authority when evidence-dependent work ends | Visa + T:0 | Basic cards; VIC optional | Medium |
| Cold-Chain Continuity | Pay for operational evidence before scarce bridge allocation | Coinbase/Metal + T:0 | Connected accounts + platform payments | High |
| MarginFence | Bridge only evidenced, still-collectible campaign exposure | T:0; Metal optional | Connected accounts + issuing | Medium-high |
| CorrelationBrake | Aggregate bridge exposure by upstream payer | T:0 + AWS | Connected accounts + issuing | Medium |
| One Worker, Three Employers | Aggregate presentation while preserving obligation ownership | T:0 + AWS | Three connected accounts + FX/payouts | Medium |
| NetPromise | Execute distinct currency and fee promises without pooled funds | T:0 + AWS | Three accounts; corridor behavior | Medium |
| Payroll Lockstep | Bind payroll revisions to approval and payment finality | T:0 + AWS | Three accounts + webhooks/simulation | Medium |
| Evidence Dividend | Buy decision-relevant evidence to release reserves | Coinbase or Metal + T:0 | Platform settlement + funded testnet | Medium-high |
| RescueSplit | Reallocate settlement for an explicitly approved rescue | T:0; Metal only for a distinct paid service | Platform settlement; consent model | High |
| CommonCause Reserves | Propagate shared-cause exposure precisely across sellers | T:0; x402 optional | Platform settlement | Medium |

Every concept should demonstrate: goal -> initial decision -> contradictory new evidence -> revised decision -> real sandbox action or justified escalation -> reconciled result. Keep balances, limits, identities, approval scopes, duplication prevention and finality checks in code. The model reads and proposes; deterministic policy and actual financial rails enforce the consequential boundary.

## Final nominations and hard tradeoffs

**Best overall build from these twelve: GrantClock (02B).** It is specific, easy to explain, and demonstrates a financial distinction that a generic cash dashboard misses: positive cash is not necessarily eligible cash. It fits the exact SaaS-terms/card-control track and can execute with basic sandbox issuing, without waiting for connected-account enablement, a real merchant allowlist, a production bridge or an external evidence vendor. Its demonstration contains a changed document, a revised purchase term, an accepted monthly charge, a rejected annual charge and a reconciled funding allocation. Keep the scope to supplied funding terms and show extracted rules for human review; otherwise the product becomes an unsupported legal-interpretation system. Build the core first, then add T:0 and a genuine Visa protocol flow if time/access justify them. It is not automatically a Visa Award candidate.

**Best Metal Award build from these twelve: Evidence Dividend (08A), using the substantive Metal variant above.** The economic reason to buy a paid service is clear: obtain potentially useful evidence before changing seller reserves. Mandate enforcement and signed orders make Metal integral to the investigation budget, while Airwallex executes the actual payout decision. This is a stronger combination than attaching an unrelated token reward to a marketplace. It also has two hard dependencies: Airwallex platform enablement and a working Metal testnet mandate payment. Verify both immediately; otherwise it is not the best short-window build. A testnet payment to our own verifier is real technical integration, but its synthetic result demonstrates only a scenario, not measured fraud reduction, independent carrier verification or a working third-party information market. Do not present released reserve as profit or a validated improvement in risk. Show both evidence acquisition and a deliberate refusal to buy, and report the result only against the declared synthetic baseline.

**Why the others do not win these nominations.** Cold-Chain Continuity adds a hard-to-validate spoilage/credit model and more domain assumptions. RescueSplit has intricate consent and liability allocation, and Metal is optional to its core value. Payroll Lockstep is useful but less visually distinctive. ExitPlan is approachable but harder to distinguish from an advanced subscription-spend controller. These remain viable choices if the team has stronger domain evidence or access in those areas.
