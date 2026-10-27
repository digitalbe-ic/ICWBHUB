# digital BE Client & Group Loans

WordPress plugin for four-party loan onboarding, staff operations, Surepass KYC, document execution tracking, separate loan/payment obligations and SLT contribution controls.

**Release: 1.0.0-rc.1.** This is an implementation for local testing and operations UAT. Live Surepass account access, AU Bank eNACH, bank transfers, production authentication and production release controls still require the configurations and acceptance checks below. No public website was deployed and no live enquiry, eSign, mandate, transfer or debit was executed during development.

## Workflow

Application and group → original-document capture/review → officer assignment → BC eligibility → counselling → initial-loan documents and mandate → confirmed INR 10,000 initial disbursement → separate INR 10,000 return → SLT membership and separate mandate → FVR/BVR and queries → accepted DB kit → confirmed final BC disbursement → authorized one-time INR 25,000 SLT contribution reconciliation.

The initial lender's loan and repayment/closure, the separate INR 10,000 return, the final BC loan, and the INR 25,000 SLT contribution have independent records. A third-party return does not close the lender's loan or reduce SLT to INR 15,000. A mandate registration and a payment initiation never prove settlement. Unknown attempts require reconciliation before retry.

## Installation

1. Use WordPress 6.5+ with PHP 8.1+, OpenSSL, mysqli and Fileinfo, and a transactional MySQL/MariaDB database. Use HTTPS for authenticated sessions, camera access and provider redirects.
2. Back up the database, private evidence and the encryption key. Configure a stable `DBCL_ENCRYPTION_KEY` containing the base64 encoding of 32 cryptographically random bytes through protected server configuration. If omitted, encryption derives from the WordPress authentication salts; changing those salts then requires recovery of the original salts to decrypt existing records. Do not change encryption material without a tested data migration.
3. Configure `DBCL_PRIVATE_DIR` as a PHP-writable directory outside all public document roots. By default the plugin attempts a private sibling directory to WordPress. Public uploads are not used for private KYC evidence.
4. Install the plugin folder or release ZIP through **Plugins → Add New → Upload Plugin**, then activate it. Activation creates the plugin's InnoDB tables and staff roles.
5. Add the shortcode `[digitalbe_client_group_loans]` to a protected WordPress page. The staff console is **digital BE Loans** in wp-admin. Each participant signs in with their own WordPress account; invitations link the co-applicant and two guarantors to those independent accounts.
6. Configure products/policy, approved text and roles before submitting real customer data. Keep financial operations disabled until independent policy approval and the required integrations/UAT are complete.

Deactivation stops the plugin reminder hook. Uninstall deliberately retains lending, consent, audit and private-evidence records; use an approved retention/export/deletion procedure instead of assuming uninstall deletes regulated records.

## Configuration and staff access

The configuration administrator edits lender/legal-entity identity, grievance contact, BC partner, versioned document templates, signer matrices, exact purpose-specific consent text, financial gate policy and Surepass environment/mappings. Settings changes create a new revision and invalidate prior financial-policy approval. A **different finance checker** approves that exact revision. A supervisor explicitly applies the approved policy to existing cases; material changes require fresh dependent checks and acceptance.

WordPress administrators configure the plugin and do not automatically receive financial maker/checker authority. Assign separate accounts and the minimum required roles:

| Role | Purpose |
| --- | --- |
| Credit officer | Assigned document review, BC/counselling and permitted case commands |
| Verification officer | Assigned FVR/BVR results and evidence |
| Operations officer | Documents, mandate/eSign evidence and DB-kit operations |
| Finance maker | Prepare financial instructions |
| Finance checker | Independent approval and authoritative reconciliation |
| Loan supervisor | Assignment, permitted operations and policy application |
| Loan auditor | Scoped read-only audit access |

