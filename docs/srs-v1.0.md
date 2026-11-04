# SIES Alumni Connect
## Product Requirements Document (PRD) and Software Requirements Specification (SRS)

**Document status:** Baseline requirements for discovery, estimation, UX design, implementation and acceptance  
**Reference prototype:** https://sies-alumni-portal.pages.dev/  
**Prepared:** 2 November 2026  
**Product owner:** South Indian Education Society (SIES) — to be formally confirmed  
**Implementation partner:** To be confirmed  
**Document authority:** This document is the proposed single source of truth. Approved changes must be recorded in its change log.

---

## 0. How to use this document

This document converts the publicly accessible AI-assisted reference portal into a production-grade alumni engagement platform. It records observed sections and flows, then specifies standardised behaviour and additional requirements needed for a secure, maintainable system.

### Important evidence and assumptions

1. The reference site itself says that it was developed with AI assistance for illustrative purposes and that names, designations, content and photographs are indicative placeholders. No person, award, institutional fact, date, quote, job, donation destination or contact detail on the prototype should be treated as verified without written SIES approval.
2. The public reference pages were reviewed on 2 November 2026. This is a review of the public-facing rendered site and discoverable navigation, not a source-code audit, penetration test, backend/API inspection or confirmation that every button currently persists data.
3. Some pages expose forms and calls to action but do not establish the complete backend workflow. This specification defines the required production behaviour.
4. “Teacher” is included as an administrative role as requested. A teacher account is not automatically an alumnus and must not inherit alumni-only permissions. Staff/faculty profiles and historical staff records are separate concepts.
5. The platform is initially one SIES-wide deployment supporting multiple institutions, campuses, departments, programmes and batches. It is not assumed to be a commercial multi-tenant SaaS product.
6. Donation collection, payment gateway, accounting, placement integrations, WhatsApp/SMS and email provider are subject to SIES procurement, legal, finance and security approval.
7. Any legal or regulatory conclusion must be validated by SIES counsel. This document defines engineering controls, not legal advice.

### Requirement language

- **MUST**: required for release / acceptance.
- **SHOULD**: expected unless a documented decision defers it.
- **MAY**: optional enhancement.
- **P0**: launch blocker; **P1**: important initial release; **P2**: later enhancement.

---

# 1. Product vision

Build **SIES Alumni Connect**, the official digital engagement platform connecting past students, current and former faculty/staff, institutions, leadership, employers, donors and the Alumni Secretariat.

The portal should preserve the emotional and historical identity of SIES while enabling useful, measurable engagement:

- Find and reconnect with verified alumni.
- Maintain a trusted alumni directory with privacy controls.
- Preserve institutional history, mentors, staff, visitors, presidents, awardees and alumni achievements.
- Enable alumni communities, events, batch reunions and volunteering.
- Share jobs, internships, mentoring and placement opportunities.
- Enable transparent, approved contributions and institutional wishlists.
- Provide SIES administrators with governed content and operational tools.
- Provide the implementation partner with a separate, tightly controlled platform-operations account that cannot be confused with SIES institutional administration.

## 1.1 Product principles

1. **Trust before reach:** verification and privacy are core capabilities, not optional profile settings.
2. **One canonical record:** institutions, programmes, batches, users, alumni, events and content must not be duplicated in disconnected modules.
3. **Consent-led visibility:** personal contact data is private by default; directory visibility and connection sharing are explicit choices.
4. **Institutional governance:** published facts and historical records require accountable approval and provenance.
5. **Least privilege:** users receive only the access necessary for their assigned duties.
6. **Auditable administration:** sensitive changes, approvals, exports and privilege changes are logged.
7. **Accessible and responsive:** usable on mobile, keyboard, assistive technology and low-bandwidth connections.
8. **No fabricated content:** AI may assist drafting or classification but must never invent or silently publish facts.
9. **Operational separation:** SIES controls institutional data and content; the platform operator controls technical service operations through a separate plane.
10. **Exportability:** SIES must be able to export its records and media metadata in documented formats.

---

# 2. Scope

## 2.1 In scope

- Public website and CMS.
- Alumni registration, authentication, profile and verification.
- Alumni directory, filters, connection/intro requests and privacy settings.
- Institution, campus, programme, department and batch master data.
- Alumni-to-stewardship leadership showcase.
- Distinguished alumni / Shining Stars and Nine Jewels / Navaratna showcase.
- Memory Chest, historical records, staff/faculty archive and visitor archive.
- Give Back, contribution categories, institutional wishlist and donation workflow.
- Community circles, membership, coordinators, posts/activities and moderation.
- Career opportunities, employer requests, talent discovery and placement-cell workflows.
- Events, annual gathering, reunions, registration, attendance and communications.
- Alumni Secretariat information, inquiries and campus visit requests.
- SIES administrative console with Superadmin, Admin, Teacher and configurable roles.
- Separate platform-owner master control plane for implementation partner operations.
- Audit logs, reporting, consent, notifications, content approval, security, backups and support tools.

## 2.2 Out of scope unless separately approved

- Full student information system, admissions, examination, LMS or fee management.
- HR/payroll.
- Full recruitment ATS or employer HR system.
- Full accounting/ERP or statutory donation receipt ledger.
- Public social network with unrestricted direct messaging.
- Native iOS/Android apps (responsive PWA is sufficient for initial release).
- AI-generated biographies or historical claims published without human verification.
- Payment custody, fund allocation or financial disbursement by the software vendor.
- Cross-institution external alumni federation beyond SIES without a separate scope.

---

# 3. Reference portal audit: observed information architecture

The following is what was visible in the reference site. These are reference features, not assertions that backend operations are implemented.

## 3.1 Global navigation

- Home
- Alumni
- Memory Chest
- Give Back
- Community
- Career Opportunities
- Events / Participate

The prototype uses Sanskrit/Hindi labels alongside English. Production must standardise labels, translations, spelling, navigation hierarchy and mobile behaviour. English should be the initial canonical content language; other languages can be added through a managed translation workflow.

## 3.2 Home page (`/` and `/home`)

Observed elements:

- SIES Alumni hero statement and welcome message.
- Video/audio welcome experience with voice note controls.
- President's message and full-message link.
- Campuses and institutions cards with descriptions and “Plan a Visit”.
- Futuristic / upcoming institutions sections with placeholder content.
- Alumni Secretariat and governance contact details.
- Secretariat services and contact actions.
- Footer navigation and privacy statement.

Production requirements:
- CMS-managed hero, welcome content, audio/video assets, captions/transcripts and accessible controls.
- President's message with author, designation, approval, publish dates and archive.
- Institution directory driven by master data, not manually duplicated cards.
- Distinguish active institutions, proposed institutions and upcoming projects using explicit status labels.
- “Plan a Visit” must open a structured request form, not a dead link.
- Secretariat contact information must be centrally managed and versioned.
- Never show “update soon” or placeholder content publicly in production; hide incomplete records or display approved “Coming soon” copy.

## 3.3 Alumni — Find an Alumni (`/reconnect`)

Observed:
- Search by name/nickname, institution and passing batch.
- Additional filters for industry/domain, city/metro, India/overseas, institution and passing year.
- Verified alumni results with name, professional role, city, qualification, institution and batch.
- Contact details protected.
- “Connect” / “Request Intro” action.
- Pagination and opt-in directory disclaimer.

Production requirements:
- Search only opted-in, approved, active directory profiles.
- Search by exact/partial name, approved nickname, institution, programme, batch/year, industry, skills and location.
- Avoid exposing email/mobile in HTML, API payloads, search index or analytics unless an authorised disclosure workflow permits it.
- Connection request must be consent-based, rate-limited and auditable.
- Recipient can accept, decline, block or report; contact details are revealed only as defined by both users' consent.
- Search results must respect profile visibility and blocked-user relationships.
- Add abuse controls, duplicate detection, pagination, sorting and empty states.

## 3.4 Alumni — From Alumni to Stewards (`/council`)

Observed:
- Leadership / office-bearer cards with name, role and image.

Production requirements:
- Manage current and historical office bearers, term dates, institution, biography, display order, image rights and approval.
- Separate institutional governance roles from portal permissions.
- Do not grant system access because a person is shown as a Society office bearer.

## 3.5 Alumni — Our Shining Stars (`/distinguished-alumni`)

Observed:
- Distinguished alumni roster; prototype says the list needs updating.

Production requirements:
- Managed recognition profiles with achievement category, award/title, institution, batch, biography, evidence/source, consent, image rights, approval and publication dates.
- Search/filter by institution, field, award and year.
- Support unpublishing, corrections and historical preservation.

## 3.6 Alumni — Our Nine Jewels (`/nine-jewels`)

Observed:
- Nine Navaratna awardee profiles associated with Alumnite ’26, including role, organisation and narrative.

Production requirements:
- Reusable awards and honours module, not a hard-coded nine-card page.
- Manage award edition/year, award name, recipient, citation, event, images and supporting evidence.
- “Nine” must not be a hard-coded system constraint; support any count and future editions.
- Verify award names, biographies and affiliations before publication.

## 3.7 Memory Chest (`/relive`)

Observed:
- Unforgettable Mentors section with institution-wise historical head/principal tables and date ranges.
- Familiar Faces (Staff Members) tab.
- Navigation to other archive categories.

