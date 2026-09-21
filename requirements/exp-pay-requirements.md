# ExpPay Requirements Draft

**Status:** Draft for stakeholder review  
**GAL mode:** STANDARD  
**Evidence baseline:** `.gal/state/project-state.json`  

## 1. Purpose

ExpPay will enable employees to submit expenses through the existing employee
portal, route expenses through the established approval policy, and support
Finance's reimbursement and tax-reporting processes.

## 2. Evidence notation

- **SUPPORTED** — explicitly established by the project sponsor during intake.
- **DERIVED** — logically necessary from supported facts; no derived
  requirements are asserted in this draft.
- **PROPOSED** — a recommendation awaiting approval; no proposed requirements
  are asserted in this draft.
- **UNKNOWN** — unresolved and intentionally not specified.

## 3. Scope

### 3.1 In scope

- Employee expense submission in the existing employee portal. **[SUPPORTED]**
- Expense categorization using the company's existing QuickBooks expense
  types. **[SUPPORTED]**
- Approval routing based on payment type and amount. **[SUPPORTED]**
- Receipt attachment when the receipt threshold applies. **[SUPPORTED]**
- Revision and resubmission of rejected expenses. **[SUPPORTED]**
- Corporate-card settlement and employee out-of-pocket reimbursement outcomes.
  **[SUPPORTED]**
- Enforcement of the 60-day submission rule. **[SUPPORTED]**

### 3.2 Out of scope

No item has been explicitly declared out of scope. **[UNKNOWN]**

## 4. Actors and external systems

| Name | Established involvement | Evidence |
|---|---|---|
| Employee | Submits expenses and may revise and resubmit a rejected expense. | SUPPORTED |
| Manager | Participates in approval according to the applicable threshold. | SUPPORTED |
| Finance | Handles reimbursement and needs QuickBooks expense types for tax reporting. | SUPPORTED |
| Payroll | Must work with Finance to determine the payroll-transfer mechanism. No ExpPay capability or payroll action is specified yet. | SUPPORTED / UNKNOWN |
| Existing employee portal | Hosts employee expense submission. | SUPPORTED |
| Existing QuickBooks configuration | Is the authoritative source of expense types. | SUPPORTED |
| Employee payroll deposit process | Delivers approved out-of-pocket reimbursement in the employee's next scheduled payroll deposit. The transfer mechanism is unresolved. | SUPPORTED / UNKNOWN |

## 5. Functional requirements

### 5.1 Expense submission and data

| ID | Requirement | Evidence |
|---|---|---|
| EXP-SUB-001 | ExpPay shall allow an employee to submit an expense in the existing employee portal. | SUPPORTED |
| EXP-SUB-002 | Each submitted expense shall include the expense date, amount, payment type, and expense category. | SUPPORTED |
| EXP-SUB-003 | For an expense with an amount of $26 or more, the employee shall attach a receipt. | SUPPORTED |
| EXP-SUB-004 | The expense category shall be an expense type from the company's existing QuickBooks configuration. | SUPPORTED |
| EXP-SUB-005 | An expense shall be submitted within 60 days of its expense date. | SUPPORTED |
| EXP-SUB-006 | ExpPay shall allow a rejected expense to be revised and resubmitted. | SUPPORTED |

No requirement for an expense description is included because that decision is
unresolved.

### 5.2 Approval routing

Approval thresholds are continuous and use the expense amount without
whole-dollar rounding.

| ID | Payment type and amount | Required approval | Evidence |
|---|---|---|---|
| EXP-APR-001 | Corporate card, amount at or below $25 | Automatically approved | SUPPORTED |
| EXP-APR-002 | Corporate card, amount over $25 and below $101 | Employee's direct manager | SUPPORTED |
| EXP-APR-003 | Corporate card, amount of $101 or more | Employee's direct manager and next-level manager | SUPPORTED |
| EXP-APR-004 | Employee-paid out of pocket, amount below $101 | Employee's direct manager | SUPPORTED |
| EXP-APR-005 | Employee-paid out of pocket, amount of $101 or more | Employee's direct manager and next-level manager | SUPPORTED |

No additional category-specific approval or spending limits have been defined.
**[SUPPORTED]**

Where two managers are required, the order of their approvals has not been
established. **[UNKNOWN]**

### 5.3 Payment and reimbursement outcomes

