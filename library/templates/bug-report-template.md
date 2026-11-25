### BA-XXX — <Short description of observed behavior>

**Step 1 — Classification (answer before anything else)**
| Question                                   | Answer                          |
|--------------------------------------------|---------------------------------|
| Is this really a bug?                      | Bug / Intended behavior / Requirement gap / Unclear |
| Evidence for the classification            | spec link, AC, PR, design, prior decision |
| Who confirms if unclear                    | PO / Dev / Design               |

> If **Intended behavior** → stop here, document the reasoning and the source.
> If **Requirement gap** → stop here, write the open question for the PO.
> If **Bug** → continue to Step 2.

**Step 2 — Bug details**
| Field          | Detail                                                  |
|----------------|---------------------------------------------------------|
| Feature        |                                                         |
| Environment    | env, build/version, browser/device                      |
| Severity       | Critical / High / Medium / Low                          |
| Priority       | P1 / P2 / P3 / P4                                       |
| Frequency      | Always / Intermittent (x of y) / Once                   |
| Preconditions  | test user, data state, session                          |

**Steps to reproduce:** 1. ... 2. ...
**Expected result:** one verifiable behavior (with source: AC / spec)
**Actual result:** what happened (URL, message, status, value)
**Evidence:** screenshot, video, logs, request/response, DataDog trace
**Suspected scope:** other features/flows that may be affected
**Regression?** Yes (last working version: ___) / No / Unknown