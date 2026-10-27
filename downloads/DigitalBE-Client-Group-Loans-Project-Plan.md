# Client and Group Loan Application — Project Plan

Developer: **digital BE**. Delivery format: WordPress plugin. Implementation baseline: the attached client/group workflow with SLT contribution, JLG application specification, active Surepass product list and sample central-onboarding form. Existing provider request patterns were recovered from the subsequently supplied **DigitalBE Loan Engine 2.1.10 RC11** package. Legal/commercial sample text is reference material and is not automatically an approved product configuration.

## Product and financial invariants

Each case links an applicant, co-applicant and two guarantors with separate accounts, profiles, documents and individual acceptance. Server-side gate evaluation controls progression; pending external work is not an approval or rejection.

| Obligation | Amount / owner | Required independent evidence |
| --- | --- | --- |
| Initial loan | INR 10,000, actual named lender and approved borrower allocation | Accepted terms, required signatures/mandate, bank verification, instruction and confirmed settlement |
| Return collection | INR 10,000, separately approved named recipient and purpose | Separate authorization, settlement and reconciliation; no automatic lender credit |
| Initial lender repayment / closure | Authoritative lender balance and repayment ownership | Lender repayment/closure evidence; independent of the return receipt |
| Final BC loan | Separately approved principal, lender, terms and beneficiary | BC approval, passed gates, accepted exact DB kit and final settlement |
| SLT contribution | INR 25,000, Shubh Labh Trust, one time | Separate accepted terms/authorization, final BC settlement, due date/notice and one successful reconciled collection |

The INR 10,000 return and INR 25,000 contribution remain INR 35,000 of distinct proposed collections. No offset, fictitious disbursement, automatic lender closure or duplicate successful contribution is permitted. Unapproved cash and third-party repayment routes remain disabled. A failed SLT collection does not change an already settled BC disbursement.

## Delivery stages

| Stage | Implemented deliverable | Completion evidence / remaining release action |
| --- | --- | --- |
| 1. Domain and configuration | Separate obligation records, four-party model, command/gate definitions, versioned policy, template/consent settings and maker/checker policy approval | Confirm lender/BC/SLT identities, allocations, return purpose, closure policy, financial rules and approved versions |
| 2. Portal and operations | Responsive authenticated portal/staff workspace, bilingual form labels, own-party invitations, private uploads, review and assignment | Integrate verified mobile login and staff MFA; run real-device camera/accessibility/Hindi review |
| 3. BC and fulfilment | Evidence-backed BC/counselling tasks, FVR/BVR result handling, separate queries, versioned DB-kit submission/acceptance | Confirm exact partner checklists/full forms, template/signature matrix and external evidence authority; connect partner/meeting APIs where contracted |
| 4. KYC and execution | Surepass active catalog, RC11 request patterns, separate KYC/bureau/eSign consent, pending/failed/unknown handling, approved-PDF execution path | Validate actual subscribed endpoints, credentials, production/sandbox availability and executed PDF delivery in the approved Surepass account |
| 5. Finance controls | Separate ledgers, amount/purpose gates, maker/checker, idempotency, unknown-outcome blocking, settlement/reversal history and one-time SLT guard | Supply AU Bank eNACH and payment contracts; implement/authenticate adapters, certify callbacks and reconcile sandbox transactions |
| 6. Pilot and release | Local WordPress/PHP/MariaDB tests, security-sensitive assertions, HTTP checks and packaged source | Security review, provider certification, backup/restore and load exercise, finance reconciliation, operations UAT and controlled release approval |

## Feature traceability

“Implemented” describes code and local tests. “Evidence route” means authorized staff record externally completed work with references; it does not claim direct automation. “Provider dependent” stays unavailable until its adapter and credentials are configured.

| Requirement | Current implementation | Dependency / boundary |
| --- | --- | --- |
| Four-party group onboarding | Separate role profiles, bank data, own-account invitations and purpose-specific consent | Verified mobile/OTP authentication is a deployment integration; WordPress login is the current authentication boundary |
| Personal, address and bank form | English/Hindi schema mapped to sample, masked identifiers, original-document instructions | Approved field/retention policy and target-device UI review |
| Private original-document evidence | Size/type validation, preserved hash, encrypted private bytes, scoped audited download and review state | Camera metadata is not proof of originality; external malware-scanner adapter and actual staff quality review required |
| Surepass KYC | RC11 PAN/bank/DigiLocker mappings and normalized verified/pending/review/error states | Live token, network access, account entitlement and current schema validation; other active CSV products need confirmed mappings |
| Credit bureau | Recovered Equifax request contract with separate consent; report is not automatic loan approval | Provider account/product availability and approved credit-review policy |
| Officer assignment / branch scope | Assigned case commands, organization/branch boundaries and staff roles | Deployment role administration and MFA bridge |
| BC enrolment and counselling | Partner eligibility and meeting/counselling evidence records with explicit outcomes | Direct partner submission and Google Meet creation require contracted connectors; no meeting or message was sent in development |
| Documents and KFS | Printable version/hash snapshots, initial/BC context, configured legal text, signer matrix and repayment/APR illustration | Approved lender terms, DPN/indemnity/stamp text and actual dates; no built-in certified HTML-to-PDF or approved legal drafting |
| Surepass eSign | Document-first provider interface and approved-PDF/signing service path | Real PDF, correct coordinates, party consent, provider result, encrypted executed artifact and delivery acceptance must be validated together |
| Separate mandates | Purpose-bound initial/BC/SLT records, independent status/evidence gates | AU Bank API, sponsor scheme, payer/beneficiary validation, one-time support and authenticated callbacks not yet supplied |
| FVR / BVR | Distinct task outcome/evidence and blocking failure/review states | Business owner must approve full forms, exact field checklists, location/photo consent and revisit procedure |
| BC queries | Separate open/responded/closed lifecycle; blocking queries gate fulfilment | Partner acknowledgement remains explicit evidence, not inferred from response submission |
| DB kit | Pack version/hash and submit/acceptance commands; changed inputs invalidate dependent readiness | Actual BC checklist/acceptance authority and approved final documents |
| Initial/final disbursement | Controlled instructions and authoritative settlement reconciliation | No bank transfer service is bundled or invoked; production provider execution requires a reviewed adapter |
| Return and lender closure | Independent records, amount checks and source evidence | Return recipient/purpose and lender repayment/closure authority must be approved |
| One-time SLT collection | Final-settlement/date/notice/authorization gates, in-flight guard, idempotency and success protection | Actual eNACH submission/settlement and approved retry/refund rules remain provider dependent |
| Finance maker/checker | Independent instruction/checker controls and source-labeled reconciliation | Assign separate identities; verify privileges in deployment and UAT |
| Audit and reporting | Scoped case queues, gate state, independent financial records, current-page CSV export and hash-linked audit/access history | Full portfolio BI, scheduled exports and external tamper-evident audit anchoring are deployment/extension work |
| Reminders / communications | Private in-app notices, per-user read status, stage-based SLA reminders and durable external-delivery states | An approved SMS/email/WhatsApp adapter, accepted channel consent and delivery templates are required for external messages; unknown delivery is held for reconciliation |
| Retention and recovery | Encryption, retained evidence/history and non-destructive uninstall | Approved retention/deletion/legal-hold jobs, key escrow, restore tests, monitoring and recovery reconciliation remain operational work |