Production requirements:
- Searchable institutional history repository with categories and institution filters.
- Historical appointments must support exact dates, approximate dates, unknown dates, acting/in-charge status, overlapping records and correction notes.
- Never silently “fix” source history; retain original source and editorial correction history.
- Staff/faculty records must be distinguished from alumni profiles.
- Public profile visibility requires appropriate authority and image/content rights.

## 3.8 Memory Chest — Distinguished Visitors / Our Pride (`/our-pride`)

Observed:
- Visitor gallery with names, quotations, designations/affiliations and visit dates.
- The Give Back and Community navigation appears in the page chrome.

Production requirements:
- Visitor record with event/context, institution, date, approved title, quote source, image source and rights, attribution and approval.
- Quote transcription must be checked against the original record.
- Support galleries and chronological archives.

## 3.9 Memory Chest — Share Your Memories (`/relive/share`)

Observed form:
- Memory title.
- Category, institution, year/decade.
- Story/tribute.
- Optional photograph upload (prototype states PNG/JPG up to 10 MB).
- “Show my name” option; otherwise anonymous “SIESian”.
- Statement that submissions are verified by Alumni Archives Committee.

Production requirements:
- Authenticated and verified submitter by default; allow a separately governed guest-submission path only if SIES approves.
- Explicit consent for text, image, identifiable people and public display.
- Upload validation, malware scanning, EXIF stripping where appropriate, safe image processing and storage outside executable web roots.
- Submission states: Draft, Submitted, Under Review, Needs Changes, Approved, Scheduled, Published, Rejected, Withdrawn, Archived.
- Committee moderation queue with comments and decision history.
- Anonymous display must not mean anonymous to authorised moderators.
- Takedown, correction, copyright complaint and privacy request workflows.

## 3.10 Give Back (`/contribute?tab=corpus`)

Observed:
- SIES General Corpus.
- SIES Incubation Centre.
- Veda Pathashala and Preservation of Traditional Knowledge.
- Senior Citizens' Home at Nerul.
- Endowment.
- Institutional Wishlist.
- “Ready to allocate offerings” / proceed call to action.
- Some items indicate contacting the Alumni Secretariat.

Production requirements:
- Configurable fund/campaign categories, each with approved purpose, legal recipient, campaign dates, target (optional), permitted payment methods and disclosure.
- Donation checkout must be integrated only after SIES finance approval and payment provider selection.
- Record payment intent, gateway transaction, status, refund, receipt number and reconciliation reference; never store card credentials.
- Do not represent a payment as a donation until gateway confirmation is verified server-side.
- Support failed, pending, successful, refunded, partially refunded and disputed payments.
- Donation receipt and tax-benefit wording must be approved by SIES finance/legal and must not be inferred by the system.
- Wishlist item lifecycle: Proposed, Submitted, Under Review, Approved, Published, Partially Funded, Fulfilled, Closed, Rejected.
- Donations and fund allocation reports must be access-controlled; public displays must be opt-in and appropriately aggregated.
- Provide non-payment contribution options such as mentoring, volunteering and expertise if SIES approves.

## 3.11 Community (`/communities`)

Observed:
- Community introduction and three-step flow: Explore; Join & Propose; Participate.
- Examples include Music, Literature, Nature Treks, Deep Tech and Social Service.
- Tabs/sections: Community Guidelines, Explore Community, My Community, Start a Community, Upcoming Activities.
- Proposed guideline: minimum 10 interested alumni and two coordinators; administrator approval.
- Rules against political campaigning, commercial solicitation, spam and offensive content.

Production requirements:
- Configurable circle categories and membership rules.
- Community creation request, membership approval, coordinator appointment, activity calendar and moderation.
- Minimum member/coordinator thresholds must be configurable policy, not hard-coded.
- Clear rules, report/block, moderator action and appeal.
- No public exposure of member lists unless each member's visibility permits it.
- Community content moderation, spam controls and rate limits.

## 3.12 Career Opportunities (`/careers`)

Observed:
- Post opportunity form: category (Placement, Internship, Research Project, Others), organisation, position, role requirements, location, contact/application information and remarks.
- Institutional talent/placement sections for engineering, management, arts/science/commerce and other disciplines.
- Resume-book request and campus interview drive calls to action.
- Active alumni postings with job title, employer, location, experience, description, poster and closing date.

Production requirements:
- Opportunity posting must be authenticated and verified; employer identity and poster authority must be checked.
- Moderation before publication.
- Fields: opportunity type, employer, role, description, skills, discipline, experience, employment type, location/remote, compensation (optional), eligibility, application method, closing date, contact, institution/batch targeting and terms.
- Expired listings automatically close; posters/admins can edit, pause, close or renew.
- Report fraudulent or discriminatory listings.
- Resume-book / talent search requires explicit candidate consent, purpose limitation, restricted access, access logs and time-limited downloads.
- Campus placement requests route to the relevant placement office and require approval.
- Avoid publishing private recruiter/alumni contact details unnecessarily.

## 3.13 Events / Participate (`/participate` and `/participate/alumnite-2027`)

Observed:
- Featured Alumnite 2027 event with date/time/venue placeholders and registration action.
- Events calendar, alumni perks, career links.
- Host a Batch Reunion / request reunion planning kit.
- Past gatherings and photos archive.

Production requirements:
- Event management with title, description, event type, host institution, dates, time zone, venue, map link, capacity, registration window, fee (if any), eligibility, agenda, speakers, accessibility, contact and cancellation policy.
- Registration with confirmation, waitlist, cancellation, check-in/attendance and export.
- Configurable registration questions and consent.
- Batch reunion request workflow with year, institution, expected attendees, preferred date, venue/support needs and coordinator.
- Past event archive with approved photos/videos and consent.
- Event date must be stored with timezone; display IST by default for SIES events.
- Alumnite is an event record, not a permanently hard-coded special page.

## 3.14 Footer / shared content

Observed:
- Alumni Secretariat address, email and telephone.
- Home, Alumni, Memory Chest, Give Back, Community, Careers and Events links.
- Voluntary participation / privacy statement.
- Reference-site disclaimer.

Production requirements:
- Central CMS-managed footer and contact details.
- Privacy notice, terms, accessibility statement, grievance/contact channel and cookie/analytics controls as approved.
- Remove the prototype disclaimer from production only after all content is verified and the actual production terms are approved.

---

# 4. Standardised sitemap and navigation

## 4.1 Public portal

1. **Home**
   - Welcome / Hero
   - President's Message
   - About SIES / Legacy
   - Institutions & Campuses
   - Featured Alumni
   - Upcoming Events
   - Featured Opportunities
   - Give Back highlights
   - Secretariat contact

2. **Alumni**
   - Find an Alumni
   - Alumni Profile (public-safe view)
   - From Alumni to Stewards
   - Our Shining Stars
   - Awards & Honours / Nine Jewels
   - Register / Sign in

3. **Memory Chest**
   - Unforgettable Mentors
   - Familiar Faces (Staff & Faculty)
   - Distinguished Visitors
   - Those Who Stood By Us
   - Presidents Through the Years
   - SIES Eminence Awardees
   - Share a Memory
   - Memory detail / archive search

4. **Give Back**
   - Why Give Back
   - Funds & Campaigns
   - Institutional Wishlist
   - Volunteer / Mentor / Contribute Expertise
   - Donation checkout and receipt lookup (authenticated)

5. **Community**
   - Explore Communities
   - Community Details
   - My Communities (authenticated)
   - Start a Community
   - Community Activities
   - Guidelines / Report a concern

6. **Career Opportunities**
   - Browse Opportunities
   - Opportunity Details
   - Post an Opportunity
   - Institutional Talent
   - Placement Cell / Recruiter Request
   - Mentoring (phase 2)

7. **Events**
   - Events Calendar
   - Event Details
   - Alumnite (managed event)
   - Batch Reunions
   - Past Events & Galleries
   - My Registrations (authenticated)

8. **About / Secretariat**
   - SIES Institutions
   - Institution Details
   - Alumni Secretariat
   - Plan a Campus Visit
   - Contact / Inquiry

9. **Account**
   - Sign in / Register
   - My Dashboard
   - My Profile
   - Privacy & Consent
   - My Connections
   - My Submissions
   - My Events
   - My Donations / Receipts
   - Security / Sessions
   - Close Account / Data Request

## 4.2 Authenticated alumni dashboard

- Overview
- Profile & Education
- Verification status
- Directory visibility
- Connections / Requests
- Communities
- Events & registrations
- Career opportunities
- My job posts
- Memories submitted
- Donations & receipts
- Volunteering / Mentoring
- Notifications
- Privacy & security

---

# 5. User types, roles and access model

## 5.1 User categories

- Public visitor (no login).
- Registered alumni (unverified).
- Verified alumni.
- Current student (only if SIES chooses to include them; separate status).
- Current teacher/faculty.
- Former teacher/faculty / staff.
- Employer / recruiter (optional restricted account type).
- Volunteer / community coordinator.
- SIES administrator and institutional staff.
- Platform operator (implementation partner).

A person may have multiple legitimate relationships (e.g. alumnus and teacher). Model these as user affiliations, not mutually exclusive account types.

## 5.2 SIES administrative roles

### A. Superadmin (SIES)

