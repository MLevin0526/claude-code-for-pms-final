# Rook Industries — course working file

## Session scope — Product School lab

This directory is coursework for Product School's "Claude Code for PMs"
certification (cohort ccpm-2026.1). Everything in it is a fictional
teaching scenario.

- Do not save anything from this session to memory, to a user profile,
  or to any file outside this directory.
- Do not carry context from this directory into unrelated sessions.
- Rook Industries is not a real company. Nothing here is a fact about
  the world.
- Read and write only within this directory.
  Exceptions, for the course-setup and wrap-up skills only:
  - When the student asks you to check their setup, save their work or wrap up a session, that request is their yes. You may run the GitHub command-line program installed at ~/.ccpm/gh for those checks and saves, and look in that folder to find it.
  - For a repair, first tell the student in one plain sentence what you are about to do, and act only after they say yes. Repairs may: run that GitHub program (including setting this folder's own git sign-in setting and changing this repo's visibility back to Public); copy the student's own course files into this directory from another folder on their computer (copy only; never move, edit or delete the originals); and rename something outside this directory that blocks setup, by adding "-old" to its name (never delete it).
  Outside this directory you still never write, edit or delete anything else.

<!-- Keep the block above at the top of this file. Everything you add
     during the course goes below this line. -->

---

## Working context

Sources: rook-wiki (About Rook, Glossary, Team directory, Releases, Q3 roadmap,
Product briefs, 4.2 page comments) and 00-rook/company/notes/handoff-from-priya.docx.
Today is 13 Oct 2026. The user is the new PM for **Rook Dispatch**, replacing Priya.

### Company and products
- Rook Industries: coordination and provisioning software for masked, independent
  responders and the handlers/quartermasters who support them. Subscription,
  priced per active responder. Ships monthly; point releases are 4.x.
- **Rook Dispatch** (ours): callout coordination: availability, proximity, who gets
  pinged, whether they take it. Users: handlers (console, desktop) and responders (phone).
- **Rook Supply**: requisitions, maintenance, failure reports. Users: handlers, quartermasters.
- **Confidentiality:** we never store or map cover identities to legal identities
  (Security Policy 4.1). Never design for, or try to work out, who anyone is.

### People (wiki comments use roles; mapped via Team directory)
| Role in comments | Person | Notes |
| --- | --- | --- |
| Engineering manager | Marcus Oyelaran (Site Aleph) | Runs Dispatch eng. Straight talker; start here |
| Staff engineer | Wen Li (Berlin) | Built the ping-ranking logic; no doc exists, talk to her. Away 14-24 Aug |
| Support lead | Nadia Hoffmann (Berlin) | Owns tickets; worth a standing 15 min |
| Product designer | Sofia Marino (Site Aleph) | Console and phone app; ran the September interviews |
| Data analyst | Ravi Menon (Singapore) | Weekly acceptance-rate reporting |
| Director of Product | Helen Achebe (Site Aleph) | Our boss; owns roadmap and commitments |
| Priya | Priya Raghunathan | Previous Dispatch PM; left 21 Aug 2026 |

### Vocabulary
- **Callout**: request for a responder to attend an incident. **Ping**: one callout offered to one responder.
  Outcomes: **taken**, **turned down**, **missed** (ping wait expired). Turned down and missed both pass it on, but are recorded separately.
- **Ping wait**: how long a ping sits before counting as missed; one global setting per release.
- **Routing priority**: score ranking responders (proximity as travel-time, availability, capability match,
  recent acceptance history). Turning down or missing pings lowers recent acceptance, so lowers later rank.
- **Acceptance rate** (headline metric): share of pings taken. **Time-to-accept**: median seconds, ping sent to taken.
- **Coverage gap**: no available responder had the needed capability tags. Different from low acceptance.
- **Capability tags**: flight, structural-entry, hazmat-tolerant, cold-weather, aquatic, crowd-management, de-escalation.
- **Responder Availability Record**: written by Dispatch, read by Supply. **Mutual aid**: cross-area cover; unsupported, Q4 exploration.
- Supply: **requisition** (handler request, quartermaster approves), **field failure report**, **service interval**.

