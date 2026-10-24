# Verified Agentic Banking Hackathon brief

Research checked 24 October 2026. This report distinguishes the official HackerEarth page, its underlying public tab data, the builder guide linked by that page, and missing information. No organizer was contacted and no registration was attempted.

## Most consequential findings

- The official overview says **12 tracks**. The Tracks tab presents twelve numbered starter-kit cards. Three ideas for each numbered card means **36 ideas**. Grouping them into only six broad use cases would miss the user's requested coverage.
- The official page explicitly links `https://airwallexdev.com/` as its Builder Guide. The developer lab itself says it is not official Airwallex API documentation. Treat it as the **hackathon-linked implementation guide**, and verify endpoint details against official Airwallex docs.
- Applications close **25 October 2026 at 18:29 UTC = 19:29 Africa/Lagos**. The build phase starts **27 October at 04:30 UTC = 05:30 Lagos**, and ends **13 November at 18:29 UTC = 19:29 Lagos**. Older third-party listings saying October 23/25 are stale.
- The page's overview contains contradictory duration language: an introductory paragraph says 48 hours, while the graphic says three weeks and the dated build phase spans October 27–November 13. Plan against the explicit phase timestamps, with the duration inconsistency disclosed.
- Visa and Metal are the only separately named cash sponsor awards. The published threshold for each is use of that sponsor's tooling **and Airwallex tooling**. No public page located gives a more detailed scoring rubric or confirms whether multiple awards may be stacked.

## Exact track map

The broad label and numbered starter-kit name are independently transcribed from the official images. Capitalization and a few spaces are normalized.

| No. | Broad label on HackerEarth | Exact starter-kit title | Required behavior in brief | Setup shown |
|---|---|---|---|---|
| 01 | Treasury & Ops | Adaptive Treasury Controller | Choose funding, conversion, deferral, or escalation when cash is constrained | Fund a wallet |
| 02 | Expense & Policy | Intent-Bound Purchase Agent | Select SaaS terms and enforce the decision with virtual-card controls | Fund a wallet |
| 03 | Treasury & Ops | Payment Ops Incident Commander | Resolve an overdue supplier transfer while preventing duplicate payment | Fund a wallet |
| 04 | Revenue Protection | Dispute Response Agent | Decide chargeback disposition using evidence and economics | No extra enablement |
| 05 | Multi-Tenant Platforms | Platform Spend Controller | Issue customer cards and allocate bridge funding during late deposits | Request platform access |
| 06 | Multi-Tenant Platforms | Multi-Employer Payroll Executor | Execute payroll with each employer's funds isolated | Platform access and three accounts |
| 07 | Dynamic Lending | Portfolio Lending Agent | Collect repayments and size a new advance while maintaining a portfolio cash floor | Request platform access |
| 08 | Multi-Tenant Platforms | Marketplace Settlement Agent | Set and revise seller reserves, then settle net proceeds | Request platform access |
| 09 | Agentic Commerce | Approval-Bound Shopping Agent | Finish an actual merchant checkout, renewing approval when terms change | Allowlisted Airi CLI access |
| 10 | Agentic Commerce | Merchant-Enabled Agentic Checkout | Search through Claude, pay with a test card, return merchant order confirmation | Merchant-side access |
| 11 | Agent Payments | x402 Business Agents | Operate three agents from one account and adjust limits after supplier prices increase | Funded Metal testnet wallet |
| 12 | Inference Sourcing | Inference Sourcing Agent | Source each AI task at live prices, rerouting when budget or latency changes | Metal testnet access |