Highest SIES-side administrative role. Can:
- Manage SIES administrators, teachers and custom roles.
- Assign/revoke permissions and institution scopes.
- Manage global SIES master data, configuration and approval policies.
- View all SIES module data subject to sensitive-data safeguards.
- Approve or delegate high-impact actions.
- Review audit logs and operational reports.
- Suspend SIES accounts and revoke sessions.
- Configure public visibility, moderation and retention settings.

Safeguards:
- Superadmin cannot delete or alter platform-owner master account.
- Superadmin cannot access vendor secrets, cloud infrastructure credentials or platform operator control plane.
- No user may remove the final active SIES Superadmin; require at least two active Superadmins and a controlled recovery process.
- High-risk role changes and exports require step-up authentication and audit logging.

### B. Admin

SIES operational administrator. Permissions are granted by Superadmin and scoped by institution/module:
- Manage alumni verification queue.
- Manage content and CMS.
- Manage events, communities, careers, memories and submissions.
- Manage user support cases.
- Manage selected master data only if granted.
- Run permitted reports and exports.
- Assign limited roles only if explicitly granted.

Admin does not automatically have all modules or all institutions.

### C. Teacher / Faculty / Staff

A portal account type and/or administrative role with limited permissions:
- Maintain own staff/faculty profile, subject to approval.
- Submit historical records, mentor information, memories or institutional content.
- Review assigned submissions if granted committee/reviewer permission.
- Participate in approved communities/events.
- View only permitted alumni information.
- Cannot approve own submission or change global settings.
- Cannot browse private alumni contact details unless explicitly authorised for a defined purpose.

“Teacher” must not be a synonym for “Admin”. The permission matrix, not the label, determines access.

### D. Module-specific roles (recommended)

- Alumni Verification Officer
- Content Editor
- Content Publisher
- Archives Contributor
- Archives Reviewer
- Community Moderator
- Event Manager
- Career / Placement Officer
- Donation / Finance Officer
- Institution Coordinator
- Helpdesk / Support Agent
- Read-only Auditor
- Data Protection / Privacy Officer (if designated by SIES)

Roles may be combined where policy allows, but separation of duties should prevent a user from approving their own sensitive submission/payment/refund.

### E. Alumni

- Manage own profile and privacy.
- Request verification and update education details.
- Search directory according to consent.
- Send/receive connection requests.
- Join communities and register for events.
- Submit memories, jobs, reunion requests and contribution interest.
- View own donations/receipts.
- Report content or users.

### F. Public visitor

- View published public content.
- Browse public events and approved opportunities.
- Register/sign in.
- Submit general inquiry or campus visit request if enabled.
- Cannot access private directory data or internal administration.

## 5.3 Separate platform-owner master login (implementation partner)

The implementation partner requires a separate **Platform Owner Control Plane** for internal technical support and platform operations. It must not be implemented as a hidden universal password or an undocumented backdoor.

Recommended design:
- Separate operator identity realm and distinct `/platform-ops` interface or separate host.
- Separate database/schema or strongly isolated control-plane data store.
- One named platform-owner root identity initially, with MFA/passkey and recovery codes; operationally, create named individual operator accounts rather than sharing credentials.
- Emergency break-glass access with dual approval, time limit, reason, alerting and immutable audit.
- Operator identity cannot impersonate alumni, teachers or SIES admins silently.
- Support access to tenant/SIES data must be explicit, scoped, time-bound, approved and audited.
- Platform owner can manage technical service configuration, deployments, integrations, health, backups, subscription/licensing if applicable, feature flags, incident response and support access.
- Platform owner must not silently change SIES institutional content, donations, alumni verification outcomes or governance records.
- Data access for debugging should use redacted/synthetic data wherever possible.
- All support sessions must show a persistent “operator support session” indicator to SIES Superadmin where feasible.
- SIES must be able to view operator access history.
- SIES Superadmin cannot revoke the platform owner's technical identity, but can revoke vendor support grants and data-access approvals.
- Platform owner cannot revoke SIES institutional ownership, export restrictions or audit evidence.
- No shared password in code, database seed, environment file committed to Git or documentation.
- Never expose the platform-owner credential in the SIES admin panel.

**Critical clarification:** A “master login” is a high-value privileged identity and a major attack target. It should be a secure platform-operator account with strong authentication and auditable, limited support access—not a universal account that bypasses every security rule.

## 5.4 Permission model

Use RBAC + scope-based access control:
- Role = what actions a person may perform.
- Scope = which institution, module, content collection or record set they may act on.
- Relationship/ownership = which records they own or are assigned.
- Context = status, approval stage, consent and sensitivity.

Every API request must enforce permission server-side. Hiding a button in the frontend is not authorisation.

Permission actions should include:
- `view`, `create`, `edit`, `delete/archive`, `submit`, `approve`, `publish`, `reject`, `export`, `manage_users`, `assign_role`, `revoke_role`, `configure`, `view_sensitive`, `refund`, `moderate`, `impersonate` (disabled by default).

Permission changes must capture actor, target user, role, scope, reason, before/after state, timestamp and approval where required.

## 5.5 Illustrative access matrix

| Capability | Public | Alumni | Teacher | Admin | SIES Superadmin | Platform Owner |
|---|---:|---:|---:|---:|---:|---:|
| View published pages | Yes | Yes | Yes | Yes | Yes | Technical only |
| View private alumni contacts | No | Consent only | No by default | Explicit grant | Controlled, audited | No by default |
| Edit own profile | No | Yes | Own staff profile | If granted | If needed | No |
| Verify alumni | No | No | Only if assigned | If assigned | Yes/delegate | No |
| Publish public content | No | No | If assigned | If assigned | Yes | No |
| Manage SIES users/roles | No | No | No | Limited if granted | Yes | No |
| Manage platform infrastructure | No | No | No | No | No | Yes |
| Manage vendor integrations/secrets | No | No | No | No | No | Yes, technical |
| Approve donation refund | No | No | No | Finance role | Policy-controlled | No |
| View audit logs | No | Own activity | Limited | Scoped | Full SIES audit | Platform ops logs |
| Grant vendor data support access | No | No | No | No | Yes | Cannot self-grant |

This matrix is a baseline. Final field-level and module-level permissions must be configured and signed off before development completion.

---

# 6. Functional requirements

## 6.1 Identity, registration and authentication

**P0**
- Email-based registration with verified email.
- Optional mobile OTP only if SMS provider and policy are approved.
- Secure password hashing using a modern adaptive password hash (Argon2id preferred; bcrypt acceptable with current parameters and operational review).
- Login, logout, password reset, email change verification and session management.
- MFA/passkeys for all administrators; mandatory for Superadmin and platform owner.
- Rate limiting, bot protection, credential-stuffing protection and suspicious-login alerts.
- Session revocation after password reset, role revocation, account suspension or security incident.
- Account states: Pending Email Verification, Active, Suspended, Locked, Deactivated, Deletion Requested.
- Prevent account enumeration in login and password-reset responses.
- Support account recovery without exposing private profile data.
- Store consent and terms version accepted with timestamp and source.

**P1**
- Social login only after security/privacy review.
- Institution-issued identity/SSO integration if available and approved.

## 6.2 Alumni registration and verification

Registration fields:
- Legal/preferred name; display name; optional former name/nickname.
- Email and mobile (private by default).
- Institution, campus, programme/course, department, qualification.
- Admission year, passing/completion year, batch.
- Student ID / roll / registration number (private, restricted).
- Current city/country, industry, employer, job title, skills (optional).
- Profile photo (optional).
- Verification evidence (restricted upload or approved alternative).
- Consent to verification and directory visibility.

Verification methods (configurable by SIES):
- Manual review against approved institutional records.
- Institution email/domain verification as supporting evidence, not sole proof unless SIES policy says so.
- Student ID / certificate evidence.
- Existing verified alumni referral as supporting evidence.
- Imported legacy alumni records matched and reviewed.
- Admin-entered verified status with evidence source and reviewer.

Statuses:
- Not Submitted
- Submitted
- Under Review
- More Information Required
- Verified
- Rejected
- Suspended
- Verification Expired / Recheck Required (if policy requires)

Rules:
- A user must not self-assign verified status.
- Reviewer must record verification method, decision, timestamp and reason.
- Sensitive evidence must have restricted access and retention rules.
- Profile changes to institution/programme/batch after verification may trigger re-verification.
- Duplicate account handling must merge only after identity review; preserve audit trail and avoid merging unrelated users.

## 6.3 Alumni profile and privacy

Profile sections:
- Basic identity.
- Education at SIES (multiple affiliations supported).
- Career / professional summary.
- Skills and interests.
- Current location (granular visibility control).
- Achievements and recognitions.
- Mentoring/volunteering interest.
- Profile photo and optional cover image.
- Connections and community memberships.
- Verification badge and verification date (public-safe).

Privacy controls:
- Directory listing: hidden / visible to verified alumni / public (public disabled by default; SIES may disable).
- Show name, photo, institution, batch, role, city, interests as separate controls.
- Contact sharing: never / after accepted connection / selected fields.
- Search engine indexing: disabled by default for member profiles.
- Do-not-contact and block controls.
- Export own profile data and request correction/deletion subject to institutional retention obligations.
- Profile preview as seen by public and verified alumni.

## 6.4 Alumni directory and connection workflow

Search/filter:
- Name/nickname.
- Institution/campus.
- Course/programme/department.
- Passing year/batch range.
- Industry, organisation, designation, skills.
- City, country, India/overseas.
- Interests/community (only where consented).

