# Requirements Backlog: Peer Tutoring Platform for Upper-Division FSU Courses

**LLM used:** Claude (Anthropic)

## 1. Problem Statement

FSU offers many tutoring resources for entry-level courses, but far fewer for upper-division courses. This project explores software that connects upper-division students with peers who can help them succeed in their courses.

## 2. Stakeholders

| Stakeholder | Interest |
|---|---|
| Tutee | An upper-division student seeking help |
| Tutor | A peer who has succeeded in the course |
| Dept/Instructor | Instructors, TAs, and departments who care about quality and academic integrity |
| Admin | The platform operators |
| IT/Privacy | University IT and privacy staff |
| Campus tutoring services | Existing services, treated as partners rather than competitors (added in pass 2) |
| Student organizations | Honor societies and similar groups, a source of tutors (added in pass 2) |

## 3. Tag Key

| Tag | Values |
|---|---|
| **Type** | F = functional; NFR = non-functional or policy |
| **Priority** | MoSCoW: Must, Should, Could |
| **Release** | MVP, R2, R3 |
| **Source** | Stakeholder who needs the requirement |
| **Risk** | What could make the requirement hard or problematic |
| **Origin** | B = pass 1 brainstorm; S = scenario walkthrough; M = misuse case; G = gap analysis (pass 2) |
| **Depends on** | Requirement IDs that must exist first |

Priorities and releases reflect pass 2 revisions where noted (marked with †).

---

## 4. Backlog

### Epic 1: Accounts and Identity

| ID | Requirement | Type | Priority | Release | Source | Risk | Origin | Depends on |
|---|---|---|---|---|---|---|---|---|
| R-01 | As a student, I can sign in with my university credentials (SSO) so that only verified FSU students use the platform. | F | Must | MVP | IT/Privacy | Needs university approval for SSO integration | B | none |
| R-02 | As a user, I can act as a tutee, a tutor, or both. | F | Must | MVP | Tutee, Tutor | Low | B | R-01 |
| R-03 | As a user, I can maintain a profile (major, year, courses of interest). | F | Must | MVP | Tutee | Low | B | R-01 |

### Epic 2: Tutor Onboarding and Trust

| ID | Requirement | Type | Priority | Release | Source | Risk | Origin | Depends on |
|---|---|---|---|---|---|---|---|---|
| R-04 | As a tutor, I can list the courses I can tutor, including the semester taken and grade earned. | F | Must | MVP | Tutor | Low | B | R-02, R-09 |
| R-05 | As a tutor, I can set recurring weekly availability. | F | Must | MVP | Tutor | Time zone and semester-schedule edge cases | B | R-02 |
| R-06 | As a tutor, I must acknowledge a code of conduct and academic integrity policy before tutoring. | F | Must | MVP | Dept/Instructor, Admin | Low | B | R-02 |
| R-07 | As an admin, I can approve or reject tutor applications. | F | Must | MVP | Admin | Admin workload | B | R-04, R-06, R-25 |
| R-08 † | As a tutee, I can see that a tutor's grade claim has been verified through **instructor endorsement (R-28) or a transcript the tutor voluntarily uploads**. | F | Should | R2 | Tutee, Dept/Instructor | Privacy and FERPA concerns; manual effort | B | R-04, R-28, R-30 |
| R-46 | As a new tutor, I complete a short training on how to tutor (explaining, not giving answers) before my first session. | F | Should | R2 | Dept/Instructor, Tutor | Training content has to be created | G | R-06 |

### Epic 3: Discovery and Matching

| ID | Requirement | Type | Priority | Release | Source | Risk | Origin | Depends on |
|---|---|---|---|---|---|---|---|---|
| R-09 | The system maintains a catalog of upper-division courses. | F | Must | MVP | Admin | Keeping it in sync with the registrar | B | none |
| R-10 | As a tutee, I can search for approved tutors by course. | F | Must | MVP | Tutee | Low | B | R-04, R-07, R-09 |
| R-11 | As a tutee, I can filter tutors by availability, modality, rating, and whether they had the same instructor. | F | Should | R2 | Tutee | Low | B | R-05, R-10, R-24 |
| R-12 † | As a tutee, I can post a help request (course and topic) that tutors can respond to. *Consider merging with R-36 into one "demand signal" feature.* | F | Should | R2 | Tutee | Spam or low response | B | R-02, R-09 |
| R-13 | As a tutee, I receive recommended tutors based on course, schedule, and past ratings. | F | Could | R3 | Tutee | Needs enough data | B | R-03, R-10, R-24 |
| R-49 | As a tutee, I can save favorite tutors and rebook them in a few taps. | F | Should | R2 | Tutee | Low | S | R-10, R-14 |

