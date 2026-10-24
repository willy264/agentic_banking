# Original product directions for tracks 09–12

These are proposed product designs, not claims that the sponsors already ship them. Three ideas are supplied for each of the four numbered tracks. Every proposal preserves the relevant kit's end-to-end financial behavior and adds a distinct decision problem.

The platform facts are grounded in the [official track graphics](https://uc.hackerearth.com/he-s3-ap-south-1/media/sprint/agentic-banking-hackathon/editor/editor_image_2733610_1e5cbf6.png), the [hackathon-linked guide](https://airwallexdev.com/guide), [Airwallex's Airi repository](https://github.com/airwallex/airi-cli), and [Metal's primary developer documentation](https://docs.metalntwx.com/). Detailed technical evidence is in `airwallex-technology.md` and `sponsor-technology.md`.

## 09 — Approval-Bound Shopping Agent

The non-negotiable track spine: agent drives a real merchant checkout; shopper approves exact purchase facts; Airi supplies approved payment credentials; changed terms require renewed approval; payment result is reported back. Airi does not operate the browser. Its current supported binaries are macOS/Linux, so a Windows team should plan a Linux runner or WSL. [Airi official README](https://github.com/airwallex/airi-cli).

### 09A. RestoreCart — buy the smallest intervention that restores operations

**User and pain.** A small ecommerce warehouse cannot ship because its label-printing setup has failed. Buying the cheapest replacement can be more expensive than paying extra to get a compatible part today.

**Distinct mechanism.** Convert an operational incident into a compatibility graph and a cost-of-delay budget. The agent chooses between a replacement cable, consumable, adapter, or complete device using documented compatibility and delivery evidence. It purchases the smallest viable repair bundle, with uncertain compatibility escalated to the operator. This sells restored capacity rather than product recommendations.

**Technology composition.** Claude interprets the manual and incident note; code evaluates candidate compatibility predicates and supplied downtime costs; an AWS-hosted browser executes the selected checkout. Airi's supported mandate fields bind merchant, line items, currency, and total; the application's separate approval snapshot also binds fulfillment and the other material terms Airi does not represent. An optional later Airwallex sandbox payout can settle a repair contractor, but is outside the smallest MVP.

**Changing-evidence demo.** A $12 part initially wins. Its delivery moves from next-day to next-week after approval. The agent invalidates that approval, shows why the $19 compatible substitute now has lower total operational cost, gets new approval, and completes one actual inexpensive purchase. A second scripted case refuses an electrically incompatible substitute.

**MVP.** One benign equipment category, two candidate real merchants, three repair strategies, one successful checkout, one terms-change replay. Measure time-to-valid-repair-plan, approval precision, and no duplicate order.

**Blockers and scope.** Airi allowlisting and an actual merchant purchase are required; real merchant verification may need user action. Do not claim a model can certify physical compatibility beyond available specifications. Visa integration is optional and separately gated; Airi alone does not prove Visa Award eligibility.

### 09B. KitLock — coordinate purchases whose usefulness depends on one another

**User and pain.** A pop-up business needs a compatible point-of-sale stand, charging adapter, receipt rolls, and a cable before opening. Four individually sensible purchases can create one unusable kit if the indispensable component sells out.

**Distinct mechanism.** Maintain a graph of dependencies and a maximum committed-loss budget. The agent compares purchase sequences: secure the scarce anchor item first, then order its dependents; prefer returnable variants when availability is uncertain. It can substitute an entire configuration when a key part disappears. This is an application-level compensation workflow; it is not an atomic transaction across merchants.

**Technology composition.** Claude reads stock, delivery, and return terms. Code computes dependencies, committed spend, and permitted fallback configurations. Browser automation and Airi create separately approved purchases. A small ledger distinguishes cart estimates, approved purchases, confirmed orders, and refunds actually received.

**Changing-evidence demo.** The first item is confirmed; a second supplier doubles shipping and the remaining bundle no longer fits the budget. Instead of buying an isolated accessory, the agent proposes an alternative kit, shows the first order's recoverability, obtains fresh approvals, and stops if maximum exposure would be exceeded.

**MVP.** Three items across two merchants, one real inexpensive checkout, a replayed second checkout for the dependency exception. Label the replay clearly; demonstrate actual completed payment as the track's live path. Measure useful-kit completion and committed cash at risk.

**Blockers and scope.** Merchant cancellation and returns are conditional; never assume a refund is instant or guaranteed. Each purchase still needs its own exact approval. Scope the demonstration to a short dependency graph rather than a universal shopping agent.

### 09C. TermsLens — a purchase agent that detects consent drift at checkout

**User and pain.** Buyers approve a one-time purchase, but the final checkout introduces a subscription, switches the merchant of record, splits delivery, changes warranty coverage, or substitutes a product while keeping the same headline price.

**Distinct mechanism.** An approval is a structured contract snapshot. The agent compares the live checkout against that snapshot semantically and structurally, not merely by total price. It computes an explainable change set and invalidates approval whenever a material field changes. The product is a checkout assurance layer with its own working shopping agent, potentially sold as an SDK after the hackathon.

**Technology composition.** Claude extracts terms with cited page spans; a typed schema and deterministic materiality policy decide whether execution is allowed; the browser resumes preserved checkout state; Airi obtains credentials only for the latest approved version. Card values remain in a secure execution helper outside the model transcript.

**Changing-evidence demo.** A $20 purchase remains $20 but gains auto-renewal. The agent blocks the stale approval, highlights the added commitment, returns to a one-time alternative, requests approval, and completes the purchase. A timeout afterward causes an order lookup instead of a second charge.

**MVP.** Six material fields, three replayed mutation cases, one real merchant checkout, an approval/version audit view. Measure detection of changed obligations and false-positive pauses against a small hand-labelled scenario set.

**Blockers and scope.** Use deterministic merchant-page recordings for injected changes; do not pretend arbitrary live sites are under team control. TAP can complement agent identity only where the merchant supports it; it does not detect consent drift itself.

## 10 — Merchant-Enabled Agentic Checkout

All three require a merchant-specific MCP endpoint, at least 100 synthetic products, shopping through locally configured Claude, a hosted test-payment component, an actual merchant order reference, and an exception path. Merchant access is a hard gate. The linked [Merchant Onboarding API](https://airwallexdev.com/agentic-commerce/) explicitly labels its contracts **draft and not deployed**; obtain the actual enabled contract rather than coding blindly to the illustrative URLs.

### 10A. LaunchCart — sell a working capability instead of a list of SKUs

**User and pain.** A community workshop operator wants to run a 24-person beginner electronics class with six reusable tool stations and a strict total budget. A catalog search produces disconnected components; the operator has to discover missing dependencies after buying.

**Distinct mechanism.** The merchant publishes products plus machine-readable bundle constraints: pack quantity, reuse count, connector type, required accessories, and capability contribution. Claude translates the buyer's intended activity into a bill of materials. Code verifies that the selected basket can actually serve all participants. When stock changes, the agent revises the plan, not just the unavailable SKU.

**Technology composition.** Airwallex merchant MCP supplies catalog search and checkout; Claude interprets the intended outcome; a merchant-side constraint service validates the bill of materials; hosted Airwallex payment completes the order. Visa TAP verification on the merchant-controlled service is a plausible sponsor integration, subject to supported routing and credentials. Base44 can supply inventory and exception review UI.

**Changing-evidence demo.** The approved 24-person basket loses the six-pack of reusable tools. The agent switches to an alternative station plan while preserving participant capacity, identifies the new price and shipping terms, requests approval, and returns a merchant order number after test payment.

**MVP.** 100 synthetic products, one activity template, a handful of compatibility predicates, one stock mutation, one successful checkout. Measure omitted dependencies and whether capacity constraints remain satisfied after replanning.

**Why it is agentic.** User goals and product descriptions are unstructured; the candidate plan changes with stock and fulfillment evidence. Arithmetic and feasibility remain code.

### 10B. RightsCart — buy data and digital assets with the rights the project needs

**User and pain.** A design or research agency finds an attractive dataset or media asset, purchases it, then discovers the selected license excludes commercial redistribution, a required territory, or use in the intended deliverable.

**Distinct mechanism.** Treat the license variant as part of the product's capabilities. The agent maps a buyer's stated intended use to a normalized set of required rights, searches only compatible SKU/license combinations, and explains the evidence for the choice. The merchant makes clear product claims in structured metadata; ambiguous clauses lead to review rather than a legal conclusion.

**Technology composition.** Merchant MCP distributes a synthetic 100-item catalog including license variants; Claude reads supplied license summaries and buyer needs; a deterministic constraint checker rejects conflicting declared rights; Airwallex hosted checkout charges the exact approved variant; a signed application receipt records the purchased SKU and license version. Visa TAP can verify incoming agent identity on the merchant's gateway if the actual integration permits it.

**Changing-evidence demo.** A dataset remains available at the same price, but its license version changes from reusable client deliverables to internal use only. The agent detects that the approved use is no longer covered, finds a different package, obtains approval, and completes test checkout.

**MVP.** Four normalized rights dimensions, 100 synthetic products, three buyer projects, versioned license evidence, one successful purchase. Measure rights mismatches caught before charging.

**Blockers and scope.** Present this as enforcement of merchant-declared conditions, not legal advice. A payment signature proves a purchase, not that the merchant truly owns those rights.

### 10C. SecondLife Cart — make unique refurbished inventory safe for agent shopping

**User and pain.** A refurbished-device merchant's inventory is unit-specific: two identical model names can have different battery health, missing accessories, cosmetic defects, warranty terms, or storage. Conventional catalog agents erase those differences and create returns.

**Distinct mechanism.** Represent each physical unit as a versioned sellable object. Claude turns condition reports into comparable attributes; code enforces the buyer's thresholds and captures the exact unit identifier in approval. The agent can substitute only after explaining the changed condition and obtaining approval. This connects inventory truth, purchase intent, and after-sale evidence.

**Technology composition.** Merchant MCP searches 100 synthetic unit records; Claude reads inspection notes and images; a merchant database supplies versioned availability and condition facts; Airwallex hosted payment returns a merchant order bound to that unit. Optional TAP identifies the buying agent. An application evidence receipt can later help disputes without claiming it prevents chargebacks.

**Changing-evidence demo.** The selected laptop sells while checkout is open. The replacement has the same model and price but worse battery health. The agent declines an automatic swap, compares a cheaper unit plus battery against a higher-grade unit, gets fresh approval, and checks out.

**MVP.** One refurbished-product category, 100 synthetic units, one condition schema, an inventory-version check, one stale-stock exception. Measure stale-unit orders avoided and return-triggering mismatches detected.

**Blockers and scope.** The platform must reveal actual stock and order-state capabilities. Implement inventory holds in the merchant application if supported; do not describe Airwallex payment authorization as reserving inventory.

## 11 — x402 Business Agents

Preserve the three-role structure: sourcing buys upstream services, support handles justified refunds, treasury reallocates mandates and pays an ordinary business obligation through Airwallex. Metal mandates enforce delegated spending; signed orders cover the offer's resource, price, payee, and network, **not arbitrary query/body parameters or output quality**. Each distinct product/terms version must have its own immutable resource route, with an application record mapping it to a stored terms hash. The application's delivery record separately supplies evidence of what was delivered. These are different proofs. [Metal mandates](https://docs.metalntwx.com/agents/mandates), [signed orders](https://docs.metalntwx.com/agents/require-signed-order).

Each mandate enforces its own agent's budget; the overall business ceiling across mandates is an application invariant. Compute proposed replacements against historical spend, outstanding obligations, and the shared ceiling in deterministic code, and serialize approval/execution so concurrent proposals cannot overallocate the same reserve.

For all three proposals, a refund is a **new, mandate-constrained direct payout** to the verified payer from the original transaction; it does not reverse the x402 transaction. Keep a durable refund ID, reuse it on retries, and enforce cumulative refunds no greater than the original paid amount. Metal's CLI also requires retries to preserve the same credential and local state directory, so an application-level payout ledger must survive process restarts and mandate changes. A support mandate that runs out of budget creates an outstanding obligation and an escalation, not proof that no refund is owed. [Metal direct payouts](https://docs.metalntwx.com/agents/payouts).

### 11A. MarginGraph — an agent business that degrades service terms before losing money

**User and pain.** A small shipping-intelligence API combines several paid inputs into a quote sold to customer agents. An upstream supplier price increase can turn a high-volume product into a loss-making service before a human notices.

**Distinct mechanism.** Maintain a dependency graph from paid inputs to customer promises: freshness, coverage, and confidence. The agent calculates which promises can still be honored at the current price. It can buy a cheaper permitted source, offer a visibly lower-freshness product, raise the customer price, or refuse work. It never silently sells yesterday's data as live data.

**Technology composition.** Metal x402 collects customer payments and pays suppliers under separate mandates; signed offers bind advertised product terms at the application level through versioned resource identifiers and stored evidence; Claude interprets source descriptions and exceptions; code enforces contribution margin and global float. Airwallex sandbox settles a EUR data-license bill after a clearly marked simulated off-ramp credit.

**Changing-evidence demo.** One supplier doubles its charge beyond the sourcing mandate's cap. The call fails without spending. Treasury proposes a new allocation; the owner approves it. The customer accepts a different freshness/price tier, or receives a clear refusal. A stale-result complaint produces an evidence-backed refund.

**MVP.** Three internal roles, two synthetic upstream services, two customer products, one price shock, one refund, one sandbox FX/payout. Measure gross margin, promises violated, and funds spent outside mandates.

**Blockers and scope.** No native Metal–Coinbase compatibility or real Airwallex stablecoin off-ramp is assumed. Product freshness is application semantics, not something a chain signature proves.

### 11B. CacheDividend — share permitted research costs and return the savings

**User and pain.** Several customer agents independently buy reports that require the same expensive, cacheable source. They pay for duplicate upstream work, while the service provider cannot transparently explain how shared-source savings are allocated.

**Distinct mechanism.** Sell a fixed-price report with a disclosed rebate formula when eligible demand overlaps. A sourcing agent buys and caches a licensed source once; a support agent computes auditable rebates from the actual shared cost; treasury manages the working float and supplier budget. Refunds are a normal product feature, not merely dispute handling.

**Technology composition.** Each report and rebate-terms version has an immutable resource route whose application record stores the terms hash; Metal's signed order binds the offer for that route, not arbitrary request parameters. Separate mandates constrain sourcing and refund payouts; an application cost graph links source hashes, delivery records, customers, and rebate calculations. Claude decides when a new query is semantically equivalent enough to reuse an allowed source; code checks freshness, licensing flags, and the rebate arithmetic. Airwallex pays the source provider's ordinary subscription invoice.

**Changing-evidence demo.** Three reports initially require separate buys. The agent discovers two share an eligible source, buys once, and sends small rebates. Then the supplier raises its next-query price above the sourcing mandate's cap. The failed purchase spends nothing; treasury proposes owner-approved replacement budgets that preserve prior spend and the shared overall ceiling. The service recalculates new-customer pricing and future rebates without rewriting completed orders. A separate freshness or cache-permission change stops ineligible reuse.

**MVP.** Three customers, two licensed synthetic sources, one shared-cost graph, one supplier-price increase, one mandate replacement, one freshness/permission change, and two refunds. Measure duplicate source buys avoided and exact rebate reconciliation.

**Blockers and scope.** Use sources explicitly permitting caching and redistribution in the synthetic demo. Do not infer those rights from successful API access. The service carries the upfront working-capital risk; customer payment does not create a magically pooled or trustless fund.

### 11C. DeliverProof — sell agent outputs with a funded correction policy

**User and pain.** Businesses buying invoice-extraction or supplier-enrichment results from AI agents need a way to distinguish an unauthorized purchase complaint from a legitimate defective-output complaint, and to receive a correction or refund.

**Distinct mechanism.** Each paid job has declared acceptance criteria and a delivery manifest. Payment authorization, purchased terms, actual output, and subsequent quality evidence remain separate records. The support agent decides whether to rerun, correct, refund, or escalate; treasury sizes the refund budget from observed defect rates and throttles new sales when obligations exceed available coverage.

**Technology composition.** Metal mandates constrain the sourcing, support, and treasury agents; each purchased service and acceptance-manifest version has an immutable resource route mapped to a stored manifest hash, so the signed offer identifies that exact application-defined contract. Arbitrary query/body fields remain outside the Metal signature. Separate application hashes and signed delivery manifests bind input/output versions; deterministic validators test field coverage and arithmetic; Claude judges ambiguous evidence. Airwallex settles a fixed monthly OCR license after the simulated chain-to-bank boundary.

**Changing-evidence demo.** An upstream OCR provider raises its price above the sourcing mandate's per-purchase cap, and the next call is refused without spending. Treasury proposes owner-approved replacement mandates within the overall business budget, preserving historical spend. A customer then denies authorizing a batch; signed purchase evidence resolves that part. Two outputs nevertheless fail acceptance criteria. The agent refunds those, corrects another, and reduces new sales when the support budget becomes too low. A further approved budget change restores capacity only if the shared ceiling permits it.

**MVP.** One synthetic invoice service, three acceptance criteria, one supplier-price increase, one mandate replacement, four disputed deliveries, bounded refunds, and one treasury payment. Measure correct complaint classification and unpaid refund liability.

**Blockers and scope.** A delivery hash does not prove correctness; mandate limits do not eliminate contractual refund obligations. If the refund budget runs out, record the debt and escalate instead of claiming the obligation disappeared. This is a commercial correction policy, not insurance.

## 12 — Inference Sourcing Agent

All three preserve card-authorized job budgets, scarce operator float, multiple paid providers, rerouting after cost/latency changes, final actual-spend capture within authorization, and unused-hold release. Metal clearing's current primary documentation describes roughly one payment per three seconds per wallet and normal withdrawals taking **20 minutes or more**; the linked hackathon guide's ten-minute figure is older. Use a prerecorded earlier withdrawal for finality evidence or show its pending state honestly. [Metal clearing](https://docs.metalntwx.com/agents/clearing).

The clearing client requires Node **22.13+** (or 23.4+ on Node 23) and uses `node:sqlite`. Persist each wallet's SQLite state and open it from **only one worker/process at a time**; parallel jobs use separate wallet files. Run this service on a suitable persistent Node deployment. Base44 may supply the interface, but its Deno functions are not assumed to run the Metal clearing client. Keep the paid-step ledger durable so an ambiguous payment is resolved at its original provider before rerouting. [Metal clearing runtime and wallet persistence](https://docs.metalntwx.com/agents/clearing).

### 12A. DecisionBudget — spend on the evidence most likely to change the decision

**User and pain.** Procurement teams buy a supplier comparison report. A conventional research agent spends evenly across sections even when one unresolved fact determines whether a supplier is viable.

**Distinct mechanism.** Maintain an explicit decision table and an uncertainty ledger. Before buying another model call or data lookup, estimate whether the answer could change the selected supplier under the buyer's supplied criteria. Allocate scarce float to high-impact unresolved claims, not simply to the longest report or the fanciest model. Stop paying when additional evidence cannot change the decision under the stated bounds.

**Technology composition.** Claude proposes useful next evidence; deterministic code computes budget and sensitivity thresholds; paid provider routes use Metal clearing wallets per job; Airwallex preauthorizes each report's budget and captures measured spend. AWS AgentCore can host orchestration, but Metal needs its own verified payment adapter rather than an assumed Coinbase-native connector.

**Changing-evidence demo.** Three report jobs compete for limited float. A supplier's certification evidence becomes ambiguous while a cheap provider slows. The agent allocates only its still-unallocated liquid reserve to the decisive check, downgrades cosmetic narrative generation elsewhere, and asks one customer to authorize more only if the key uncertainty cannot fit its hold. It does not withdraw or redistribute funds already committed to another job's clearing wallet during the short demo; those remain subject to Metal's finality delay. End by capturing each job's actual paid spend within its authorization, releasing unused holds or cancelling unspent jobs, and showing the queued float withdrawal plus separately recorded completion after finality.

**MVP.** Three jobs, two supplier comparisons per job, five evidence dimensions, three priced providers, one context expansion, one authorization increase. Measure decision-changing evidence per dollar and unsupported decisive claims.

**Blockers and scope.** Estimated value of information is an application heuristic, not guaranteed optimality. The demo should use known synthetic ground truth to make decisions inspectable.

### 12B. Counterexample Foundry — buy adversarial tests until a software claim survives

**User and pain.** A small software team wants confidence that a proposed patch actually fixes its bug without paying for premium reasoning on every test and every line of a repository.

**Distinct mechanism.** Break a release claim into falsifiable properties. Cheap agents propose counterexamples; sandbox execution rejects irrelevant ones; a more expensive provider investigates only reproducible failures or unresolved high-severity cases. The deliverable is an executable evidence bundle and a remaining-uncertainty ledger, not a prose code-review score.

**Technology composition.** Metal clearing purchases bounded generation/analysis steps; code-execution tools validate each claimed failure; Claude identifies assumptions and promising counterexamples; Airwallex holds a customer-approved verification budget and captures actual paid cost. AWS isolation is useful because customer code must execute in a separate job environment.

**Changing-evidence demo.** Three customer patches run concurrently. One suddenly requires a fourfold larger context, and the cheapest analysis service slows. The agent stops paying for already disproved hypotheses, reserves premium calls for a reproducible boundary bug, finishes a simpler job with the cheap route, and asks before expanding the remaining job's hold. End by capturing actual paid spend once per job within its authorization, releasing unused holds or cancelling unspent jobs, and showing a pending float withdrawal with its later finalized completion in a separate recording.

**MVP.** Three small benign code fixtures, two generator providers plus one verifier provider, deterministic test execution, one cost shock, and recorded card capture. Measure reproducible failures found per dollar, provider spend, and claims lacking execution evidence.

**Blockers and scope.** Limit the task to functional correctness in sandboxed test repositories. This does not prove general security or absence of bugs. A paid call that failed still counts in the actual-spend ledger if Metal issued its receipt.

### 12C. DeadlineWorks — buy the minimum complete deliverable before buying polish

**User and pain.** A small agency has several client proposal packages due together. Some sections are mandatory for acceptance; others are cosmetic. Unplanned model costs and one slow provider can leave every proposal half-finished.

**Distinct mechanism.** Turn each customer's acceptance criteria into a dependency graph with a minimum valid completion set. The agent first funds the steps needed to complete at least one valid deliverable per job, then spends remaining budget on improvements. Across jobs, it considers deadlines, required dependencies, current confidence, and available float. It can negotiate a reduced deliverable or new authorization before doing optional work.

**Technology composition.** Claude extracts requirements from a supplied brief and critiques draft adequacy; code validates required fields and attachments; Metal clearing pays paragraph generation, retrieval, and layout checks; Airwallex preauthorizes jobs and charges only measured spend. Base44 can render a customer view showing completed requirements, optional improvements, and the exact budget increase request.

**Changing-evidence demo.** One customer's input suddenly expands; another provider develops latency. The agent reroutes a mandatory section, pauses optional stylistic rewriting, finishes two complete proposals, and asks the third customer to choose a smaller scope or a larger hold. It captures actual paid spend once per job within the authorized amount, releases the unused holds or cancels unspent jobs, then shows pending float withdrawal and separately recorded completion after finality. No job is billed above its authorization.

**MVP.** Three jobs with six required blocks each, three providers, one deadline/cost shock, a dependency visualizer, and full hold/capture/cancel lifecycle. Measure completed acceptance criteria by deadline per dollar and number of incomplete paid deliverables.

**Blockers and scope.** Use synthetic business proposal briefs; avoid claims of legal tender compliance. A provider payment must be reconciled before rerouting after an ambiguous response, and clearing float cannot be instantly withdrawn to rescue another job.

## Best candidates and sponsor strategy

| Candidate | Why it stands out | Strongest sponsor composition | Principal risk |
|---|---|---|---|
| TermsLens (09C) | Consent changes even when price does not; vivid failure demo | Airwallex Airi + Claude + AWS browser/runtime | Real checkout and Airi access |
| LaunchCart (10A) | Converts intended capability into a verifiably complete basket | Airwallex merchant MCP + Claude; Visa TAP if real verification enabled | Merchant API enablement and actual schema |
| RightsCart (10B) | Products differentiated by usable rights, not price | Airwallex merchant MCP + Claude + optional Visa identity | Must keep rights interpretation bounded |
| CacheDividend (11B) | A different agent-commerce business model: shared-cost rebates | Metal mandates/signed orders + Airwallex treasury + Claude | Source licensing and exact rebate ledger |
| DeliverProof (11C) | Separates proof of purchase from proof of service quality | Metal mandates + application delivery evidence + Airwallex | Refund obligations can exceed wallet budget |
| DecisionBudget (12A) | Routes spend according to decision value rather than generic model quality | Airwallex card holds + Metal clearing + Claude + AWS orchestration | Evaluation of value-of-information heuristic |
| Counterexample Foundry (12B) | Bought reasoning must produce executable evidence | Airwallex + Metal clearing + isolated AWS execution | Repository scope and runtime isolation |

For a **Metal Award** attempt, kits 11–12 make Metal essential to the core economic loop. For a **Visa Award** attempt, merchant-controlled track 10 is structurally stronger than asserting that an arbitrary real merchant in track 9 supports TAP. Add a real verified Visa integration or documented organizer-provided VIC flow; a card logo or a home-made signature imitation should not be represented as satisfying the prize.

Coinbase can power a separate customer or provider lane on supported CDP networks if there is a genuine need, but adding it to a Metal build must not imply that CDP supports Metal. T:0 can be useful for bank/chain accounting if its actual sandbox/tool contract is supplied. Sponsor count is less persuasive than one indispensable sponsor mechanism with a demonstrable failure mode.