## Configuration sequence

1. Install to a test WordPress site with PHP extensions, HTTPS, transactional database and private evidence storage outside the web root. Keep test and production data/keys separate.
2. Configure stable encryption material and a recoverable backup process before entering customer information. Restrict filesystem/database privileges. Test recovery with the original key and private files.
3. Create separate staff accounts and roles. Configure organization/branch metadata and case assignments. Deploy actual mobile authentication and a session-verifying MFA bridge.
4. Publish exact versioned consent text for each purpose; no checkbox is preselected. Configure lender/BC/SLT identities, approved templates, signer roles, due-date/notice rules and verification/kit policy.
5. Save a policy revision. A different finance checker approves that exact revision. Supervisors apply the approved snapshot to existing cases, triggering required revalidation rather than silently editing history.
6. Configure Surepass securely and verify the relevant contracted APIs in their supported sandbox/production test arrangements. Begin with synthetic/authorized data and a provider-approved validation plan.
7. Supply AU Bank and payment contracts before implementing/enabling live financial adapters. Test authenticated callbacks, duplicates, amount/account/purpose matching, unknown outcomes and reversals. An extension filter alone is not a certified provider integration.
8. Complete source-authority, operations, security and finance UAT. Publish/deploy only through the site's release process after independent sign-off. No deployment was performed as part of development.

## Acceptance and validation plan

The automated suites run against disposable WordPress with synthetic users/cases and intercepted provider HTTP calls. They validate domain/financial invariants, protected API actions, encrypted state/files, individual/group isolation, stale-version conflicts, consent, replay/idempotency and document calculations. See [TESTING.md](TESTING.md) for commands and actual runner output. A passing mock does not establish live Surepass access or a real signature/payment.

Required release scenarios from the attached specification include:

- Missing/unreadable required party evidence blocks submission; a correction does not overwrite original evidence.
- One guarantor cannot read another party's private evidence. A party's own session is required for acceptance.
- Pending BC, mandate or signature results remain pending; a browser return URL cannot mark execution complete.
- Material profile/bank/terms/evidence changes invalidate dependent verification, acceptance, signatures and kit readiness.
- Settling the return leaves the initial lender loan independent and leaves SLT at INR 25,000.
- Pending/failed final disbursement, future SLT due date, insufficient notice, cancelled mandate, failed FVR/BVR, unresolved queries or unaccepted kit prevent dependent operations.
- Concurrent submission, callback replay and worker restart cannot create duplicate successful transfers or SLT collections; unknown outcomes block blind retry.
- A settlement does not regress to pending, and a reversal/refund is preserved as a linked event.
- A financial maker cannot approve their own work or their own policy revision.
- The repayment schedule reconciles principal exactly, preserves calendar anchors and calculates APR from disclosed cashflows and explicit dates.

Outstanding release checks include real browser/device and accessibility review, translated copy review, actual provider sandbox end-to-end journeys, formal threat/security review, capacity/load measurement, backup restore and in-flight-payment recovery, operational monitoring, staff training and finance/operations UAT acceptance. Proposed latency/availability/RPO/RTO figures in the source specification remain targets, not measured service guarantees.

## Release decisions still required

Business/lender owners must finalize actual lender/BC relationships, INR 10,000 borrower allocation and repayment responsibility, approved return recipient/purpose, initial-closure gate and final-loan terms. SLT owners must finalize membership purpose, optional/required participation, beneficiary, cancellation/refund, notice, due-date and failed-debit rules. Operations must finalize FVR/BVR definitions/checklists, DB-kit requirements, document/stamp/eSign matrix and SLA ownership. Engineering/provider owners must supply AU Bank and payment contracts, authentication/MFA/communication/scanning connectors, hosting capacity, monitoring and retention/recovery procedures.

These decisions do not authorize the plugin to infer missing external results or relax the confirmed amount separation.
