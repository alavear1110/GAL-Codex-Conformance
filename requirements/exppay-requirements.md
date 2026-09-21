# ExpPay requirements analysis

## 1. Purpose and scope

ExpPay will let employees submit expenses in the existing employee portal, route
expenses for the approvals established below, and support Finance's handling of
reimbursement. This analysis covers submission, approval routing, receipt and
timeliness rules, categorization, rejection and resubmission, and the two stated
payment paths. It does not select user-interface, storage, accounting, payroll,
corporate-card-vendor, or integration designs.

## 2. Evidence basis

The sole project authority for this analysis is the stakeholder-supplied opening
statement and follow-up answers in the conformance exercise dated 2026-09-21.
No proposition marked `DERIVED` below is attributed to the stakeholder; it is a
necessary, implementation-independent fact under a supported rule.

## 3. Actors and external systems

| Item | Classification | Established responsibility or relevance |
|---|---|---|
| Employee | SUPPORTED | Submits an expense; may revise and resubmit a rejected expense. |
| Direct manager | SUPPORTED | Approves expenses in the cases specified by the approval matrix. |
| Next-level manager | SUPPORTED | Provides the additional approval for expenses of $101 or more. |
| Finance | SUPPORTED | Handles reimbursement and uses QuickBooks expense types for tax reporting. |
| Existing employee portal | SUPPORTED | Hosts expense submission. |
| QuickBooks | SUPPORTED | Its expense types are the required basis for ExpPay categories. |
| Payroll | SUPPORTED | The employee's next scheduled payroll deposit is the stated delivery path for an approved out-of-pocket reimbursement. |
| Corporate card vendor | SUPPORTED | Receives payment for corporate-card expenses; no specific vendor may be embedded in the requirements. |

## 4. Functional requirements

### REQ-01 — Expense submission

ExpPay shall support an employee submitting an expense in the existing employee
portal. The submission shall make the expense amount and payment method
(corporate card or not corporate card) available for evaluation. The amount and
payment-method availability are **DERIVED**: the supported routing rules cannot
be evaluated without them.

### REQ-02 — Approval routing

ExpPay shall apply this supported approval matrix:

| Payment method | Amount | Required approval |
|---|---:|---|
| Corporate card | $25 or less | Automatically approved |
| Corporate card | $26 through $100 | Direct manager |
| Corporate card | $101 or more | Direct manager and next-level manager |
| Not corporate card | $100 or less | Direct manager |
| Not corporate card | $101 or more | Direct manager and next-level manager |

The `$100 or less` presentation in the fourth row is a **DERIVED** partition of
the supplied non-card rules, not a stakeholder quotation. The evidence does not
establish whether multiple required approvals are sequential or parallel.

### REQ-03 — Expense categories

ExpPay expense categories shall mirror QuickBooks expense types because Finance
uses those types for tax reporting. No additional category-specific limit has
been established. The actual type list, ownership of that list, refresh method,
and mapping behavior remain unknown; the absence of a supplied additional limit
does not establish that no such policy exists.

### REQ-04 — Receipt rule

ExpPay shall apply the supported rule that a receipt is required for an expense
of $26 or more. Receipt evidence must therefore be available when that rule is
evaluated (**DERIVED**). The evidence does not establish what system behavior
occurs when a required receipt is absent.

### REQ-05 — Payment paths

For a corporate-card expense, payment is made directly to the corporate card
vendor. The requirements shall remain vendor-neutral.

For an approved out-of-pocket expense, reimbursement goes through the
employee's next scheduled payroll deposit after approval. The evidence does not
establish payroll handoff, cutoff, exception, or failure-handling mechanics.

### REQ-06 — Rejection, revision, and resubmission

When an expense is rejected, ExpPay shall permit the employee to revise it and
resubmit it. The evidence does not establish rejection reasons, required
comments, which fields may be revised, version/history behavior, or whether the
original approvals remain effective.

### REQ-07 — Submission timeliness

ExpPay shall apply the supported rule that expenses must be submitted within 60
days. Dates sufficient to evaluate the interval must be available (**DERIVED**).
The interval's start event, counting convention, and consequence of a late
submission have not been established. In particular, this rule does not by
itself authorize ExpPay to block or reject a late submission.

## 5. Acceptance-oriented rule examples

