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

- Interviews (Aunt Dot, Ambrose, Halloran, Kip) and 147 tickets agree: "gone before I could answer" (13 tickets) and "quiet, few or no pings" (32 tickets) are all filed after 12 Aug, none before. Farlight and The Undertow have 22 of the quiet tickets; Halfmoon and Corporal Ashgrove 5 each, with only a mild ping dip in the data.
- Missed pings: 25 of 1,085 (2.3%) before 4.2 to 110 of 611 (18%) after, all 16 responders worse. For the four cut responders, misses spike the week 4.2 ships and pings collapse 1-2 weeks later: a likely miss, lower rank, fewer pings spiral. No weather, geography, volume or time-of-day explanation in the data.
- Kip's The Gale is the opposite case (69 pings, 13 turned down, "exhausted"); no ticket mentions too many pings. Handlers read quiet weeks as normal, which kept the seasonal story alive; Vesper and Meteor Mite are among the cut four but have no tickets. Ignore the old note about filter tickets: 12 of 16 describe real resets and wrong-user filters, not noise.
- The database has no time-to-accept, so slow answerers can't be identified. Open: how "recent acceptance" works (Wen Li), what the 3 4.2 defect fixes were (Marcus), and whether a staging environment or per-group ping wait exists.
- Proposed fix, untested: restore the 90s wait, then lift or cap the rank penalty for the four cut responders and alert handlers when a responder goes quiet. Check with Marcus and Helen first; Ravi should track weekly miss share, pings for the four and tickets.
- The 3 4.2 defect fixes (release notes): duplicate push when a ping is re-sent, capability tag order in the responder panel, wrong time zone on the coverage report export. None touch ranking or ping wait; the duplicate-push fix is worth asking Marcus about (could it suppress or delay a first push?), no evidence yet.
- Ping wait is 60s for 2nd and later pings too (62s gap). Misses rose at every position: 1st ping 2.7% to 21.4%, 2nd 0.5% to 9.8%. The four miss 70% as first choice vs 16.5% for the other 12.
- Farlight is the clearest case: 12 pings/wk to 0 by 31 Aug (last ping 28 Aug); pinged on all 59 Uptown callouts before 4.2, 6 of 31 after (went to Falkirk, Cindermark, Bulwark). Matched responders Captain Vantage and Halfmoon did not collapse. The other three of the four fell to 1-2 pings a week, not zero.
- Tickets: Meteor Mite, Vesper, The Gale and Sgt. Bulwark have zero tickets ever, Captain Vantage one; The Undertow 21 and Farlight 19 are the most. Quiet tickets lag the ping drop by about 3-5 days (handlers wait, then check availability first).
- Rank effect is unproven (no ranking scores in the database). Miss rate vs ping change across 16 responders is -0.91 but driven by the four (-0.16 for the other 12), and a miss did not delay the next ping for the other 12, so it looks like a threshold, not a smooth penalty. Still need: Wen Li, time-to-accept, push delivery logs, pings after 6 Sep.

- 4.2 changed only values in config.py, no new logic: ping wait 90s to 60s; weights proximity 0.45 to 0.60, recent acceptance 0.40 to 0.25, capability stays 0.15. Same formula for every responder: no rule for decliners vs new vs existing, so Marcus's 14 Aug question is answered for the code (applies to all) but not for intent (ask Priya, Helen, the roadmap row "Change to who gets pinged" and the 4.2 page comments).
- Score rules (history.py): starts 0.5; +0.08 only when a responder takes a callout; -0.12 for anything not taken, missed and turned down alike (offer.py throws away the difference, deliberately); clamped 0 to 1; no time window, no decay (2019 TODO unresolved), no reset, no manual override. A responder who is not pinged cannot earn points back, and dispatch stops at the first yes, so low rank means rarely asked even though README says nobody is removed.
- Pings table (1,696 rows, 29 Jun to 6 Sep) backs this: misses 2.3% to 18.0%, turn-downs 21.1% to 18.0% (did not rise), so the four cut responders were slow to answer, not habitual decliners (pre-4.2 turn-down rate about 21% for them as for everyone). Correlation of pre-4.2 turn-down rate with ping change is only -0.27; post-4.2 miss rate is -0.91. Before window is about 6.1 weeks and after about 3.7, so compare rates, not counts.
- Open from the code: are scores saved or reset on restart or release (in-memory dictionary in history.py); can the duplicate-push fix delay a first push; could Availability Confidence change the availability record that Supply reads (contract note in availability.py, unverified); the push and availability functions are placeholders, so real delivery is not visible here. Ask Marcus for the actual 4.2 diff.