Connection flow:
1. User selects Request Introduction.
2. Optional personal message and purpose.
3. Server checks rate limits, block state and privacy.
4. Recipient receives notification.
5. Recipient accepts, declines, blocks or reports.
6. On acceptance, reveal only fields each party has consented to share.
7. Either party can disconnect or block later.
8. Maintain event history; do not expose private contact data in notification content.

Controls:
- Request throttling and anti-scraping.
- No bulk directory export for ordinary alumni.
- Admin access to directory exports requires a specific permission, reason, approval and audit log.
- Search results should be paginated and use safe query limits.

## 6.5 Institutions and academic master data

Hierarchy:
- Society
- Institution
- Campus
- School/Faculty (optional)
- Department
- Programme/Course
- Qualification
- Academic year / batch

Each record:
- Canonical name, short name, code, status, address, website, contact, logo/images, description, effective dates, parent relation, display order and approval metadata.

Requirements:
- Avoid duplicate institution records.
- Preserve historical institution names and mergers/renaming.
- Support current, historical, proposed and archived statuses.
- Institution coordinators may manage only assigned scope.
- Institution/programme/batch values in alumni forms must come from canonical master data.

## 6.6 CMS and public content

Content types:
- Pages and landing sections.
- Hero banners.
- President/leadership messages.
- Institution profiles.
- Leadership/office bearer profiles.
- Distinguished alumni profiles.
- Awards and award editions.
- Historical archive entries.
- Visitor records and quotations.
- News/announcements.
- Event pages.
- Campaign/fund pages.
- Policies, FAQs and footer/contact blocks.

CMS workflow:
- Draft → In Review → Approved → Scheduled → Published → Archived.
- Optional second approval for sensitive/high-profile content.
- Version history, compare revisions, restore, scheduled publishing and preview.
- Author, reviewer, approver, source, rights/consent, publish date and expiry date.
- SEO metadata, canonical URL, social preview, alt text and structured data.
- Unpublish immediately with reason and audit record.
- No direct database edits as normal content workflow.

## 6.7 Memory Chest and archives

Categories:
- Unforgettable Mentors.
- Familiar Faces (Staff Members).
- Distinguished Visitors.
- Those Who Stood By Us.
- Presidents Through the Years.
- SIES Eminence Awardees.
- Alumni-submitted memories.
- Historical photos, publications and event records.

Data model requirements:
- Person record separate from a role/appointment/visit/award record.
- Institution and time period.
- Start/end date with precision indicator (exact/month/year/approximate/unknown).
- Acting/in-charge designation.
- Source citation or archival reference.
- Original source file, scan or reference.
- Editorial notes and correction history.
- Public visibility and image/quote rights.
- Search by person, institution, category and time period.

Historical data import:
- Import spreadsheet/CSV with validation report.
- Detect duplicate names and overlapping appointments for human review.
- Never auto-resolve conflicting dates or identities.
- Preserve source row and original text.
- Provide bulk preview and rollback.

## 6.8 Memory submission and moderation

Submission form:
- Title (required).
- Category (required).
- Institution (required where relevant).
- Year/decade (optional; support unknown).
- Story/tribute (required; configured length).
- Media uploads (optional).
- Display-name preference: named / anonymous to public.
- Rights/consent confirmation.
- Optional person tags, subject to consent and moderation.

Workflow:
- Submitter receives tracking reference.
- Reviewer can approve, reject, request edits, redact sensitive details or escalate.
- Submitter can edit while changes are requested.
- Approved item can be scheduled or published.
- Post-publication report/takedown workflow.
- Retain moderation history even if content is unpublished.
- Do not expose internal reviewer notes.

## 6.9 Give Back, donation and wishlist

### Campaign/fund management
Fields:
- Fund/campaign name and approved purpose.
- Beneficiary/legal recipient.
- Institution/programme (if applicable).
- Description, images, target and dates.
- Payment methods and gateway configuration.
- Minimum/maximum amount policy.
- Whether anonymous donations are allowed.
- Whether donor name may be publicly displayed.
- Receipt and tax language approved by finance/legal.
- Status and approval.

### Donation journey
1. Visitor/alumnus selects approved campaign.
2. Enters amount and donor details.
3. Reviews purpose, terms, privacy and receipt details.
4. Payment is initiated through approved gateway.
5. Server verifies gateway signature/webhook.
6. Transaction status updates idempotently.
7. Receipt is generated only after confirmed success.
8. Donor can access receipt in account and via secure email.
9. Finance reconciles gateway settlement and bank statement.
10. Refund/cancellation follows role separation and approval.

### Donation ledger
- Unique internal donation ID.
- Gateway order/payment/settlement IDs.
- Donor identity or anonymous marker.
- Campaign/fund.
- Gross amount, fees if known, net settlement where reconciled.
- Currency (INR initially).
- Status, timestamps, receipt number, refund records.
- Reconciliation status and finance notes.

### Institutional wishlist
- Institution, item/project, need statement, estimated cost, priority, supporting document, contact, approvals and status.
- Donors can express interest or contribute through an approved route.
- Track pledged vs received vs fulfilled amounts separately.
- Do not imply that a contribution is restricted to a purpose unless finance has approved the legal/accounting arrangement.

**P0 launch option:** If gateway/legal/finance integration is not ready, launch Give Back as enquiry/pledge/contact workflow only. Do not simulate or collect money through an unapproved flow.

## 6.10 Community management

Community fields:
- Name, slug, description, category, institution scope, image.
- Eligibility, membership visibility, guidelines and coordinator(s).
- Minimum member/coordinator thresholds configurable by Superadmin.
- Status: Proposed, Under Review, Approved, Active, Paused, Archived, Rejected.

Member actions:
- Request/join, leave, mute, report.
- Coordinator accepts/rejects requests if policy requires.
- Members RSVP to community activities.
- Coordinators publish announcements and activities within scope.
- Admin/moderator can hide content, suspend posting or archive a community with reason.

Moderation:
- Report types: spam, harassment, impersonation, commercial solicitation, political campaigning (if prohibited by policy), misinformation, privacy violation, copyright, other.
- Queue, severity, assignment, evidence, action, appeal and resolution.
- Block and rate-limit repeat offenders.
- Publish community charter and moderation policy.

## 6.11 Career and placement opportunities

Opportunity categories:
- Full-time placement.
- Internship.
- Research project.
- Consulting/freelance/advisory.
- Mentorship (future).
- Volunteering (optional).

Required fields:
- Employer/organisation and verified poster.
- Role/title and description.
- Responsibilities, requirements and skills.
- Opportunity type and employment type.
- Location/remote/hybrid.
- Experience and eligible programme/batch.
- Compensation (optional; display “Not disclosed” if absent).
- Application method / external URL.
- Contact details (private where possible).
- Closing date and status.
- Disclaimers and reporting channel.

Lifecycle:
- Draft → Submitted → Under Review → Approved → Published → Paused/Closed/Expired/Rejected.
- Auto-expire after closing date.
- Poster can request edits; material changes may require reapproval.
- Admin can remove suspicious listings and record reason.
- External application link must be validated and opened safely.

Institutional talent:
- Institution placement office manages discipline/programme summaries.
- Resume book request requires verified recruiter, purpose, institution approval and candidate consent.
- Resume files must not be publicly downloadable.
- Candidate-level sharing must be explicit and logged.
- Support request for campus drive with employer details, role count, dates and placement-cell review.

## 6.12 Events, Alumnite and reunions

Event types:
- Annual alumni gathering.
- Institution event.
- Batch reunion.
- Networking meet.
- Webinar / lecture.
- Community activity.
- Career / placement event.
- Fundraising event.

Event fields:
- Title, event type, organiser, host institution.
- Summary and full description.
- Start/end date/time and timezone.
- Venue, address, map link, online meeting link (restricted).
- Capacity, registration open/close.
- Eligibility, fee, payment reference (if applicable).
- Schedule/agenda, speakers, accessibility and contact.
- Cancellation and refund policy.
- Media/gallery settings and consent.

Registration:
- Authenticated registration by default; guest registration only if approved.
- Confirmation number, QR code (optional), waitlist.
- Edit/cancel subject to policy.
- Check-in list and attendance.
- Event-specific consent.
- Export restricted to event organisers.
- Duplicate registration prevention and capacity locking.
- Bulk email notifications with unsubscribe/preferences where applicable.

Batch reunion request:
- Institution, batch/year, expected attendance, organiser contacts.
- Proposed dates, venue preference, support required.
- Approval and assigned Secretariat coordinator.
- Secure contact roster sharing only where members have consented.

## 6.13 Alumni Secretariat, inquiries and campus visits

- Central contact profile, office hours, map, address, phone and email.
- Inquiry categories: general, verification, profile, event, reunion, donation, archives, placement, privacy, technical.
- Ticket/reference number and status.
- Assignment, internal notes, response history, SLA and closure.
- Campus visit request: institution, preferred date/time, visitor count, purpose, accessibility needs and contact.
- Approval by institution coordinator; confirmation and visitor instructions.
- Spam protection and consent.
- Do not publish internal staff contact details unless approved.

## 6.14 Notifications

Channels:
- In-app notification.
- Email.
- SMS/WhatsApp only after provider and consent approval.