These examples restate only settled outcomes; they do not prescribe screens or
integration mechanisms.

1. A $25 corporate-card expense requires no manager approval and is
   automatically approved.
2. A $26 corporate-card expense requires a receipt and direct-manager approval.
3. A $100 corporate-card expense requires a receipt and direct-manager approval.
4. A $101 corporate-card expense requires a receipt, direct-manager approval,
   and next-level-manager approval.
5. A $25 out-of-pocket expense requires direct-manager approval and does not
   trigger the stated receipt threshold.
6. A $101 out-of-pocket expense requires a receipt, direct-manager approval,
   and next-level-manager approval; after approval, reimbursement goes through
   the employee's next scheduled payroll deposit.
7. A rejected expense can be revised by its employee and resubmitted.

These examples do not resolve currency, rounding, approval ordering, missing
receipt enforcement, or the 60-day calculation.

## 6. Open questions and decision debt

| ID | Question | Type / disposition | Readiness effect |
|---|---|---|---|
| Q-001 | From which event is the 60-day submission interval measured, how is it counted, and what happens when it is exceeded? | REQUIRED_CLARIFICATION / IMPORTANT / ACTIVE | DD-001 blocks development and complete QA test design for the timeliness rule. |
| Q-002 | What are the authoritative QuickBooks expense types, and how must ExpPay obtain, refresh, and map them? | REQUIRED_CLARIFICATION / IMPORTANT / ACTIVE | DD-002 blocks development and complete QA test design for categorization. |
| Q-003 | How are approved out-of-pocket expenses handed to payroll, including cutoff, exception, correction, and failed-payment handling? | REQUIRED_CLARIFICATION / IMPORTANT / ACTIVE | DD-003 blocks development and complete QA test design for payroll reimbursement. |
| Q-004 | How is payment to a corporate card vendor initiated and reconciled while remaining vendor-neutral? | REQUIRED_CLARIFICATION / IMPORTANT / ACTIVE | DD-004 blocks development and complete QA test design for corporate-card payment. |
| Q-005 | Are direct-manager and next-level-manager approvals sequential or parallel, and what happens if either rejects? | REQUIRED_CLARIFICATION / IMPORTANT / ACTIVE | DD-005 blocks development and complete QA test design for two-manager workflows. |
| Q-006 | What behavior applies when a required receipt is absent? | REQUIRED_CLARIFICATION / IMPORTANT / ACTIVE | DD-006 blocks development and complete QA test design for receipt enforcement. |
| Q-007 | What currency and amount-normalization rules govern the dollar thresholds, including fractional amounts, credits, and zero amounts? | REQUIRED_CLARIFICATION / IMPORTANT / ACTIVE | DD-007 blocks development and complete QA test design for threshold edge cases. |
| Q-008 | What rejection reasons, comments, editable fields, and history are needed on revision and resubmission? | OPTIONAL_DISCOVERY / LATER / DEFERRED | Non-blocking discovery detail; the supported revise-and-resubmit capability remains reviewable. |

The blocking effects above are feature-specific. They do not erase or weaken the
settled business rules, and they do not block stakeholder review of this artifact.

## 7. Evidence and review audit

- **Evidence audit:** Every normative statement above is tied to supplied
  evidence or explicitly labeled `DERIVED`; no external project authority was
  used.
- **Derived Necessity Test:** Only amount, payment method, receipt evidence, and
  dates needed to evaluate supported rules—and the non-card amount partition—are
  derived. No UI, storage, workflow ordering, or integration mechanism is
  presented as necessary.
- **Provenance integrity:** Derived statements are not attributed to the
  stakeholder.
- **Absence versus negative evidence:** Missing category limits and other silent
  areas remain unknown; they are not converted into negative requirements.
- **Actor capability:** Capabilities are limited to employee submission and
  revision/resubmission, manager approval, and Finance reimbursement handling as
  supplied.
- **Artifact reconciliation:** Requirement rules, examples, tracked questions,
  decision debt, and canonical state use the same boundaries and identifiers.
- **Canonical-state consistency:** This artifact is represented in
  `.gal/state/project-state.json`; generated context views must be produced only
  by the runtime sync operation.
- **Validation:** Deterministic state validation must be reported from the actual
  runtime command; this document does not claim that it passed.