Sources: [Official track cards 1–6](https://uc.hackerearth.com/he-s3-ap-south-1/media/sprint/agentic-banking-hackathon/editor/editor_image_2733610_9216ea9.png), [official track cards 7–12](https://uc.hackerearth.com/he-s3-ap-south-1/media/sprint/agentic-banking-hackathon/editor/editor_image_2733610_1e5cbf6.png), [official track introduction](https://uc.hackerearth.com/he-s3-ap-south-1/media/sprint/agentic-banking-hackathon/editor/editor_image_2733610_8c4095b.png).

The guide organizes kits 11 and 12 under Agentic Commerce, while HackerEarth gives them the labels Agent Payments and Inference Sourcing. Preserve all twelve kit names to avoid this taxonomy ambiguity.

## Prize and sponsor facts

| Award/resource | Published value | Published condition or supplied technology |
|---|---:|---|
| Founder's Choice | $30,000 | Open category, no specific extra requirements stated |
| Judges Choice | $20,000 | Open category, no specific extra requirements stated |
| Visa Award | $15,000 | Visa and Airwallex tooling |
| Metal Award | $15,000 | Metal and Airwallex tooling |
| Claude credits | $10,000 | Free model tokens; email support |
| AWS credits | $50,000 | Compute credits; Bedrock AgentCore; Slack support |
| Base44 credits | $16,000 | App builder; developer credits; Slack support |
| Visa technology | — | Trusted Access Protocol (TAP); Visa Intelligent Commerce (the graphic calls it “Visa Intelligence Commerce”); Slack support |
| Metal technology | — | L1 chain, documentation, nodes, faucet, wallets; Slack support |
| Coinbase technology | — | CDP and stablecoin infrastructure; Slack support |
| T:0 technology | — | AI accounting, documentation, MCP server, sandbox; Slack support |

The listed cash awards total $80,000 and listed credits total $76,000. The overview separately advertises “$100K prizes & API credits.” **Do not harmonize this into an invented official total or per-team entitlement.** The brief does not explain how credits are allocated, availability to every registrant, expiration, cloud eligibility, or stackability.

Sources: [Official prizes graphic](https://uc.hackerearth.com/he-s3-ap-south-1/media/sprint/agentic-banking-hackathon/editor/editor_image_2733610_ace7f6e.png), [official product partners graphic](https://uc.hackerearth.com/he-s3-ap-south-1/media/sprint/agentic-banking-hackathon/editor/editor_image_2733610_c293391.png), [official overview graphic](https://uc.hackerearth.com/he-s3-ap-south-1/media/sprint/agentic-banking-hackathon/editor/editor_image_2733610_62fda2e.png).

## Eligibility, ownership, submission, timing

The custom FAQ says participation is free, worldwide, age 18+, with teams of one through four. Developers, designers, data scientists, and founders are welcome. Registered participants are promised sandbox and workshop access. Participants retain their project IP; submission gives permission to showcase the work. The hackathon is online; in-person Demo Day in San Francisco is optional, and remote teams have access to mentors and judging.

Required submission: a working demo, a walkthrough video **under five minutes**, and a repository link containing setup instructions. The public material does not specify a mandatory open-source license or public repository visibility, a weighted scoring formula, an exact technical judge list, whether pre-existing code is eligible, a travel reimbursement policy, or a separate sponsor submission form.

| Date | Milestone |
|---|---|
| 5 October 2026 | Applications open during SF Tech Week |
| 25 October 2026 | Applications close |
| 27 October 2026 | Accepted teams notified; official build begins |
| 13 November 2026 | Project submissions due |
| 15 November 2026 | Finalists selected |
| 19 November 2026 | Demo Day; remote participation available |

Sources: [Official FAQ graphic](https://uc.hackerearth.com/he-s3-ap-south-1/media/sprint/agentic-banking-hackathon/editor/editor_image_2733610_ceea493.png), [official dates graphic](https://uc.hackerearth.com/he-s3-ap-south-1/media/sprint/agentic-banking-hackathon/editor/editor_image_2733610_f3e517e.png), [official event page with UTC phase times](https://www.hackerearth.com/community/challenges/hackathon/agentic-banking-hackathon/).

## What the linked builder guide actually rewards in a demo

The guide asks for a recurring finance task with a consequential choice that changes when balance, time, evidence, or risk changes. Show the original plan, a meaningful new fact, the changed decision, and an executed financial action or explicit escalation. Keep financial arithmetic and hard limits in code; use the model for interpreting documents, comparing evidence, planning, and explaining exceptions. Approvals should cover the exact payment and purchase facts. These are **guide recommendations, not a published weighted judging rubric**. [Hackathon builder guide](https://airwallexdev.com/guide#build-around-a-financial-decision).

Specific build gate facts worth surfacing in idea selection:

- Kits 1–4 use ordinary sandbox access. Kits 5–8 need **both connected accounts and platform payments enabled by Airwallex**; these are not self-serve switches.
- Kit 9 requires allowlisted Airi access and actual merchant purchases. The team's browser agent performs shopping and checkout; Airi supplies payment mandates and one-time credentials. The organizer guide says participants receive an Airwallex-issued card, but does not publish the amount or access lead time. Airi's [official README](https://github.com/airwallex/airi-cli) currently lists macOS and Linux binaries, so the team's Windows environment needs a Linux runner or WSL for this path. Its mandate flow includes shopper passkey approval, and its credential command can write a restricted file instead of exposing card data in model context.
- Kit 10 needs separate merchant enablement and a merchant-specific MCP connection, **at least 100 synthetic products**, Claude configuration, hosted test-payment entry, a merchant order number, and a changed-price/unavailable-item/declined-payment demonstration. Ordinary developer MCP is not this merchant service. The linked [Merchant Onboarding API](https://airwallexdev.com/agentic-commerce/) labels its contracts as draft and not deployed: do not treat its sample onboarding/product URLs or merchant MCP URLs as currently available services. Obtain the actual enabled contract from Airwallex.
- Kits 11–12 use Metal testnet and Airwallex sandbox; Metal setup is described as self-serve. Guide-specific instructions use Metal's *USDZ token.
- Kit 11's Metal-to-Airwallex conversion is **an explicitly simulated settlement boundary**: Airwallex sandbox cannot receive stablecoins. Store the chain transaction reference and simulate a deposit; do not claim a live off-ramp.
- Kit 12 requires card preauthorization, actual-spend capture within the authorized ceiling, unused-hold release, job-specific clearing wallets, and explicit handling of testnet clearing timing. The guide says a clearing wallet pays around one request per three seconds. Its ten-minute withdrawal estimate is superseded by [Metal's current primary clearing documentation](https://docs.metalntwx.com/agents/clearing), which says normal withdrawals take **20 minutes or more**. Do not promise an immediate transfer of already-deposited float between job wallets; use a still-liquid reserve for short-demo top-ups and show pending withdrawal honestly or recorded finality from an earlier run.

Source: [Hackathon-linked builder guide](https://airwallexdev.com/guide). The companion Airwallex and sponsor reports cross-check the technical constraints against primary documentation. Actual account enablement and integration behavior still require testing during the build.

## Research retrieval and evidence trail

The event's main HTML renders skeletons for its tabs, and ordinary text browsing omits almost the entire brief. The frontend JavaScript exposes the public route `/challengesapp/api/events/{slug}/tabs/{tab}/`; unauthenticated GET returned each tab's HTML, which embeds the official graphics above. Public tab metadata and official graphics are retained as `hackathon-*.json` and `brief-*.png` so the research is reviewable. Raw HTML and website bundles remain in the local research cache and are excluded from version control.

Public tab endpoints, useful for reproducing the extraction:

- https://www.hackerearth.com/challengesapp/api/events/agentic-banking-hackathon/tabs/tracks/
- https://www.hackerearth.com/challengesapp/api/events/agentic-banking-hackathon/tabs/key-dates/
- https://www.hackerearth.com/challengesapp/api/events/agentic-banking-hackathon/tabs/prizes-credits/
- https://www.hackerearth.com/challengesapp/api/events/agentic-banking-hackathon/tabs/product-partners/
- https://www.hackerearth.com/challengesapp/api/events/agentic-banking-hackathon/tabs/questions/
- https://www.hackerearth.com/challengesapp/api/events/agentic-banking-hackathon/tabs/overview/

Search results from Internshala and HireToday showed superseded dates. They are not used as evidence for current rules. A public existing dispute-response repository appeared in search, confirming the baseline dispute agent is already an obvious direction, but it is not a rules authority and no originality guarantee follows from this limited search.