### Epic 4: Scheduling and Sessions

| ID | Requirement | Type | Priority | Release | Source | Risk | Origin | Depends on |
|---|---|---|---|---|---|---|---|---|
| R-14 | As a tutee, I can request a session in a tutor's open time slot. | F | Must | MVP | Tutee | Double-booking | B | R-05, R-10 |
| R-15 | As a tutor, I can accept or decline session requests. | F | Must | MVP | Tutor | Low | B | R-14 |
| R-16 | As a user, I get email or push reminders and confirmations. | F | Must | MVP | Tutee, Tutor | Notification fatigue | B | R-14 |
| R-17 † | As a user, I can choose in-person (with suggested campus locations) or virtual (with a generated video link). *Ships together with R-41 (in-person safety guidance).* | F | Should | R2 | Tutee, Tutor | Third-party video integration | B | R-15 |
| R-18 | As a user, I can cancel or reschedule under a stated policy. | F | Should | R2 | Tutee, Tutor | No-shows | B | R-15 |
| R-19 | As a user, I can sync sessions to Google/Outlook/iCal. | F | Should | R2 | Tutee, Tutor | Low | B | R-15 |
| R-20 | As a tutor, I can host group or exam-review sessions. | F | Could | R3 | Tutor, Tutee | Capacity and room logistics | B | R-15 |
| R-48 | As a tutee, I can add context when requesting a session (topic, assignment type, what I'm stuck on), so the tutor can prepare. | F | Should | MVP | Tutee, Tutor | Low | S | R-14 |

### Epic 5: Communication

| ID | Requirement | Type | Priority | Release | Source | Risk | Origin | Depends on |
|---|---|---|---|---|---|---|---|---|
| R-21 † | As a booked tutee or tutor, I can message the other party in-app, so personal contact info stays private. | F | Should | R2 | Tutee, Tutor, IT/Privacy | Harassment or abuse | B | R-15, R-26, R-42, R-57 |
| R-22 | As a user, I can share files or notes within a session. | F | Could | R3 | Tutee, Tutor | Cheating or misuse; storage | B | R-21, R-34 |

### Epic 6: Feedback and Quality

| ID | Requirement | Type | Priority | Release | Source | Risk | Origin | Depends on |
|---|---|---|---|---|---|---|---|---|
| R-23 | As a tutee, I can rate and review a tutor after a completed session. | F | Must | MVP | Tutee, Admin | Retaliatory or biased reviews | B | R-15 |
| R-24 | As a tutee, I can see a tutor's aggregate rating and session count. | F | Should | R2 | Tutee | Cold start for new tutors | B | R-23 |
| R-43 | As a tutor, I can reply publicly to a review, and admins can review flagged or suspicious reviews (e.g., coordinated fake ratings). | F | Should | R2 | Tutor, Admin | Moderation workload | M | R-23, R-26 |
| R-51 | As a tutee, I answer a short post-session question ("did this help you reach your goal?"), separate from the star rating. | F | Should | R2 | Admin, Dept/Instructor | Survey fatigue | G | R-23 |

### Epic 7: Administration and Insight

| ID | Requirement | Type | Priority | Release | Source | Risk | Origin | Depends on |
|---|---|---|---|---|---|---|---|---|
| R-25 | As an admin, I can manage users, courses, and tutor status in a dashboard. | F | Must | MVP | Admin | Low | B | R-01, R-02 |
| R-26 | As a user, I can report or block another user or session. | F | Must | MVP | Tutee, Tutor, Admin | Needs a moderation process | B | R-02 |
| R-27 | As an admin, I can see analytics such as sessions per course and searches with no available tutors (unmet demand). | F | Should | R2 | Admin, Dept/Instructor | Low | B | R-10, R-14 |
| R-28 † | As an instructor, I can endorse tutors for my course. | F | Should | R2 | Dept/Instructor | Instructor adoption | B | R-07 |
| R-29 | As a tutor, I can log hours for service credit or an incentive program. | F | Could | R3 | Tutor | Depends on a policy decision (volunteer vs. paid) | B | R-15 |

### Epic 8: Launch and Cold Start

| ID | Requirement | Type | Priority | Release | Source | Risk | Origin | Depends on |
|---|---|---|---|---|---|---|---|---|
| R-35 | As an admin, I can enable the platform one course at a time, so we can pilot with a few departments. | F | Must | MVP | Admin | Low | G | R-09, R-25 |
| R-36 | As a tutee, I can join a waitlist for a course with no tutors and get notified when one becomes available. | F | Should | R2 | Tutee | Needs a notification channel | S | R-09, R-10, R-16 |
| R-37 | As a tutee, when no tutor is available, I see links to existing campus tutoring and academic support resources. | F | Should | MVP | Tutee, Admin | Keeping links current | G | R-10 |
| R-38 | As an admin, I can invite likely tutors for a course (via instructor referrals or student-org rosters) with a pre-filled application. | F | Should | R2 | Admin, Dept/Instructor | Privacy of the referral lists | G | R-07, R-09 |

### Epic 9: Integrity and Safety

| ID | Requirement | Type | Priority | Release | Source | Risk | Origin | Depends on |
|---|---|---|---|---|---|---|---|---|
| R-39 | As a user, I see an academic integrity reminder when I book a session and again when it starts. | F | Must | MVP | Dept/Instructor | Users ignoring it | M | R-06, R-14 |
| R-40 | As an instructor, I can post course-specific tutoring guidelines (e.g., "no help on take-home exams") that appear on that course's tutor listings and booking flow. | F | Should | R2 | Dept/Instructor | Instructor adoption | M | R-09, R-39 |
| R-41 | As a user booking an in-person session, I am steered toward public campus locations and can share session details with a trusted contact. | F | Should | R2 | Tutee, Tutor, IT/Privacy | Liability questions | M | R-17 |
| R-42 | As an admin, I can suspend users, users can appeal, and every moderation action is recorded in an audit log. | F | Must | MVP | Admin, IT/Privacy | Needs a defined process and staff | M | R-25, R-26 |
| R-50 | As an admin, I can see no-shows and set booking limits after repeated no-shows by either party. | F | Should | R2 | Tutor, Admin | Fairness of the policy | M | R-18 |

### Epic 10: Tutor Experience

| ID | Requirement | Type | Priority | Release | Source | Risk | Origin | Depends on |
|---|---|---|---|---|---|---|---|---|
| R-44 | As a tutor, I have a dashboard of upcoming sessions, past sessions, and feedback. | F | Should | R2 | Tutor | Low | S | R-15, R-23 |
| R-45 | As a tutor, I can pause my availability or cap weekly hours (e.g., during my own exams), so I don't burn out or get double-booked. | F | Should | R2 | Tutor | Low | S | R-05 |
| R-47 | As a tutor, I can earn recognition (certificate, badge, or a verification letter for a resume). | F | Could | R3 | Tutor | Depends on the incentive policy | S | R-29, R-44 |

### Epic 11: Inclusion and Data Fallbacks

| ID | Requirement | Type | Priority | Release | Source | Risk | Origin | Depends on |
|---|---|---|---|---|---|---|---|---|
| R-52 | As an admin, I can import or update the course catalog from a CSV file if no registrar integration exists. | F | Must | MVP | Admin | Manual upkeep each semester | G | R-09 |
| R-53 | If SSO is unavailable, a user can verify with an @fsu.edu email address. | F | Should | MVP | IT/Privacy | Weaker identity assurance | G | R-01 |
| R-54 | As a tutee, I can filter for accommodations (captioned virtual sessions, accessible meeting locations). | F | Should | R2 | Tutee | Needs tutor data on what they can offer | S | R-11, R-17 |
| R-55 | As a tutor, I can optionally list languages I tutor in. | F | Could | R3 | Tutee, Tutor | Low | S | R-04 |
| R-60 | *Conditional:* if the program is paid, support tutor payment and refunds. | F | Could | R3 | Tutor, Admin | Large scope, legal and tax issues | G | R-29, Open Question 1 |

### Cross-Cutting: Non-Functional and Policy Requirements

| ID | Requirement | Type | Priority | Release | Source | Risk | Origin | Depends on |
|---|---|---|---|---|---|---|---|---|
| R-30 | The system complies with FERPA and university data policies and collects only the minimum data needed. | NFR | Must | MVP | IT/Privacy | Legal review needed | B | applies to all |
| R-31 | The UI meets WCAG 2.1 AA accessibility. | NFR | Must | MVP | Tutee, IT/Privacy | Low | B | applies to all UI |
| R-32 | The UI is usable on mobile browsers. | NFR | Must | MVP | Tutee | Low | B | applies to all UI |
| R-33 | Search returns within about 2 seconds, and the system handles peak load at midterms and finals. | NFR | Should | R2 | Tutee, Admin | Hosting costs | B | R-10, R-14 |
| R-34 † | The terms of use prohibit completing graded work for tutees. Enforcement is implemented through R-39 (reminders), R-40 (course guidelines), R-26 (reports), and R-42 (suspension). | NFR/Policy | Must | MVP | Dept/Instructor | Hard to enforce | B | R-06, R-26, R-39, R-40, R-42 |
| R-56 | Tutors control which profile details are shown, and a tutee's grades and struggles are never visible to other users. | NFR | Must | MVP | IT/Privacy, Tutee | Low | M | R-30 |
| R-57 | Users can delete their accounts. Messages and reports are retained for a defined period for moderation, then purged. | NFR | Must | MVP | IT/Privacy | Legal review of retention period | G | R-21, R-30 |
| R-58 | The system targets high availability during the academic calendar, with load tested before midterms and finals. | NFR | Should | R2 | Admin | Hosting cost | G | R-33 |
| R-59 | The system captures success metrics: sessions completed, repeat bookings, and tutee goal-met rate by course. | NFR | Should | R2 | Admin, Dept/Instructor | Needs consent for any research use | G | R-27, R-51 |

---

## 5. Revision Log (Pass 1 Requirements Changed in Pass 2)

| ID | Change | Reason |
|---|---|---|
| R-08 | Replaced university transcript checks with instructor endorsement or a tutor-uploaded transcript. Dependencies now R-04, R-28, R-30. | University does not release grades, which reduces FERPA risk. |
| R-12 | Noted overlap with R-36; consider merging into one demand-signal feature. | Both capture unmet demand. |
| R-17 | Must ship together with R-41. | In-person sessions need safety guidance. Dependency is listed on R-41 only, to avoid a circular dependency. |
| R-21 | Added dependencies on R-42 and R-57. | Messaging needs moderation and a retention policy first. |
| R-28 | Raised from Could/R3 to Should/R2. | It is now the main trust mechanism. |
| R-34 | Enforcement now implemented through R-39, R-40, R-26, and R-42. | The original statement was not testable by itself. |

## 6. Suggested Build Order

1. **Foundation:** R-01, R-02, R-03, R-09, R-52, R-25, R-35
2. **Tutor pipeline:** R-04, R-05, R-06 then R-07
3. **Core loop:** R-10 then R-14, R-48, R-15, R-16, then R-23
4. **Safety and integrity gate (before any messaging or public launch):** R-26, R-42, R-39, R-56, R-57
5. **Quality and trust (R2):** R-24, R-43, R-28, R-08, then R-11 and R-13
6. **Scale and insight (R2):** R-36, R-38, R-44, R-45, R-27, R-51, R-59, R-33, R-58
7. **Later (R3):** R-20, R-22, R-29, R-47, R-55, R-60

Cross-cutting NFRs (R-30, R-31, R-32) apply throughout.

## 7. Acceptance Criteria for Selected Must-Have Requirements

| ID | Acceptance criteria |
|---|---|
| R-01 | **Given** a user with a valid FSU login, **when** they sign in, **then** they reach their dashboard. **Given** a non-FSU account, **then** access is denied. |
| R-10 | **Given** an approved tutor lists a course, **when** a tutee searches that course, **then** the tutor appears. Unapproved or suspended tutors never appear. |
| R-14 | **Given** a tutor's open slot, **when** a tutee requests it, **then** the slot is held pending acceptance and no second tutee can book it. |
| R-26 | **Given** any session or profile, **when** a user submits a report, **then** an admin sees it in the queue, and the reporter can block the other user immediately. |
| R-39 | **Given** a booking, **when** the tutee confirms, **then** the integrity reminder is displayed and must be acknowledged before the booking is submitted. |
| R-42 | **Given** a suspension, **then** the action, reason, and admin are logged, and the user can submit an appeal that an admin can see. |

## 8. Assumptions

- The platform is limited to FSU students and is free to use.
- Tutors are peers (typically students who earned a B+ or higher), not professional tutors.
- Initial scope is a web app, not native mobile apps.
- **Pilot first:** launch in a few courses and departments (R-35), not the whole university.
- **Tutor model:** volunteer or service credit for the pilot, with payment (R-60) deferred. This is provisional, not decided.
- The platform complements existing campus tutoring and links to it (R-37).
- Grade verification relies on instructor endorsement or student-supplied transcripts, not university-released grades.
