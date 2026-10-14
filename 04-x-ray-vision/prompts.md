# 04 · X-Ray Vision — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly. Last session the numbers showed you what happened: a
ping used to wait ninety seconds and now it waits sixty, people
missed pings they used to catch, and missing one counts the same as
turning one down — so four responders stopped hearing from us
altogether.

At the end of the session, type wrap up, and Claude Code saves the
prompts you wrote yourself below — not the starter prompt — updates
CLAUDE.md, and saves your work to GitHub. By Module 6 this file is a
prompt library built from your own questions.

---

### 1.

Has anything changed recently?  Walk me though the differences in simple terms and explain why this might matter to a responder?

### 2.

How would this account for a responder no longer getting pinged?

### 3.

A missed ping and a turned-down ping are punished identically. The code records them as different outcomes, but when it updates the score it treats them the same, and both cost 0.12. The code comment says this on purpose (“we asked and we didn’t get a yes”)

### 4.

Are there any engineering comments in the codebase worth evaluating further

### 5.

what code changes were introduced in 4.2 that may be contributing towards the issues we've been seeing with more misses and less pings being sent

### 6.

Did the change to who gets asked first apply to responders who'd already been turning jobs down or just new ones?

### 7.

The pings table on rook-database has last session's numbers. Read that alongside this code. Does it back up what I found in Lab A? And does that answer the engineering manager's question above?

### 8.

What might be the question behind the question when Marcus asks if the change applies to responders who'd already been turning jobs down or just new ones?  And what would answer that question?

### 9.

Find me the part of this code that takes points off somebody when they miss a ping or turn one down. Show it to me and explain it in plain English. Then find me every single thing in this code that puts points back on.

### 10.

If responder does not receive pings, how can they put points back on?

### 11.

If I had only asked what the codes does and not what it doesn't do, what would I have missed?
