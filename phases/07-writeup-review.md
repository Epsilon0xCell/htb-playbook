# Phase 7: Writeup and Post-Box Review

Purpose: review only. Reporting already happened continuously in the record during Phases 1 to 6 (NIST SP 800-115: reporting occurs simultaneously with the other phases), so this phase consolidates, extracts lessons, and proposes playbook changes. It is done in the same session as the root flag.

Entry criteria: root flag obtained, or the box formally parked or abandoned, in which case the review records that outcome.

Steps:

1. Assemble the writeup from the record: recon, the key insight, exact commands in order, why it worked, detection and fix, what transfers. Dead ends included. Credentials redacted. Versions pinned where they matter. No padding, no score theatre.
2. Complete the post-box review from [`templates/post-box-review.md`](../templates/post-box-review.md): outcome and times per phase; intended path versus your path; missed signals (things sitting in your own saved output that you did not act on); dead ends with time spent and the evidence that killed each; new techniques keyed service:technique; candidate lessons as trigger-to-action rules; the framework change this box justifies, named by file.
3. Feed candidate lessons into the lessons system: a candidate becomes doctrine only on a second, different box; two misfires demote it; playbooks change only via a post-box review, never mid-box.

Exit criteria: writeup pushed and review complete. A box without a review does not count as done.

Checklist:

- [ ] Writeup assembled from the record, dead ends in, credentials redacted
- [ ] Review complete, all fields answered
- [ ] Candidate lessons filed
- [ ] Calibration scored: prediction versus what happened
