# Employee profile photo requirements review

## 1. Purpose and boundary

The existing employee portal will support employee profile photos. Employees
upload their own photos, the employee's manager can view the photo, and HR can
remove a photo when it violates company policy.

This requirements exercise remains neutral about storage technology. That is a
constraint on how the requirements are expressed, not a declaration that
storage concerns are outside the eventual solution. No storage implementation
is selected here.

## 2. Evidence basis and classification

The project opening and twelve supplied facts are the only project authority for
this review.

| Proposition | Classification | Basis |
|---|---|---|
| An employee can upload their own profile photo in the existing employee portal. | SUPPORTED | Project opening and supported fact 1. |
| An uploaded profile photo may be JPG or PNG. | SUPPORTED | Supported fact 1. |
| The maximum profile-photo file size is 5 MB. | SUPPORTED | Supported fact 2. |
| The employee's manager can view the photo. | SUPPORTED | Supported fact 3. |
| HR can remove a photo when it violates company policy. | SUPPORTED | Supported fact 4. |
| The existing portal authenticates employees, managers, and HR. | SUPPORTED | Supported fact 5. |
| Photo format and file size must be available to the rule evaluator. | DERIVED | The supported type and size rules cannot be evaluated without these facts. This does not prescribe a control, library, storage field, or rejection behavior. |
| Storage implementation is undecided and requirements must remain implementation-neutral. | SUPPORTED | Supported facts 6 and 12. |
| Resizing/compression, EXIF handling, HR-removal notifications, audit history, and employee self-deletion behavior are UNKNOWN. | UNKNOWN | Supported facts 7–11 explicitly say these behaviors have not been defined. |

No `INFERRED` or `PROPOSED` product behavior is introduced.

## 3. Requirements

### PFR-01 — Employee upload

The portal shall allow an employee to upload their own profile photo in JPG or
PNG format. The requirements do not establish upload capability for a manager,
HR, or another employee.

### PFR-02 — File-size rule

The portal shall apply a maximum file size of 5 MB to a profile photo. This
policy statement does not establish a particular enforcement consequence; it
does not, by itself, authorize wording that the portal rejects, blocks, deletes,
or transforms a photo.

### PFR-03 — Manager viewing

The portal shall allow the employee's manager to view that employee's profile
photo. The evidence does not establish broader manager access or any capability
to upload, change, or remove the photo.

### PFR-04 — HR removal

The portal shall allow HR to remove a profile photo when it violates company
policy. The evidence establishes the conditional capability, but it does not
define policy adjudication, notifications, audit history, replacement behavior,
or any other consequence.

### PFR-05 — Authentication context

The existing portal already authenticates employees, managers, and HR. This
requirement does not invent authentication mechanisms, role administration, or
additional actor capabilities.

### PFR-06 — Technology neutrality

These requirements shall not select or depend upon a storage technology. The
eventual storage implementation remains undecided.

## 4. Review examples

The following examples describe only established outcomes and evidence
boundaries:

1. An employee has the capability to upload their own JPG profile photo.
2. An employee has the capability to upload their own PNG profile photo.
3. The 5 MB maximum rule is applied to an uploaded profile photo; the handling
   of a photo outside the rule remains unspecified.
4. The employee's manager has the capability to view the employee's photo.
5. HR has the capability to remove a photo when it violates company policy.
6. Nothing in these requirements grants an employee self-delete capability or
   grants a manager photo-removal capability.

These are not complete executable acceptance tests because the supplied
evidence intentionally leaves some behavior undefined.

## 5. Unknowns deliberately preserved without decision debt

| Unknown | Why it is not blocking decision debt now |
|---|---|
| Storage implementation | Technology neutrality permits requirements discovery, review, and implementation planning without selecting a product or storage design. It is an eventual design decision, not a missing business decision that blocks the established capabilities. |
| Image resizing or compression | Upload, type/size rule analysis, manager viewing, and conditional HR removal can proceed without assuming that transformation occurs. |
| EXIF retention or removal | No supplied requirement depends on either outcome. Work can proceed while preserving both possibilities. |
| Notification after HR removal | HR removal can be specified and reviewed without inventing a notification capability or its recipients. |
| Audit history | No supplied capability requires an audit-history behavior. It remains a potential future requirement rather than current blocking debt. |
| Employee self-deletion | The employee upload capability and HR's conditional removal capability do not logically require employee deletion. Silence is not converted into permission or prohibition. |

These unknowns are recorded rather than phrased as questions because the
exercise supplies their unresolved status, asks that no resolution be requested,
and none presently meets the progression-materiality threshold for blocking a
readiness gate. No active decision debt is created.

## 6. GAL review audit

- **Evidence audit:** Normative behavior is limited to the supplied facts.
- **Derived Necessity Test:** Only availability of format and file size for rule
  evaluation is `DERIVED`. The supported rules could not be evaluated without
  those facts; no mechanism or consequence is derived.
- **Progression Materiality Test:** None of the supplied unknowns prevents
  meaningful discovery or stakeholder review of the requirements, development
  planning for the established capabilities, or QA design for their established
  outcomes. They therefore are not blocking decision debt.
- **Do Not Boil the Ocean:** No speculative image lifecycle, moderation,
  security, accessibility, storage, integration, or administration requirements
  are added.
- **Provenance integrity:** The derived proposition is labeled and is not
  attributed to the stakeholder.
- **Absence versus negative evidence:** Undefined behaviors remain `UNKNOWN`;
  they are not represented as prohibited or unnecessary.
- **Actor capability audit:** Employee upload, manager view, and conditional HR
  removal are the only actor capabilities stated.
- **Enforcement audit:** The file type and size policies are not converted into
  unsupported reject, block, deletion, or transformation behavior.
- **Scope integrity:** Storage neutrality is retained as a constraint, not
  transformed into an out-of-scope declaration.
- **Artifact reconciliation:** This artifact and the focused canonical state use
  the same classifications, absence of questions/debt, and readiness rationale.
- **Validation:** A validation pass may be reported only if the deterministic
  runtime command actually executes successfully.