Organization and branch scope use the WordPress user metadata `dbcl_org_id` and `dbcl_branch`; assign and test these during deployment. Configure verified mobile authentication and staff MFA through trusted authentication integrations. The `dbcl_mfa_verified` bridge must verify the actual current session; an unconditional passing filter is not an MFA implementation. Enable the staff-MFA policy only after this bridge is installed and tested.

Uploads are validated, encrypted and kept in private storage. Malware-scan results are supplied by the `dbcl_scan_document` adapter; no antivirus product is bundled. The default pending scan must not be represented as clean. A separately approved manual-review policy may be configured, with the actual evidence/result recorded.

Approved documents require lender-owned text, version and signer configuration. Generated HTML can be printed; the plugin does not claim certified PDF conversion or supply an approved legal contract. The eSign path uses an uploaded, approved final PDF with its hash, current terms, actual signer and actual signature coordinates. A specimen signature is a different record.

## Surepass and provider boundaries

The supplied `DigitalBE-Loan-Engine-v2.1.10-RC11-Install.zip` was used to recover existing request contracts. The attached active-subscription CSV determines the available product catalog. No old secret is copied or migrated automatically.

Set `DBCL_SUREPASS_TOKEN` only in protected server configuration, or use the supported encrypted credential option. Select sandbox first. RC11 request mappings cover PAN, bank verification, DigiLocker, Equifax and the document-first eSign sequence; additional active products need confirmed mappings before use. The CSV lists product codes, not complete API schemas. Separate consent is required for KYC, credit-bureau enquiries and eSign. The recovered bureau contract currently accepts only its supported gender values; do not change a party's declared identity to satisfy an unsupported contract.

AU Bank's eNACH API has not been supplied. No AU mandate/debit endpoint is enabled. BC submission, payment, meeting, communication and other adapters require their actual contracts. Evidence-backed officer tasks record externally completed work with its source; they do not manufacture a provider-confirmed result. In-app notifications and stage-based SLA reminders are implemented. External delivery is disabled until an approved adapter is configured; uncertain delivery is not retried blindly. A party can request mandate-authorization withdrawal; the workflow blocks further use immediately and keeps bank cancellation confirmation separate.

Provider evidence retains its sandbox/production environment. Production policy cannot use sandbox KYC evidence. Changing provider policy requires explicit case adoption and fresh affected checks.

See [Surepass contracts and adapter requirements](docs/SUREPASS.md), [form/template mapping](docs/FORM-MAPPING.md), and [project plan and feature traceability](docs/PROJECT-PLAN.md).

## Development and validation

Source is modular PHP with browser JavaScript/CSS and no Composer/npm build dependency. REST endpoints are under `/wp-json/digitalbe-loans/v1/`, use authenticated object scope and expected record versions, and expose business commands instead of unrestricted status edits.

Use a disposable WordPress database. Tests create synthetic records and suppress outbound email and provider networking:

```sh
PHP_BIN=/workspace/.runtime/bin/php \
DBCL_WP_ROOT=/workspace/.runtime/wordpress \
./tools/test.sh
```

See [testing instructions](docs/TESTING.md) for another machine. Local validation uses WordPress 6.9.4, PHP 8.4.27 and MariaDB 11.8.6; this does not establish compatibility with every supported host or live provider account. Provider mocks test request/response interpretation, consent and failure controls. Live sandbox certification, browser/device camera tests, Hindi copy review, load/restore tests, security review and operations/finance UAT remain release gates.

Before production, finalize actual lender/BC identities, borrower allocations, the return recipient and legal purpose, initial-loan closure policy, SLT terms/beneficiary/notice/refund rules, exact FVR/BVR checklists, DB-kit requirements, signing/stamping documents, retention/legal hold and recovery runbooks. Deploy actual mobile authentication, MFA, scanning and communications adapters. Independent audit anchoring and a tested retention/deletion process are operational requirements; the plugin's database audit hash chain alone does not protect against a malicious database administrator.

License: GPL-2.0-or-later.