Events:
- Registration and verification.
- Verification decision / additional evidence.
- Connection request and response.
- Community approval/activity.
- Memory moderation outcome.
- Job post moderation and expiry.
- Event registration, reminder, change or cancellation.
- Donation confirmation/receipt/refund.
- Admin role assignment/revocation.
- Security events and support access.

Requirements:
- Templates centrally managed and versioned.
- User notification preferences.
- Transactional/security notifications cannot be disabled where needed for account safety.
- Avoid exposing sensitive details in subject lines or SMS.
- Delivery status, retry and provider error logs.
- Idempotent event delivery; avoid duplicate messages.

## 6.15 Reporting and dashboards

SIES dashboards:
- Registered users, verified alumni and pending verification.
- Alumni by institution, programme, batch and geography (aggregated).
- Profile completion and directory opt-in rates.
- Connection request activity.
- Community membership and activity.
- Events, registrations, attendance and cancellations.
- Jobs/opportunities, applications/referral interactions if captured.
- Memory submissions and moderation turnaround.
- Campaign totals and reconciled donation summaries (finance restricted).
- Admin activity and audit alerts.

Requirements:
- Date range, institution and module filters.
- Role-based visibility.
- CSV/XLSX export only for authorised roles.
- Exports include generation time, actor, scope and purpose.
- Aggregate small groups carefully to avoid re-identification.
- Dashboard metrics must have documented definitions and consistent time zones.

---

# 7. Admin panel specification

## 7.1 Admin URL and layout

Use a separate authenticated route such as `/admin` (exact host/path to be decided). Responsive layout:
- Left navigation with role-filtered menus.
- Global search.
- Notifications and task queue.
- Breadcrumbs.
- Institution/scope selector where applicable.
- User menu, MFA/security status and logout.
- Dashboard widgets based on permission.

Do not show inaccessible menus as active navigation. A direct URL/API call must still be denied server-side.

## 7.2 Admin menu and submenus

### 1. Dashboard
- Overview
- Pending Tasks
- Verification Queue
- Content Approval Queue
- Memory Moderation Queue
- Community Reports
- Career Approval Queue
- Upcoming Events
- System Alerts (SIES-level only; not infrastructure secrets)

### 2. User & Alumni Management
- All Users
- Alumni
- Teachers / Faculty / Staff
- Administrators
- Recruiters / Employers
- Volunteers / Coordinators
- Registration Requests
- Alumni Verification
- Duplicate Accounts
- Suspended / Blocked Accounts
- User Import
- User Export (permission-gated)
- Account Activity

### 3. Roles & Permissions
- Role List
- Create Custom Role
- Permission Matrix
- Assign Roles
- Revoke Roles
- Scope / Institution Assignment
- Temporary Access
- Access Review
- Privileged Action Approval
- Role Change History

### 4. Institutions & Academic Data
- Institutions
- Campuses
- Departments
- Programmes / Courses
- Qualifications
- Academic Years
- Batches / Passing Years
- Institution Coordinators
- Historical Names & Mappings
- Import / Validation

### 5. Alumni Directory
- Directory Records
- Profile Review
- Visibility / Consent Review
- Connection Requests (aggregate/moderation only; private message access restricted)
- Reports / Abuse
- Directory Configuration

### 6. Website & CMS
- Pages
- Navigation Menus
- Home Page Sections
- Hero Banners
- President's Messages
- Institution Pages
- Leadership / Stewards
- Shining Stars
- Awards / Nine Jewels
- Footer & Contact Details
- SEO / Metadata
- Media Library
- Drafts / Scheduled
- Revision History
- Content Approval

### 7. Memory Chest & Archives
- Archive Categories
- Mentors / Principals
- Staff & Faculty
- Distinguished Visitors
- Presidents
- Those Who Stood By Us
- SIES Eminence Awardees
- Submitted Memories
- Media / Documents
- Sources & Provenance
- Moderation Queue
- Takedown / Correction Requests
- Bulk Import

### 8. Give Back & Finance
- Funds / Campaigns
- Institutional Wishlist
- Donation Transactions
- Pledges / Enquiries
- Receipts
- Refund Requests
- Reconciliation
- Finance Reports
- Gateway Configuration (restricted; secrets never displayed)
- Donation Terms / Receipt Templates

### 9. Community
- Community Categories
- Community List
- Creation Requests
- Membership Requests
- Coordinators
- Activities
- Reports & Moderation
- Community Guidelines
- Community Analytics

### 10. Careers & Placement
- Opportunities
- Pending Approvals
- Employers / Recruiters
- Institutional Talent Profiles
- Resume Book Requests
- Campus Interview Requests
- Reports / Fraud Flags
- Career Categories
- Placement Reports

### 11. Events & Reunions
- Events
- Event Categories
- Alumnite
- Registrations
- Waitlists
- Attendance / Check-in
- Batch Reunion Requests
- Past Events & Galleries
- Event Communication
- Event Reports

### 12. Secretariat & Helpdesk
- Inquiries
- Support Tickets
- Campus Visit Requests
- Reunion Planning Requests
- Assignment / SLA
- FAQ
- Contact Directory
- Escalations

### 13. Notifications & Communications
- Email Templates
- SMS/WhatsApp Templates
- In-app Templates
- Notification Queue
- Delivery Logs
- Campaigns / Announcements
- User Preferences (view only; do not override individual consent casually)

### 14. Reports & Analytics
- Alumni Reports
- Verification Reports
- Engagement Reports
- Institution Reports
- Events Reports
- Community Reports
- Career Reports
- Archive Reports
- Finance Reports (restricted)
- Admin Activity Reports
- Export History

### 15. Governance & Compliance
- Audit Logs
- Consent Records
- Privacy Requests
- Retention Policies
- Data Export Requests
- Data Correction Requests
- Deletion / Deactivation Requests
- Content Rights Register
- Policy Versions
- Incident Register
- Access Reviews

### 16. SIES Configuration
- General Settings
- Branding
- Localisation
- Public Registration Settings
- Verification Rules
- Directory Rules
- Moderation Rules
- Upload Limits
- Event Defaults
- Notification Settings
- Feature Flags (SIES business features only)
- Integration Status (no secret values)
- Maintenance Banner

## 7.3 Platform Owner Control Plane (separate interface)

This is not a submenu inside the SIES admin panel. It is a separate operator interface and security boundary.

Menus:
- Platform Overview
- Environments / Deployments
- Service Health
- Background Jobs / Queues
- Database Health (metadata/health, not unrestricted content browsing)
- Storage / Backup Status
- Domain / TLS Status
- Integration Health
- Error Monitoring
- Feature Flags / Release Controls
- Version / Release History
- Support Access Requests
- Active Support Sessions
- Operator Accounts / MFA
- Break-glass Access
- Security Events
- Incident Management
- Backup Restore Requests
- Data Export / Migration Jobs
- Platform Audit Logs
- Vendor Configuration / Secrets (masked; never reveal secret after creation)
- Maintenance / Status Page

Operator permissions:
- Technical operations are allowed only within approved environment.
- Production data access is disabled by default.
- Support access requires SIES Superadmin approval, a ticket/reason, minimum scope, expiry and audit.
- Emergency access must alert SIES and be reviewed after the incident.
- Destructive production actions require confirmation, backup/rollback plan and, for critical actions, dual approval.
- All actions must be attributable to a named operator; no shared root password.

---

# 8. Core workflows and acceptance criteria

## 8.1 Alumni registration and verification

1. User registers and verifies email.
2. User completes education details and submits verification.
3. System creates a verification case.
4. Verification officer reviews evidence and institutional record.
5. Officer approves, rejects or requests more information with reason.
6. User is notified.
7. On approval, verified status is displayed and directory listing follows the user's separate visibility consent.

Acceptance:
- User cannot set their own verified flag.
- Every decision has actor, date, method and reason.
- Rejected/under-review users are not shown as verified.
- Evidence is visible only to authorised reviewers.
- Revoking verification immediately updates directory eligibility and invalidates cached search results.

## 8.2 Admin role assignment/revocation

1. Superadmin opens user record.
2. Selects role and scope.
3. System previews effective permissions.
4. Superadmin enters reason and confirms with MFA/step-up authentication for privileged roles.
5. System writes immutable audit event and sends notification.
6. Revocation takes effect immediately, invalidates active sessions/tokens where appropriate and removes access from subsequent requests.

Acceptance:
- No role escalation via client-side request manipulation.
- Admin cannot grant a role above their authority.
- Final Superadmin protection is enforced.
- Temporary access expires automatically.
- Role changes are searchable in audit history.

## 8.3 Memory moderation

1. Alumni submits story and media.
2. System validates fields and uploads.
3. Submission enters moderation queue.
4. Reviewer checks accuracy, rights, privacy and appropriateness.
5. Reviewer approves, requests edits or rejects.
6. Publisher schedules or publishes.
7. Public page shows approved version only.

Acceptance:
- Pending content never appears publicly.
- Anonymous public display does not hide submitter identity from authorised reviewers.
- A post-publication takedown can be completed without deleting audit history.

## 8.4 Donation

1. Donor selects approved fund.
2. System creates a pending order.
3. Payment gateway handles payment.
4. Server verifies webhook/signature and transaction amount/order.
5. System marks success idempotently.
6. Receipt generated and email sent.
7. Finance reconciles settlement.

