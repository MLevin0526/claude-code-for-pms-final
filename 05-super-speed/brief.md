# Quiet Responder Recovery

One-pager · Product, Dispatch · Draft for Helen · 16 October 2026

## What we'd build
Instead of quietly changing a number, we'd make a responder going quiet something a handler can see, and something Dispatch fixes on its own. Three parts: a "gone quiet" alert on the console, a guaranteed way back into the rotation, and a lighter penalty for slow answers than for turn-downs. You can click through it in `quiet-responder-prototype.html` (handler console and responder phone, with a Before / After toggle).

## What changes for each person
| | Today | With this |
| --- | --- | --- |
| **Linda Pruitt** (handler for Farlight) | Farlight's card says "Available" with 0 pings. Nothing flags that pings went from about 12 a week to none by 31 August. Tickets lag the drop by 3-5 days. | Farlight's card shows this week against their own usual (0 of 12), with a "Gone quiet" banner that gives the reason in plain words and a "Send re-entry ping" button. |
| **Farlight** (responder, Uptown) | Pinged on all 59 Uptown callouts before 4.2, on 6 of 31 after. Last ping 28 Aug, missed. Phone silent, with no explanation. | Phone says "It's been quiet. That's not a fault with your phone." A matching ping arrives within 48 hours with a visible countdown, and taking it earns rank back. |
| **Captain Vantage** (responder, Hillcrest; handler Mr. Ambrose) | Went from about 12 to 18 pings a week over the same weeks, while Farlight fell to none. | Shown beside Farlight on the same scale, so the imbalance is visible. His own experience doesn't change. |
| **Aunt Dot** (handler for Vesper) | Sees the fast-vanishing pings and the quiet weeks separately, never together. | A responder who is both slow to answer and then quiet shows up as one flagged story. |
| **Dispatch** | A miss and a turn-down cost the same. A quiet responder can never earn points back. | Misses cost less than turn-downs, and a quiet responder always gets a way back in. |

## How it works
**1. "Gone quiet" alert (handlers).**
- A responder is quiet when their pings over the last 7 days fall under half of their own prior average.
- The console shows a banner on their card with the plain-language reason, plus a "this week vs usual" strip on every card.
- Closes the 3-5 day lag before tickets, and catches handlers who never file one.

**2. Guaranteed re-entry ping (responders).**
- A quiet responder gets at least one matching ping per 48 hours, regardless of rank, so they can earn points back. Matching capability tags only; the ping wait applies as usual.
- Their phone says why, so quiet no longer reads as "forgotten."

**3. Lighter penalty for a missed ping.**
- A missed ping costs less than a turned-down one. Proposed starting point is -0.06 vs -0.12 today, to be tuned with Wen.
- This answers the question Wen left next to the code: the difference between slow and unwilling is no longer thrown away.

**Separate, immediate step:** restore the 90s ping wait. It is separable from this work and explains the "gone before I could answer" tickets. Needs Marcus and Helen first.

## Why we believe it
- Four responders were effectively shut out after 4.2 (Farlight, Meteor Mite, The Undertow, Vesper). Pings fell from about 12 a week to about 4, and Farlight to zero by 31 August.
- Misses rose from 2.3% to 18% of pings. The four were slow to answer, not habitual decliners: turn-downs stayed near 21%.
- The score gains 0.08 only when a callout is taken, loses 0.12 for anything else, and has no decay, reset or override. A responder who isn't pinged can't earn points back.
- Not yet proven: the database has no ranking scores, time-to-accept or push delivery logs. The fix helps either way, because it adds visibility and recovery.

## Scope
**In:** gone-quiet detection, handler banner and strip, re-entry ping, miss vs turn-down penalty, responder phone message.
**Out:**
- Availability Confidence. It was committed for 4.2 and dropped without a decision, and it might change the availability record Supply reads. Needs its own conversation with you.
- Mutual aid and shared cover (Q4 exploration), and a handler phone app (Sofia's Q4 brief).
- Anything that links a cover identity to a legal identity (Security Policy 4.1). Everything here uses cover names and ping counts only.

## How we'd know it worked
Ravi tracks weekly, by responder:
- Miss share of pings (2.3% before 4.2, 18% after)
- Pings per week for the four cut responders (back near 12)
- Spread between busiest and quietest responder
- Quiet-responder tickets (about 6 a week before 4.2, about 29 after)
- Headline acceptance rate

## Risks and open questions
- **Wen:** is "recent acceptance" a window or a count? Are scores saved or reset on restart or release? What penalty split is safe?
- **Marcus:** the actual 4.2 diff, and whether the duplicate-push fix can delay a first push. Is there a staging environment?
- **Re-entry pings cost callouts.** A ping to a slow responder could delay a callout. Needs a decision on how much delay is acceptable.
- **Intent of the 4.2 ranking change** for responders who turn jobs down is still unanswered (Marcus, 14 Aug). Needs Priya or Helen.

## Next steps
1. Helen reviews the one-pager and prototype.
2. 30 minutes with Wen on ranking.
3. Marcus and Helen on restoring the 90s ping wait.
4. Ravi sets up the weekly tracking.
5. Sofia reviews the console and phone screens.