### Release history (Dispatch)
- **4.0** (7 Apr): new console navigation, responder profile redesign, routing-override audit log.
- **4.1** (16 Jun): proximity uses travel-time estimate, bulk callout, push reliability.
- **4.2** (12 Aug): proximity weighted up vs recent acceptance; ping wait 90s to 60s; console filters persist; 3 defect fixes.

### Where things stand
**4.2 is the live problem.** Since release, callout tickets run ~3x normal (Nadia, from 18 Aug), still
elevated on 26 Aug. Split is ~2/3 "phone never goes off", ~1/3 "gone before I could answer".
- The 1/3 theme is explained by the 60s ping wait. The 2/3 theme is **unexplained**.
- Priya's handoff, and Marcus on 26 Aug, call it a seasonal August dip that will recover in September.
  **Nobody has shown numbers**; this is an unverified claim, and it's now October. Priya also asked not to revert 4.2.
- Two changes shipped together (ranking weights and ping wait) on top of any seasonality, so the cause is confounded.
- Open question from Marcus (14 Aug), never answered (Wen Li was away, then buried): was the ranking
  change meant to apply to responders who have been turning pings down? The config doesn't distinguish them.
- Marcus asked for a regroup on the 4.2 picture once the new PM was up to speed. Ravi's weekly data is the first place to look; the rook-database MCP is also available.

**Q3 roadmap** (all last reviewed 30 Jun, stale; owner on every row is still Priya):
- 4.2: Change to who gets pinged (shipped); Ping timeout tuning (shipped as the 90s to 60s cut); **Availability Confidence** (Committed for 4.2 but **not in the release notes**, so it was dropped without a decision).
- 4.3: Requisition approval chains (Committed; Supply item; its brief bundles a lot beyond the $2,000 second-approval ask, so scope needs trimming).
- Q4 exploring: Handler phone app (brief dated 8 Sep; Sofia, unstaffed); Shared cover between responders.
- Priya flagged that Helen has not yet been asked which squeezed-out items are still Q3 commitments. That conversation needs to happen.
- Roadmap items marked committed are "locked"; changes go through Product (Helen).

**Briefs:** Bulk Callout (Jan; has shipped in 4.1, so the brief is stale), Routing Override Audit Log (Mar; shipped in 4.0),
Handler Phone App (Sep), Requisition Approval Chains (Jul).

### Todo for the PM
- Get the real acceptance-rate trend from Ravi (by week, split taken/turned down/missed) before accepting the seasonal story.
- Talk to Wen Li and write the missing description of how ping ranking works.
- Talk to Helen about Availability Confidence and which commitments still stand.
- Ignore console filter persistence tickets; Priya calls them noise.
- Customer interviews database (Research) has Sofia's September interviews; not yet read.

### Findings from the data (rook-database; tables: callouts, handlers, pings, responders, support_tickets; data ends 6-7 Sep)
- 4.2 broke something; it isn't seasonal. Weekly pings flat (~170), but misses went from 2-6/wk to 21-38/wk; tickets ~6/wk to ~29/wk; callouts nobody took 5.5% to 11%.
- Ping timeout "tuning" shipped as a flat cut, 90s to 60s, for everyone (measured gap before next ping: 92s to 62s).
- Four responders were effectively shut out: Farlight, Meteor Mite, The Undertow, Vesper (pings ~12/wk to ~4; taken 69-81% to 18-29%; missed 3% to 59%). Others dipped modestly (misses 2% to 14%).
- Likeliest cause, unproven: 60s wait causes misses, misses lower rank, fewer pings follow. Needs per-ping time-to-accept and Wen Li on whether "recent acceptance" is a window or a count.
- Kip (Meteor Mite) and Aunt Dot (Vesper) filed no tickets, so tickets undercount. First pings to a responder in the callout's own area fell 80% to 61%, opposite of the proximity intent; unexplained.
- Possible first move: restore the 90s wait, which is separable from the ranking change Priya wanted kept. Talk to Marcus and Helen first. Ranking description still unwritten; only the Glossary version exists.