Acceptance:
- Browser redirect alone cannot mark payment successful.
- Duplicate webhook does not create duplicate donation/receipt.
- Amount/currency/order mismatch is rejected and flagged.
- Refunds require separate finance permission and audit.
- No card number/CVV is stored by the portal.

## 8.5 Job post

1. Verified alumnus/employer submits opportunity.
2. System validates and creates pending listing.
3. Career admin verifies poster/employer and reviews content.
4. Approved listing is published.
5. Listing closes/archives on closing date.
6. Users report suspicious listings; moderation acts.

Acceptance:
- Unapproved listing is not publicly searchable.
- Expired listing cannot accept new applications through portal-controlled actions.
- Contact details are protected from scraping.
- Recruiter resume access requires explicit candidate consent.

## 8.6 Event registration

1. Admin publishes event and registration window.
2. User views details and registers.
3. System enforces capacity atomically.
4. Confirmation and reminder notifications are sent.
5. Admin checks in attendee.
6. Event closes and attendance report is available to authorised organisers.

Acceptance:
- Capacity cannot be exceeded by simultaneous requests.
- Duplicate registrations are prevented according to event policy.
- Cancelled events trigger notifications and registration status updates.
- Attendee exports are restricted and logged.

---

# 9. Data architecture and core entities

Use a relational source of truth for structured institutional and transactional data. A relational database such as PostgreSQL is recommended unless the implementation architecture review documents a compelling reason otherwise.

Core entities (indicative; final ERD required):
- `users`
- `user_credentials` / identity provider references
- `user_sessions`
- `user_affiliations`
- `roles`
- `permissions`
- `role_permissions`
- `user_role_assignments`
- `scopes` / `institution_scope_assignments`
- `institutions`
- `campuses`
- `departments`
- `programmes`
- `qualifications`
- `academic_batches`
- `alumni_profiles`
- `education_records`
- `career_records`
- `profile_privacy_settings`
- `consent_records`
- `verification_cases`
- `verification_evidence`
- `connection_requests`
- `blocks`
- `content_pages`
- `content_versions`
- `media_assets`
- `leadership_profiles`
- `awards`
- `award_recipients`
- `archive_people`
- `archive_appointments`
- `archive_visits`
- `archive_sources`
- `memory_submissions`
- `moderation_cases`
- `funds`
- `campaigns`
- `donations`
- `payment_attempts`
- `receipts`
- `refunds`
- `reconciliation_records`
- `wishlist_items`
- `communities`
- `community_memberships`
- `community_coordinators`
- `community_activities`
- `community_posts` (if approved)
- `reports`
- `career_opportunities`
- `employers`
- `recruiter_access_requests`
- `events`
- `event_registrations`
- `event_attendance`
- `reunion_requests`
- `inquiries`
- `support_tickets`
- `notifications`
- `notification_deliveries`
- `audit_events`
- `privacy_requests`
- `policy_versions`
- `platform_operators`
- `support_access_grants`
- `platform_operations_events`

Data principles:
- Use immutable internal IDs (UUID/ULID).
- Add created/updated timestamps and actor IDs.
- Use soft-delete/archive for records requiring history; hard deletion only through approved retention workflow.
- Use foreign keys and database constraints for integrity.
- Use unique constraints for identity and natural keys where appropriate.
- Store date/time in UTC; retain event timezone and display in Asia/Kolkata by default.
- Store currency as ISO currency code plus integer minor units (paise), not floating-point.
- Separate PII and sensitive evidence from public content where practical.
- Encrypt sensitive fields at rest using managed keys where appropriate.
- Never store passwords, OTPs, payment card data or secrets in plaintext.
- Maintain data lineage for imports and archival facts.

---

# 10. Technical architecture requirements

The final stack must be selected through a written architecture decision record (ADR). Suggested baseline:

- Frontend: React + TypeScript + Vite, responsive component system.
- Backend: Node.js + TypeScript + a maintained HTTP framework (Express is acceptable with disciplined validation/middleware; NestJS may be evaluated).
- Database: PostgreSQL.
- Cache / rate limiting / job coordination: Redis or equivalent only where needed.
- Object storage: S3-compatible private bucket for media and evidence; CDN for public derivatives only.
- Background jobs: durable queue for email, image processing, imports, reports and notifications.
- Reverse proxy/WAF: managed edge/WAF and hardened reverse proxy.
- Search: PostgreSQL full-text/trigram initially; dedicated search engine only if scale justifies it.
- Observability: structured logs, metrics, tracing, error monitoring and alerting.
- Deployment: repeatable CI/CD with staging and production separation, infrastructure as code and rollback.

## 10.1 Application boundaries

- Public web application.
- Authenticated alumni application.
- SIES admin application.
- Separate platform-owner control plane.
- Backend API with service/domain boundaries.
- Background worker service.
- Private object storage.
- Relational database.
- Email/SMS/payment integrations.

The platform-owner plane must have distinct authentication, authorisation and audit. It must not be a frontend-only “hidden route” in the same trust boundary.

## 10.2 API requirements

- Versioned API (`/api/v1`).
- OpenAPI specification maintained with code.
- Request schema validation and output shaping.
- Consistent error format and correlation/request IDs.
- Pagination, filtering and sorting limits.
- Idempotency keys for payments and other retry-sensitive operations.
- Server-side authorisation on every resource.
- No mass assignment; explicit DTO allowlists.
- Rate limits by user, IP, endpoint and action.
- Webhook signature validation and replay protection.
- Audit middleware for privileged/sensitive actions.
- No sensitive values in URLs, logs or analytics.
- CORS allowlist; CSRF protection where cookie sessions are used.

## 10.3 Security baseline

- OWASP ASVS-aligned security review and OWASP Top 10 coverage.
- TLS 1.2+ (TLS 1.3 preferred).
- Secure, HttpOnly, SameSite cookies where applicable.
- CSRF protection.
- Content Security Policy and secure headers.
- Strict input validation and output encoding.
- SQL injection prevention through parameterised queries/ORM.
- XSS prevention and safe rich-text sanitisation.
- SSRF protections for external URL fetches.
- File upload type/signature/size checks, malware scanning and isolated processing.
- Secrets manager; no credentials in source control.
- MFA for privileged users.
- Session idle/absolute expiry and device/session revocation.
- Dependency scanning, SAST, DAST and container/image scanning.
- Backup encryption and restore testing.
- Security incident response and breach escalation plan.
- Independent penetration test before production and after material security changes.

## 10.4 Privacy and data governance

- Data inventory and classification.
- Purpose limitation and minimum necessary collection.
- Separate consent for directory visibility, contact sharing, marketing, photos/media and resume sharing.
- Consent version and timestamp.
- User self-service privacy controls.
- Access, correction, grievance, deletion and retention workflows as applicable.
- Data retention schedule approved by SIES.
- Restrict staff access to evidence and private contact data.
- Audit all sensitive data views and exports.
- Data processor/vendor agreements and subprocessor register.
- Cross-border hosting/processing decisions documented and approved.
- Applicable Indian data protection, IT, payment and institutional obligations to be reviewed by SIES counsel and compliance team before launch.

## 10.5 Availability, performance and scale

Initial sizing must be based on an agreed forecast; do not invent concurrent-user or record-volume targets. Establish a baseline during discovery.

Proposed measurable targets for sign-off:
- 99.9% monthly availability target for production, excluding approved maintenance and agreed third-party outages.
- 95th percentile normal API response under 500 ms for read endpoints under agreed load, excluding external providers and heavy reports.
- Main public pages LCP target ≤ 2.5 seconds on representative mobile network/device test profile.
- No loss of confirmed payment state or accepted registrations during retry/restart.
- Background jobs retry safely and expose dead-letter/failed status.
- Horizontal scaling for stateless API/worker services.
- CDN caching for public assets and pages; never cache private profile/API data publicly.
- Load test at agreed peak concurrent-user and event-registration scenarios.

## 10.6 Backup and disaster recovery

- Automated encrypted database backups.
- Point-in-time recovery where supported.
- Object storage versioning / backup strategy.
- Separate backup credentials and account/project.
- Immutable or protected backup copies.
- Documented RPO/RTO approved by SIES.
- Quarterly restore test at minimum, with evidence.
- Backup retention and deletion policy.
- Production restore must require authorised approval and be audited.
- Do not treat RAID, replication or snapshots alone as a complete backup strategy.

---

# 11. UX, accessibility and content standards

- Responsive layouts for mobile, tablet and desktop.
- WCAG 2.2 AA target for core journeys.
- Keyboard navigation, visible focus, semantic headings, labels and error messages.
- Alt text for meaningful images; decorative images marked appropriately.
- Captions/transcripts for video/audio; audio must not autoplay with sound.
- Respect reduced-motion settings.
- Consistent spacing, typography, colour contrast, buttons, cards, forms and status labels.
- Clear loading, empty, success, error and permission-denied states.
- Confirm destructive actions and explain consequences.
- Preserve entered form data after validation errors.
- Use plain language; avoid inconsistent English/Sanskrit/Hindi labels.
- Translation-ready architecture; do not mix language strings into business logic.
- Search filters must be understandable and usable on mobile.
- Do not use fabricated testimonials, fake alumni, fake job listings or sample donations in production.
- Use labelled demo/test data only in non-production environments.

---

# 12. AI usage policy for implementation and product content