| ID | Requirement | Evidence |
|---|---|---|
| EXP-PAY-001 | A corporate-card expense shall be paid directly to the card vendor. | SUPPORTED |
| EXP-PAY-002 | An approved employee-paid out-of-pocket expense shall be included in the employee's next scheduled payroll deposit after approval. | SUPPORTED |

These are required business outcomes. This draft does not assign ExpPay a
payment-execution capability or prescribe how approved out-of-pocket expenses
are transferred into payroll.

## 6. Business rules

| ID | Rule | Evidence |
|---|---|---|
| EXP-BR-001 | The receipt rule is based on expense amount: a receipt must be attached at $26 or more. | SUPPORTED |
| EXP-BR-002 | The 60-day submission period is measured from the expense date. | SUPPORTED |
| EXP-BR-003 | The company's existing QuickBooks configuration is authoritative for expense types. | SUPPORTED |
| EXP-BR-004 | The approval matrix in section 5.2 governs routing; there are no additional category-specific limits currently defined. | SUPPORTED |
| EXP-BR-005 | A rejected expense may be revised and resubmitted. | SUPPORTED |

The treatment of a submission made exactly at the end of the 60th day, including
time zone and end-of-day handling, has not been established. **[UNKNOWN]**

## 7. Unresolved requirements and decision debt

The following items remain deliberately unresolved and are not implementation
requirements:

| ID | Unresolved item | Priority / disposition | Owner or needed input |
|---|---|---|---|
| Q-002 / DD-001 | The process or system that transfers an approved out-of-pocket expense into payroll, and ExpPay's role in that transfer. | Non-blocking; deferred | Finance and Payroll |
| Q-008 / DD-003 | Who may reject an expense and whether a rejection reason is required. | Non-blocking; deferred | Stakeholder decision |
| Q-009 / DD-004 | Which workflow events produce notifications and who receives them. | Non-blocking; deferred | Stakeholder decision |
| Q-010 / DD-002 | Whether an employee must provide an expense description. | Non-blocking; deferred | Stakeholder decision |
| Q-011 / DD-005 | The behavior when an expense is submitted outside the 60-day period. | Non-blocking; deferred | Stakeholder decision |
| Q-012 / DD-006 | Whether two-manager approval is sequential and, if so, its ordering and behavior after either decision. | Non-blocking; deferred | Stakeholder decision |
| Q-013 / DD-007 | How ExpPay obtains or refreshes expense types from the existing QuickBooks configuration. | Non-blocking; deferred | Finance and technical stakeholders |

## 8. Acceptance criteria

The following criteria cover only established behavior.

1. An employee can submit an expense through the existing employee portal with
   an expense date, amount, payment type, and expense category.
2. An expense of $26 or more cannot satisfy the established receipt rule unless
   a receipt is attached.
3. The category selected for an expense corresponds to an expense type in the
   company's existing QuickBooks configuration.
4. Approval routing produces the approval result specified by each row of the
   matrix in section 5.2.
5. A rejected expense can be revised and resubmitted.
6. The system applies the submission rule using the expense date as the start
   of the 60-day period.
7. A corporate-card expense follows the direct-to-card-vendor payment outcome.
8. An approved employee-paid out-of-pocket expense follows the next-scheduled-
   payroll-deposit reimbursement outcome.

Acceptance criteria for rejection permissions, rejection reasons,
notifications, descriptions, QuickBooks synchronization, payroll transfer, and
the detailed 60-day cutoff cannot be completed until the corresponding open
items are resolved.

## 9. Review status

- Evidence audit: completed for this draft; requirements labeled SUPPORTED are
  traceable to confirmed business rules.
- Derived Necessity Test: completed; this draft asserts no DERIVED requirements.
- Provenance integrity: completed against canonical GAL state.
- Absence-vs-negative-evidence audit: completed; missing decisions are recorded
  as UNKNOWN rather than negative requirements.
- Actor capability audit: completed; no unresolved rejection, payroll-transfer,
  notification, or synchronization capability is assigned to an actor.
- Artifact reconciliation: completed against canonical GAL state.
- Canonical-state consistency: pending deterministic state validation.
- Validator execution: **NOT EXECUTED** because PowerShell (`pwsh`) is not
  available in the current environment. Validation PASS is not claimed.
