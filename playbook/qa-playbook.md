# QA Playbook with AI
## The rule
AI drafts. I validate. I decide. AI never approves anything on its own.
## Tasks (write this part as a table in your file)

| Task                | When              | Prompt to use                   | AI drafts           | I validate                            | I decide                |
|---------------------|-------------------|---------------------------------|---------------------|---------------------------------------|-------------------------|
| Test cases          | Story is "Ready"  | `test-cases.md`                 | Test case draft     | Coverage, test users, expected results | Which to automate      |
| Acceptance criteria | Refinement        | `acceptance-criteria-review.md` | Gaps and questions  | Which questions are real              | What to raise to the PO |
| Bug analysis        | Bug found         | `bug-analysis.md`               | Report draft        | Steps reproduce, rule cited           | Severity, priority      |
| Release             | Before deploy     | —                               | —                   | —                                     | Go / no-go              |

## Before accepting any AI output
- [ ] I read all of it
- [ ] Every test user and rule exists in context.md
- [ ] Nothing confidential left the approved tools

## When something escapes to production
"The AI said it was fine" is not an answer. Review which step of this
playbook failed and update the prompt or the checklist.