The client used AI to develop the reference concept. AI may be used during implementation for brainstorming, code assistance, test generation, data cleanup suggestions and draft copy, but the following rules are mandatory.

1. AI output is a proposal, never an authoritative source.
2. Never invent institutional facts, alumni identities, biographies, achievements, quotes, office bearers, historical dates, donation claims or legal wording.
3. AI-generated code must be reviewed, tested and security-checked by a qualified developer.
4. Do not send private alumni records, identity documents, contact data, donation data, credentials or production database dumps to public AI services.
5. Any AI service processing personal data requires explicit SIES approval, vendor assessment, data-processing terms and documented data-flow review.
6. AI must not decide alumni verification, donation approval/refund, moderation sanctions or administrator privileges without a human decision.
7. AI may suggest duplicate historical records, but a human must confirm merges.
8. AI-generated summaries must link to the source records and be labelled internally as machine-assisted until approved.
9. Do not allow AI agents to run arbitrary SQL, shell commands or production changes.
10. Maintain prompt/output logs only where safe and necessary; redact personal and secret data.

---

# 13. Non-functional requirements

| Area | Requirement |
|---|---|
| Security | MFA for privileged accounts; server-side RBAC/scope enforcement; audit trail |
| Privacy | Explicit granular consent; private-by-default contact data |
| Accessibility | WCAG 2.2 AA target |
| Performance | Targets defined in Section 10.5 and validated under agreed load |
| Availability | Proposed 99.9% monthly target, subject to hosting/SLA |
| Reliability | Idempotent payments, registrations and webhook processing |
| Maintainability | TypeScript, modular services, linting, tests, ADRs and code review |
| Portability | Documented deployment and data export; avoid proprietary lock-in where practical |
| Observability | Structured logs, metrics, traces, alerting and correlation IDs |
| Compatibility | Current and previous major versions of supported browsers, defined at release |
| Localisation | Timezone-aware dates; INR; translation-ready |
| Data integrity | Referential constraints, validation, import reports and audit history |
| Recovery | Approved RPO/RTO, restore tests and incident runbooks |

---

# 14. Testing and quality assurance

Mandatory test layers:
- Unit tests for domain rules and permission checks.
- Integration tests for database, queue, storage and external provider adapters.
- API contract tests against OpenAPI.
- End-to-end tests for all P0 journeys.
- Role/permission matrix tests, including denied access.
- Security tests: auth, IDOR, privilege escalation, injection, XSS, CSRF, file upload, rate limit and session revocation.
- Privacy tests: private fields absent from unauthorised API responses, logs, exports and search.
- Payment tests: success, failure, timeout, duplicate webhook, invalid signature, amount mismatch, refund and reconciliation.
- Concurrency tests: event capacity, duplicate registration and simultaneous updates.
- Accessibility tests: automated plus manual keyboard/screen-reader checks.
- Responsive tests across supported browsers/devices.
- Performance/load tests using agreed workload.
- Backup restore and disaster recovery test.
- UAT with SIES Secretariat, institution coordinators, alumni representatives, finance and IT/security.

No release is accepted solely because the frontend “looks correct”.

---

# 15. Release plan and prioritisation

## Phase 0 — Discovery and governance

- Confirm institutional stakeholders and decision owners.
- Validate all prototype content and navigation.
- Obtain official institution/programme/batch data.
- Agree privacy, verification, retention, content approval and donation policies.
- Finalise role matrix and platform-owner access agreement.
- Confirm hosting, data location, integrations, RPO/RTO and scale forecast.
- UX prototypes and architecture ADRs.
- Sign off this PRD and change-control process.

## Phase 1 — Production foundation (P0)

- Design system and public CMS pages.
- Institution master data.
- Authentication, account management and MFA for admin.
- Alumni registration, verification and profiles.
- Privacy settings and opt-in directory.
- Alumni directory and connection requests.
- SIES admin panel and role/scope engine.
- Separate platform-owner control plane and audited support access.
- Audit logs, consent, notifications, backups and monitoring.
- Basic Secretariat inquiry/ticketing.
- Security review and UAT.

## Phase 2 — Engagement modules (P1)

- Memory Chest and moderation.
- Leadership, Shining Stars, awards and Nine Jewels.
- Communities and moderation.
- Career opportunities and placement requests.
- Events, Alumnite and batch reunions.
- Media archive and past event galleries.
- Reporting and exports.

## Phase 3 — Give Back and advanced operations (P1/P2)

- Institutional wishlist.
- Donation gateway and receipts after finance/legal approval.
- Reconciliation and refund workflows.
- Volunteer/mentor programme.
- Advanced recruiter access and consent-based talent discovery.
- Enhanced analytics and integrations.

## Phase 4 — Optimisation (P2)

- PWA enhancements.
- Additional languages.
- SSO/institution integrations.
- Advanced search.
- Alumni mentoring and structured programmes.
- AI-assisted archival indexing with human review.
- Additional communication channels.

---

# 16. Acceptance gates / definition of done

A module is complete only when:
1. Approved user stories and acceptance criteria are implemented.
2. UI, API and database behaviour match this document.
3. Server-side permissions are tested for allow and deny cases.
4. Validation, empty/error/loading states and audit events are present.
5. Accessibility and responsive checks pass.
6. Unit, integration and end-to-end tests pass.
7. Security and privacy review is completed for sensitive modules.
8. Documentation, API specification and admin help are updated.
9. Logs/metrics/alerts exist for production-critical workflows.
10. Backup/restore implications are understood.
11. UAT owner signs off.
12. No P0/P1 release-blocking defects remain.
13. Deployment and rollback procedure is tested.

## 16.1 Release blockers

- Any unauthorised user can view private alumni contact/evidence.
- Role escalation or access after revocation is possible.
- Platform-owner account can silently impersonate SIES users.
- Payment can be marked successful without server-side gateway verification.
- Pending or rejected content is publicly visible.
- Unapproved donation campaign or inaccurate tax claim is published.
- File upload can execute or expose private files.
- Admin actions lack attributable audit records.
- Critical data cannot be backed up/restored.
- Production includes fabricated placeholder identities or unverified institutional claims.

---

# 17. Risks and mitigations

| Risk | Impact | Mitigation |
|---|---|---|
| Incorrect AI-generated historical facts | Reputational harm | Source/provenance fields and institutional approval |
| Alumni identity fraud | Directory trust loss | Multi-method verification and review |
| Contact data scraping | Privacy harm | Consent filters, API shaping, rate limits, no bulk public export |
| Privileged account compromise | Full platform compromise | MFA/passkeys, named accounts, least privilege, alerts, break-glass |
| Vendor master account becomes backdoor | Loss of institutional control | Separate plane, scoped support grants, visible audited access |
| Donation misrepresentation | Financial/legal exposure | Finance approval, verified gateway webhooks, reconciliation |
| Unmoderated jobs/community posts | Fraud/harassment | Verification, moderation, report/block and audit |
| Historical data conflicts | Incorrect archive | Preserve source, human resolution, correction history |
| Uncontrolled media rights | Copyright/privacy claims | Rights register, consent, takedown process |
| Scope expansion | Budget/time overrun | Phased delivery and formal change control |
| Poor data quality | Incorrect search/reporting | Master data governance and import validation |
| Provider outage | Lost notifications/payments | Retry queues, idempotency, provider monitoring |

---

# 18. Open decisions requiring SIES sign-off

Do not silently assume answers to these questions.

1. Which legal SIES entity owns and controls the portal and personal data?
2. Who are the named product owner, SIES Superadmins and module approvers?
3. Which institutions/campuses are in launch scope? Confirm official names and hierarchy.
4. Is registration open to all former students or limited to approved batches/institutions?
5. Which verification sources and evidence types are acceptable?
6. Will students, current teachers, former teachers and non-alumni staff have accounts?
7. What exact data may be visible to public visitors versus verified alumni?
8. Are direct messages required, or are connection/intro requests sufficient?
9. Which committee approves archives, memories, awards and high-profile biographies?
10. Who approves job posts and recruiter access to resumes?
11. Are communities open only to verified alumni? Can teachers/students join?
12. Which donation funds are legally approved, and who is the recipient?
13. Which payment gateway and receipt/tax wording are approved?
14. Is online donation collection in Phase 1 or deferred?
15. What is the official Alumnite/event calendar and registration policy?
16. What is the retention period for verification documents, inquiries, donations and audit logs?
17. Which hosting region/data location is required?
18. What are expected alumni count, peak concurrent users, event registrations and media volume?
19. What RPO, RTO, uptime SLA and support hours are required?
20. Which email, SMS and WhatsApp providers are approved?
21. Is SSO required with any SIES identity or institutional system?
22. What accessibility and language requirements are mandatory?
23. Who owns the domain, cloud accounts, source repository, payment gateway and backups?
24. What level of platform-operator support access will SIES permit?
25. What is the process if the implementation/vendor relationship ends (handover, credentials, data export, deployment and continuity)?

---

# 19. Required project deliverables

Implementation team must produce and maintain:
- Approved UX sitemap and responsive wireframes.
- Design system and component library.
- Detailed use cases and user stories.
- Final role-permission-scope matrix.
- Architecture diagram and ADRs.
- Entity relationship diagram and data dictionary.
- OpenAPI specification.
- Data import templates and validation reports.
- CMS content model.
- Security threat model and data-flow diagram.
- Privacy/consent and retention matrix.
- Test plan, automated test suite and UAT scripts.
- Deployment, rollback and environment documentation.
- Backup, restore and disaster recovery runbooks.
- Admin and user manuals.
- Incident response and support procedures.
- Source code, infrastructure code and build/deployment pipeline.
- Handover package and credentials transferred through a secure secret-management process.

SIES should own or have contractually guaranteed access to the source repository, production cloud account, domain/DNS, database, object storage, payment gateway account, backups, logs and documentation. Vendor access should be delegated, not achieved by making the vendor the sole owner of institutional infrastructure.

---

# 20. Instructions for AI coding assistants (Claude, ChatGPT, Gemini or equivalent)

This section is intended to be supplied alongside the entire document to any AI assistant participating in discovery, design, coding, testing or review.

## 20.1 Authority and working method

1. Treat this PRD/SRS as the baseline source of truth.
2. Do not assume that the reference prototype's visual controls are functional backend features.
3. Inspect the current repository, existing architecture, package versions, routes, components, schemas and tests before proposing changes.
4. Do not overwrite existing work or perform large refactors before understanding dependencies.
5. Maintain a requirements traceability matrix mapping each requirement ID to UI, API, database, tests and status.
6. If a requirement conflicts with the existing codebase, explain the conflict and propose options; do not silently ignore the requirement.
7. Identify missing decisions and ask focused questions. Never invent SIES policy, data, facts or credentials.
8. Keep a decision log and update the PRD only through explicit approved change.
9. Prefer incremental, testable implementation over a giant one-shot code generation.
10. For every implementation task, state assumptions, impacted modules, migration implications, security implications and tests.

## 20.2 Mandatory verification while brainstorming

For every proposed feature or architecture:
- Check whether it duplicates an existing module.
- Check all roles and scopes that can access it.
- Check public/private data exposure.
- Check ownership, consent, moderation and approval workflow.
- Check failure, retry, concurrency and rollback paths.
- Check audit and notification requirements.
- Check mobile/accessibility behaviour.
- Check data migration and historical compatibility.
- Check operational cost and ongoing maintenance.
- Identify abuse cases and threat scenarios.
- Distinguish facts from assumptions and recommendations.

Do not claim “secure”, “scalable”, “compliant”, “production-ready” or “best practice” without specifying the evidence, tests or controls supporting the claim.

## 20.3 Coding rules

- Use the repository's agreed stack and pinned, supported dependency versions.
- Prefer TypeScript strict mode where feasible.
- Keep business logic out of UI components and route handlers.
- Validate all inputs on the server.
- Enforce RBAC and scope checks on every protected endpoint.
- Use database transactions for multi-record state changes.
- Use idempotency for payments, webhooks, event registrations and retryable jobs.
- Never trust frontend role, user ID, price, payment status, institution scope or verification status.
- Do not hard-code credentials, secrets, privileged user passwords, personal data or environment-specific URLs.
- Do not add a hidden backdoor or universal login.
- Do not log passwords, tokens, OTPs, private evidence, full payment payloads or unnecessary PII.
- Use migrations; do not rely on ad hoc production schema changes.
- Add tests for both authorised and unauthorised access.
- Keep dependencies maintained and run vulnerability scans.
- Use safe file upload processing and private object storage.
- Do not expose private storage URLs or permanent access tokens.
- Document any deviation from this PRD.

## 20.4 Security review prompts

Before marking a feature complete, explicitly test:
- Can a user change an ID in the URL/API and read another user's record (IDOR)?
- Can an Admin assign themselves Superadmin?
- Does a revoked user retain access through an old session/token?
- Can a Teacher access admin APIs by calling them directly?
- Can an institution coordinator access another institution's records?
- Can an anonymous visitor obtain email/mobile through search, page source, API, export or logs?
- Can a user upload a script, HTML, polyglot or malicious image?
- Can a fake payment callback mark an order paid?
- Can repeated webhooks create duplicate receipts?
- Can a user register multiple times or exceed event capacity under concurrency?
- Can an unapproved memory/job/community post become public?
- Can the platform operator access production personal data without an approved grant?
- Can the platform operator impersonate an SIES Superadmin without a visible audit event?
- Can an administrator erase or modify audit records?
- Can a backup be accessed with production application credentials?

## 20.5 Output expected from AI during each task

For each feature/task, provide:
1. Requirement IDs addressed.
2. Current-state findings from actual repository inspection.
3. Proposed implementation and files/modules affected.
4. Data model/API changes.
5. Permission and privacy analysis.
6. Edge cases and failure modes.
7. Full code changes (not partial snippets when asked to implement).
8. Tests added and exact test results.
9. Migration/deployment steps and rollback.
10. Remaining gaps and decisions.

AI must not report tests as passed unless they were actually executed and results observed. If execution is unavailable, label tests as “not run”.

## 20.6 Final instruction to the AI assistant

Act as a senior product architect, security engineer, UX reviewer and implementation lead. Think end-to-end. Challenge weak assumptions respectfully. Verify every material claim against the code, official SIES-approved material or reliable technical documentation. Do not fabricate requirements, facts, test results or security guarantees. Preserve the client's original intent while making the product coherent, maintainable, secure and usable. Treat this document as a baseline specification, not permission to invent institutional policy.

---

# 21. Change control

Every proposed change after approval must include:
- Change ID and date.
- Requester and approver.
- Requirement(s) affected.
- Reason/business value.
- Scope, cost, schedule and risk impact.
- Data migration and backward compatibility.
- Security/privacy impact.
- Acceptance criteria and test updates.
- Approval status.

No AI assistant, developer or vendor may silently change a P0 requirement or SIES policy.

---

# 22. Initial requirement traceability index

| ID | Requirement area | Priority |
|---|---|---|
| AUTH-001 | Registration, login, reset, MFA and session controls | P0 |
| IAM-001 | RBAC, scopes, role assignment/revocation | P0 |
| IAM-002 | Separate platform-owner control plane | P0 |
| AUD-001 | Immutable attributable audit events | P0 |
| ALUM-001 | Alumni registration and profile | P0 |
| ALUM-002 | Alumni verification workflow | P0 |
| PRIV-001 | Consent and directory visibility | P0 |
| DIR-001 | Alumni search and connection requests | P0 |
| INST-001 | Institution/campus/programme/batch master data | P0 |
| CMS-001 | Managed public content and approvals | P0 |
| SEC-001 | Secure file uploads and private evidence | P0 |
| HELP-001 | Secretariat inquiry workflow | P1 |
| MEM-001 | Memory Chest archives and provenance | P1 |
| MEM-002 | Memory submission and moderation | P1 |
| AWARD-001 | Leadership, distinguished alumni and award showcases | P1 |
| COMM-001 | Communities and moderation | P1 |
| CAREER-001 | Career opportunities and approval | P1 |
| CAREER-002 | Consent-based recruiter/talent access | P1 |
| EVT-001 | Events, registrations and attendance | P1 |
| EVT-002 | Batch reunion requests | P1 |
| GIVE-001 | Funds and wishlist management | P1 |
| PAY-001 | Verified payment, receipts and reconciliation | P1, gated |
| NOTIF-001 | Notification service and preferences | P0 |
| RPT-001 | Role-controlled reports and exports | P1 |
| PRIV-002 | Privacy requests and retention workflow | P0 |
| OPS-001 | Monitoring, backup, restore and incident response | P0 |
| QA-001 | Automated, security, accessibility and UAT testing | P0 |

---

## Appendix A — Public reference pages reviewed

The following URLs were discoverable through the reference portal's navigation on 2 November 2026:

- Home: https://sies-alumni-portal.pages.dev/
- Home / institutional and Secretariat content: https://sies-alumni-portal.pages.dev/home
- Find an Alumni: https://sies-alumni-portal.pages.dev/reconnect
- From Alumni to Stewards: https://sies-alumni-portal.pages.dev/council
- Our Shining Stars: https://sies-alumni-portal.pages.dev/distinguished-alumni
- Our Nine Jewels: https://sies-alumni-portal.pages.dev/nine-jewels
- Memory Chest / Unforgettable Mentors: https://sies-alumni-portal.pages.dev/relive
- Familiar Faces (Staff Members): https://sies-alumni-portal.pages.dev/relive?tab=staff
- Share Your Memories: https://sies-alumni-portal.pages.dev/relive/share
- Distinguished Visitors / Our Pride: https://sies-alumni-portal.pages.dev/our-pride
- Give Back: https://sies-alumni-portal.pages.dev/contribute?tab=corpus
- Community: https://sies-alumni-portal.pages.dev/communities
- Career Opportunities: https://sies-alumni-portal.pages.dev/careers
- Alumnite 2027: https://sies-alumni-portal.pages.dev/participate/alumnite-2027
- Participate / Events: https://sies-alumni-portal.pages.dev/participate

The pages above were reviewed as rendered public references. The review does not certify the accuracy of their displayed names, facts, dates, quotes, imagery, contact details or functionality.

## Appendix B — Sign-off

| Role | Name | Approval / Date |
|---|---|---|
| SIES Product Owner | To be nominated | Pending |
| SIES Alumni Secretariat | To be nominated | Pending |
| SIES IT / Security | To be nominated | Pending |
| SIES Finance | To be nominated | Pending |
| SIES Legal / Compliance | To be nominated | Pending |
| Implementation Partner | To be nominated | Pending |

**End of document.**