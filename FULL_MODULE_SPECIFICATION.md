Full Module Specification

System Title
Vinzons Pilot Elementary School — Student Information Management System (VPES SIMS)

General Purpose
The system is designed to support the Vinzons Pilot Elementary School in managing student enrollment, academic records, scheduling, document submission, teacher assignments, and administrative operations. It provides a centralized digital platform for administrators, teachers, and students to efficiently manage school processes from application to graduation.

---

I. MODULE OVERVIEW

The proposed system is composed of the following major modules:

1. User Account and Access Management Module
2. Landing Page and Public Information Module
3. Student Application and Enrollment Module
4. Student Dashboard Module
5. Document Management Module
6. Student Records Management Module
7. Section Management Module
8. Schedule Management Module
9. Subject Management Module
10. Teacher Management Module
11. Teacher Assignment Module
12. Grades Management Module
13. Re-Enrollment Management Module
14. Promotion and Graduation Module
15. Admin Dashboard Module
16. Teacher Dashboard Module
17. Settings and School Year Management Module
18. Email Notification Module

---

II. DETAILED MODULE SPECIFICATIONS

---

### 1. User Account and Access Management Module

**Purpose:**
This module controls user authentication, authorization, and access levels based on roles within the school management system (Administrator, Teacher, Student/Applicant).

**Features:**
- User login and logout
- Role-based access control (Admin, Teacher, Applicant)
- Account registration with email verification
- Password reset functionality
- Firebase Authentication integration
- Automatic redirect based on user role after login
- Session management and token validation
- Unverified account cleanup

**Inputs:**
- Email address
- Password
- Full name
- Role assignment (admin / teacher / applicant)
- Firebase authentication token
- Email verification status

**Outputs:**
- Authenticated user session
- Login confirmation
- Role-based access permissions
- Unverified account removal notice
- Password reset email

**Business Rules:**
- Only verified email accounts may log in to the system.
- Admin accounts can only be created by existing administrators.
- Teacher accounts are created by the administrator with a generated staff account.
- Students/applicants register independently and are assigned the applicant role by default.
- Passwords are managed by Firebase Authentication and stored in encrypted form.
- Inactive or unverified accounts are automatically removed after a set period.

**School Workflow:**
- Applicants register through the landing page or login page.
- Administrator creates teacher accounts via the Teacher Management module.
- Upon login, users are redirected to their respective dashboard based on their assigned role.
- Administrators manage and monitor all user accounts through the User Management module.

**ISO 25010 Alignment:**
- Functional suitability: ensures correct access to allowed system functions per role
- Security: protects accounts, sessions, and user credentials
- Usability: role-specific interfaces reduce confusion for each user type
- Maintainability: centralized user and permission management

**Screenshots Required:**
| # | What to Screenshot | Where / What to Show |
|---|---|---|
| 1 | Login page — full view | `login.html` — email & password fields, Login button visible |
| 2 | Registration form | `login.html` — Sign Up tab open, all registration fields visible |
| 3 | Email verification notice | After registering — the notice/message shown to verify email |
| 4 | Login error message | Enter wrong credentials — show the error alert/message |
| 5 | Successful login redirect | After login — show the dashboard it redirects to (admin/teacher/student) |

---

### 2. Landing Page and Public Information Module

**Purpose:**
This module provides the public-facing entry point of the system, displaying school information, live enrollment statistics, announcements, and school year details to prospective applicants and visitors.

**Features:**
- Hero carousel with school photos and school name
- Live statistics display (enrolled students, teachers, grade levels, active school year)
- Enrollment status announcement banner (open or closed)
- Grade levels and programs information section
- Document requirements table for applicants
- News and announcements section
- School contact information and location map
- Quick link to enrollment application form

**Inputs:**
- Active school year (from database)
- Enrollment open/close status (from settings)
- Total enrolled students count
- Total teachers count
- Announcements content

**Outputs:**
- Public information page
- Live enrollment stats display
- Enrollment open/closed banner
- Document requirements list

**Business Rules:**
- Enrollment application link is accessible only when enrollment is set to "Open" by the administrator.
- Statistics displayed are pulled live from the database (active SY enrolled count).
- School year displayed reflects the currently active school year in the system settings.
- Document requirements are configurable by the administrator.

**School Workflow:**
- Administrator opens enrollment through the Settings module.
- The landing page enrollment banner automatically updates to "Open."
- Prospective students visit the landing page and click "Enroll Now" to begin application.

**ISO 25010 Alignment:**
- Functional suitability: accurate and complete public-facing information
- Performance efficiency: fast page load with cached statistics
- Usability: clear and accessible layout for parents and students
- Reliability: live stats reflect actual database state

**Screenshots Required:**
| # | What to Screenshot | Where / What to Show |
|---|---|---|
| 1 | Hero section — full view | `index.html` — carousel showing school name, tagline, school year stat cards |
| 2 | Enrollment banner — Open | Top banner showing "Enrollment is Open" status |
| 3 | Enrollment banner — Closed | Top banner showing "Enrollment is Closed" (toggle in settings first) |
| 4 | Programs / Grade Levels section | Section showing Grade 1–6 program info |
| 5 | Document requirements table | Table showing required documents per student type |
| 6 | News/Announcements section | Show any posted announcements |
| 7 | Mobile view (optional) | Resize browser to mobile width — show responsive hero layout |

---

### 3. Student Application and Enrollment Module

**Purpose:**
This module manages the submission and processing of student enrollment applications, including form completion, validation, review, and approval by the administrator.

**Features:**
- Multi-step enrollment application form
- Student type detection (New, Transferee, Balik-aral, Re-enrollee)
- LRN (Learner Reference Number) verification for existing students
- Personal information, guardian, address, and previous school data entry
- reCAPTCHA verification to prevent spam submissions
- Application status tracking (Pending, Approved, Rejected)
- Admin review and approval/rejection with remarks
- Printable enrollment form generation
- Application logs and activity history

**Inputs:**
- Student type
- LRN (if existing student)
- Personal information (full name, birth date, sex, religion, etc.)
- Guardian information (name, relationship, contact, occupation)
- Home address (barangay, municipality, province, zip code)
- Previous school information (name, address, grade completed)
- Supporting documents
- Admin remarks (on approval/rejection)

**Outputs:**
- Submitted application record
- Application status notification
- Printable enrollment confirmation form
- Application list for admin review
- Application history log

**Business Rules:**
- Applications can only be submitted when enrollment is open.
- Each applicant may only have one active application per school year.
- LRN is validated against existing student records before proceeding.
- Incomplete applications cannot be submitted.
- Only administrators can approve or reject applications.
- Approved applicants are automatically tagged as enrolled students.

**School Workflow:**
- Applicant fills out the enrollment form online.
- Application is submitted and placed in Pending status.
- Administrator reviews applications in the Applications Management module.
- Administrator approves or rejects with optional remarks.
- Approved applicants are notified and gain access to the student dashboard.

**ISO 25010 Alignment:**
- Functional suitability: complete and accurate enrollment application process
- Usability: step-by-step multi-form layout guides applicants clearly
- Security: reCAPTCHA prevents automated spam submissions
- Reliability: application data is preserved even if submitted partially

**Screenshots Required:**
| # | What to Screenshot | Where / What to Show |
|---|---|---|
| 1 | Student type selection | `applicationform.html` — Step 1: New / Transferee / Balik-aral options |
| 2 | Personal information form | Step 2 — full personal info fields (name, birthdate, sex, etc.) |
| 3 | Guardian information form | Step 3 — guardian name, relationship, contact fields |
| 4 | Address form | Step 4 — home address fields with zip code |
| 5 | Previous school form | Step 5 — previous school info (visible for Transferee type) |
| 6 | Validation error message | Leave a required field blank, show the error highlight/message |
| 7 | Submission success | After submitting — show the success confirmation screen/message |

---

### 4. Student Dashboard Module

**Purpose:**
This module provides the student-facing interface after login, displaying relevant information and tools based on the student's current enrollment status.

**Features:**
- Three dashboard modes: Applicant, Enrolled, Graduated
- Application status tracking (Applicant mode)
- Section information, grade average, and today's schedule (Enrolled mode)
- Final grades and graduation year display (Graduated mode)
- Class schedule timetable view
- Grade history per quarter and school year
- Document requirements and upload access
- Re-enrollment form submission
- LRN linking modal for existing students
- Profile and account settings

**Inputs:**
- Student enrollment status (Applicant / Enrolled / Graduated)
- Section assignment
- Grades data per subject and quarter
- Class schedule entries
- Document submission status
- Re-enrollment confirmation data

**Outputs:**
- Dashboard home view (mode-specific)
- Class schedule timetable
- Grades table with quarterly breakdown
- Document status list
- Re-enrollment confirmation form
- Graduation summary card (Graduated mode)

**Business Rules:**
- Dashboard mode is automatically determined based on the student's enrollment status in the active school year.
- A graduated student retains access to view final grades only.
- Re-enrollment option is hidden for Grade 6 students.
- Students may only view their own records and documents.
- Grades are read-only for students; only teachers may modify them.

**School Workflow:**
- Student logs in and is directed to the appropriate dashboard mode.
- Applicants track application status and upload required documents.
- Enrolled students view their section, schedule, grades, and re-enrollment form.
- Graduated students view their completion summary and final grades.

**ISO 25010 Alignment:**
- Functional suitability: displays correct data per enrollment status
- Usability: clear, role-specific layout minimizes confusion
- Security: students can only access their own data
- Reliability: dashboard correctly reflects latest enrollment and grade records

**Screenshots Required:**
| # | What to Screenshot | Where / What to Show |
|---|---|---|
| 1 | Applicant mode — home | `studentDashboard.html` (logged in as applicant) — application status card |
| 2 | Applicant mode — documents tab | Document requirements list with upload status per document |
| 3 | Enrolled mode — home | Welcome banner, section info, grade average, today's schedule |
| 4 | Enrolled mode — My Section tab | Section name, adviser, classmates list |
| 5 | Enrolled mode — My Grades tab | Grades table per subject with quarterly breakdown |
| 6 | Enrolled mode — Class Schedule tab | Full weekly timetable view |
| 7 | Enrolled mode — Re-Enrollment tab | Re-enrollment confirmation form |
| 8 | Graduated mode — home | Graduation banner, final average, graduation year, status card |
| 9 | Graduated mode — Final Grades tab | Full grade table with "GRADUATED" badge |

---

### 5. Document Management Module

**Purpose:**
This module manages the submission, review, and verification of student enrollment documents required by the school.

**Features:**
- Student document upload (PDF, image formats)
- Document requirements configuration per student type and grade level
- Document status tracking (Pending, Verified, Rejected)
- Admin verification and rejection of uploaded documents
- In-browser document preview
- Secure document download
- Document submission slot booking
- Appointment slip generation
- Email notification on document status change

**Inputs:**
- Uploaded document file (PDF, JPG, PNG)
- Document type (Birth Certificate, Report Card, etc.)
- Student ID reference
- Admin verification remarks
- Appointment slot selection

**Outputs:**
- Document submission record
- Verification status update
- In-browser document preview
- Downloadable document file
- Appointment slip (printable)
- Email notification to student

**Business Rules:**
- Only accepted file types (PDF, JPG, PNG) may be uploaded.
- Each document type per student may only have one active submission.
- Documents must be verified by an administrator before the application is fully processed.
- Students may only view and download their own documents.
- Administrators may view, verify, reject, and download all documents.
- Document slots limit the number of students per submission schedule.

**School Workflow:**
- Student uploads required documents through the student dashboard.
- Administrator reviews uploaded documents in the Documents module.
- Administrator marks documents as Verified or Rejected with remarks.
- Student is notified via email of the document status.
- Student books an appointment slot for physical document submission if required.

**ISO 25010 Alignment:**
- Functional suitability: complete document submission and verification workflow
- Security: file access is restricted by ownership; secure download endpoints
- Usability: clear document status indicators for students and admin
- Reliability: uploaded files are preserved and retrievable at any time

**Screenshots Required:**
| # | What to Screenshot | Where / What to Show |
|---|---|---|
| 1 | Document upload page (student side) | `uploadDocument.html` — file upload form with document type selector |
| 2 | Uploaded document list (student side) | Student dashboard Documents tab — list of submitted docs with status badges |
| 3 | Admin documents table | `documents.html` — all submitted documents table (student name, type, status) |
| 4 | Filter by status | Admin view — filter dropdown showing Pending/Verified/Rejected options |
| 5 | In-browser document preview | Click Preview on a document — show the preview modal/window |
| 6 | Verify document action | Admin clicking Verify — show the confirmation or updated status |
| 7 | Reject document action | Admin clicking Reject — show the rejection with remarks modal |
| 8 | Document slots management | `documentSlots.html` — appointment slot schedule table |
| 9 | Appointment slip (optional) | Generated printable appointment slip for a student |

---

### 6. Student Records Management Module

**Purpose:**
This module manages the official student master records including personal information, LRN, enrollment history, section assignments, and academic standing.

**Features:**
- Student records list with search and filters
- Individual student detail view
- LRN verification and update
- Manual student creation by admin
- Bulk student import via CSV
- Section assignment and reassignment
- Auto-assign students to sections
- Enrollment history tracking
- Student account linking to Firebase user

**Inputs:**
- Student personal information
- LRN (Learner Reference Number)
- Grade level
- Section assignment
- CSV file (for bulk import)
- Firebase UID (for account linking)

**Outputs:**
- Student master record
- Enrollment history
- Section assignment record
- LRN verification result
- Bulk import summary report
- Student list filtered by grade/section/status

**Business Rules:**
- Each student must have a unique LRN in the system.
- A student may only be assigned to one section per school year.
- CSV imports are validated for required fields before processing.
- Only administrators may create, update, or delete student records.
- Linking a student record to a Firebase account enables student dashboard access.

**School Workflow:**
- Administrator adds students manually or imports via CSV.
- Students are assigned to sections after enrollment approval.
- LRN is verified and linked to the student's Firebase account.
- Student record is updated each school year through the promotion process.

**ISO 25010 Alignment:**
- Functional suitability: accurate and complete student registry management
- Performance efficiency: fast search and retrieval of student records
- Reliability: preserves integrity of core student data across school years
- Usability: bulk import reduces data entry effort for large student volumes

**Screenshots Required:**
| # | What to Screenshot | Where / What to Show |
|---|---|---|
| 1 | Student records table | `students.html` — full list with search bar, filters, and student rows |
| 2 | Individual student record | Click a student — show full profile (name, LRN, grade, section, status) |
| 3 | Assign to section modal | Click "Assign" — show the section selection modal |
| 4 | CSV import page | `import_students.html` — file upload field and import button |
| 5 | Import result | After CSV import — show the success/error summary |
| 6 | Auto-assign students page | `auto-assign-students.html` — grade level selector and assign button |

---

### 7. Section Management Module

**Purpose:**
This module manages the creation and maintenance of class sections per grade level, including section naming, color coding, adviser assignment, and student capacity.

**Features:**
- Section list per grade level
- Create, edit, and delete sections
- Color coding per section for visual identification
- Adviser teacher assignment
- Student count per section display
- Auto-assign students to sections

**Inputs:**
- Section name
- Grade level
- Adviser (teacher)
- Section color
- Maximum student capacity

**Outputs:**
- Section record
- Section list with student counts
- Color-coded section badge
- Students per section list

**Business Rules:**
- Each section must belong to a specific grade level.
- A section name must be unique within its grade level.
- An adviser may only be assigned to one section per school year.
- Sections with enrolled students cannot be deleted.
- Section colors must be unique across all sections.

**School Workflow:**
- Administrator creates sections before the start of the school year.
- Adviser teachers are assigned to sections.
- Students are assigned to sections after enrollment approval.
- Sections are reset each school year during the promotion process.

**ISO 25010 Alignment:**
- Functional suitability: complete section lifecycle management
- Usability: color coding allows quick visual identification of sections
- Reliability: section-student assignments are preserved across operations
- Maintainability: easy section structure updates per school year

**Screenshots Required:**
| # | What to Screenshot | Where / What to Show |
|---|---|---|
| 1 | Sections list | `sections.html` — all sections with grade level, adviser, student count, color badge |
| 2 | Create section modal | Click "Add Section" — show the create section form modal |
| 3 | Edit section modal | Click "Edit" on a section — show the edit form modal |
| 4 | Delete confirmation modal | Click "Delete" — show the confirmation dialog |
| 5 | Color-coded sections | Show sections list with different color badges per section |

---

### 8. Schedule Management Module

**Purpose:**
This module manages the class schedules of each section, assigning subjects, teachers, time slots, and days of the week to produce a complete school timetable.

**Features:**
- Timetable grid builder per section
- Add, edit, and delete schedule entries
- Subject and teacher assignment per time slot
- Teacher conflict detection
- Auto-assign schedule functionality
- Schedule view per teacher
- Student schedule view in dashboard

**Inputs:**
- Section
- Subject
- Teacher
- Day of week
- Start and end time
- School year

**Outputs:**
- Class schedule timetable (per section)
- Teacher's weekly schedule
- Student's class schedule
- Teacher conflict warning

**Business Rules:**
- A teacher cannot be assigned to two different sections at the same time.
- Each subject slot must have an assigned teacher.
- Schedule entries are tied to a specific section and school year.
- Only administrators may create or modify schedules.
- Students and teachers may view but not edit their respective schedules.

**School Workflow:**
- Administrator builds the class schedule per section after sections are created.
- System checks for teacher conflicts during schedule entry.
- Teachers view their assigned schedule in the teacher dashboard.
- Students view their class schedule in the student dashboard.

**ISO 25010 Alignment:**
- Functional suitability: complete schedule creation and conflict detection
- Usability: timetable grid provides clear visual overview of schedules
- Reliability: conflict prevention maintains schedule integrity
- Performance efficiency: schedule data loads quickly per section or teacher

**Screenshots Required:**
| # | What to Screenshot | Where / What to Show |
|---|---|---|
| 1 | Schedule management page | `schedule_management.html` — section dropdown selector and empty/filled timetable grid |
| 2 | Add schedule entry modal | Click a time slot — show the modal with subject, teacher, day, time fields |
| 3 | Filled timetable grid | Show a complete schedule for one section with all time slots filled |
| 4 | Teacher conflict warning | Assign same teacher to overlapping time — show the conflict alert |
| 5 | Teacher's schedule view | `teacher_schedule.html` — teacher's own weekly timetable |

---

### 9. Subject Management Module

**Purpose:**
This module manages the official list of subjects offered per grade level in the school.

**Features:**
- Subject list per grade level
- Add, edit, and delete subjects
- Subject color coding
- Subject assignment to sections

**Inputs:**
- Subject name
- Grade level
- Subject color
- Units or credit hours

**Outputs:**
- Subject record
- Subject list by grade level
- Color-coded subject labels

**Business Rules:**
- Subject names must be unique per grade level.
- Subjects assigned to active schedules or grade entries cannot be deleted.
- Only administrators may manage subjects.
- Subject colors are used consistently across schedules and grade tables.

**School Workflow:**
- Administrator sets up subjects per grade level at the start of the school year.
- Subjects are selected when building class schedules.
- Subjects appear in grade entry forms for teachers.

**ISO 25010 Alignment:**
- Functional suitability: complete subject catalog management
- Usability: color coding provides quick visual identification in schedules
- Maintainability: centralized subject list simplifies updates across modules

**Screenshots Required:**
| # | What to Screenshot | Where / What to Show |
|---|---|---|
| 1 | Subject list table | `subjectManagement.html` — all subjects with grade level and color |
| 2 | Add subject modal | Click "Add Subject" — show the add form modal |
| 3 | Edit subject modal | Click "Edit" on a subject — show the edit form modal |
| 4 | Delete confirmation | Click "Delete" — show the confirmation dialog |

---

### 10. Teacher Management Module

**Purpose:**
This module manages teacher records, including personal information, account creation, and status monitoring.

**Features:**
- Teacher records list
- Add, edit, and view teacher profiles
- Admin-created teacher accounts (Firebase + database)
- Teacher status management (active/inactive)
- Teacher list for assignment selection

**Inputs:**
- Teacher full name
- Employee ID
- Contact number
- Email address
- Specialization/subject area
- Account credentials

**Outputs:**
- Teacher record
- Firebase teacher account
- Teacher list
- Teacher assignment availability

**Business Rules:**
- Only administrators may create teacher accounts.
- Each teacher must have a unique email address.
- Teacher accounts are created simultaneously in Firebase and the local database.
- Inactive teachers cannot be assigned to sections or schedules.

**School Workflow:**
- Administrator adds a new teacher and creates their login account.
- Teacher receives their account credentials to log in.
- Teacher is then assigned to sections and subjects via the Teacher Assignment module.

**ISO 25010 Alignment:**
- Functional suitability: complete teacher account and profile management
- Security: teacher accounts are created with proper authentication
- Usability: simple teacher management interface for administrators
- Maintainability: centralized teacher records linked to Firebase accounts

**Screenshots Required:**
| # | What to Screenshot | Where / What to Show |
|---|---|---|
| 1 | Teacher list table | `teacherManagement.html` — all teachers with name, email, status |
| 2 | Add teacher form | Click "Add Teacher" — show the add form (name, email, contact, etc.) |
| 3 | Edit teacher modal | Click "Edit" on a teacher — show the edit form |
| 4 | Teacher profile details | Click a teacher — show their full profile view |

---

### 11. Teacher Assignment Module

**Purpose:**
This module manages the assignment of teachers to specific sections and subjects for the active school year.

**Features:**
- Teacher-to-section assignment
- Teacher-to-subject assignment per section
- Conflict and duplicate assignment detection
- Assignment list view
- Assignment removal and update

**Inputs:**
- Teacher
- Section
- Subject
- School year

**Outputs:**
- Teacher assignment record
- Assignment list per section
- Assignment list per teacher
- Conflict warning

**Business Rules:**
- A teacher may be assigned to multiple sections and subjects.
- A subject in a section may only have one assigned teacher.
- Assignments are school-year specific.
- Only administrators may manage teacher assignments.
- Assignments must not conflict with the teacher's existing schedule.

**School Workflow:**
- Administrator assigns teachers to sections and their respective subjects.
- System warns if a conflict is detected.
- Teacher assignment determines which classes appear in the teacher's dashboard.

**ISO 25010 Alignment:**
- Functional suitability: accurate teacher-section-subject assignment management
- Reliability: conflict prevention maintains valid assignment integrity
- Usability: clear assignment list view for quick review and updates

**Screenshots Required:**
| # | What to Screenshot | Where / What to Show |
|---|---|---|
| 1 | Teacher assignment list | `teacherAssignment.html` — list of all teacher → section → subject assignments |
| 2 | Assign teacher modal | Click "Assign" — show modal with teacher, section, subject dropdowns |
| 3 | Conflict/duplicate warning | Assign a teacher already assigned — show the warning alert |
| 4 | Remove assignment | Click "Remove" — show confirmation or updated list after removal |

---

### 12. Grades Management Module

**Purpose:**
This module manages the recording, updating, and viewing of student grades per subject and quarter for each school year.

**Features:**
- Grade entry per subject per student per quarter
- Quarterly grade breakdown (Q1, Q2, Q3, Q4)
- Final grade and grade average computation
- Grade completion status check
- Grade history per school year
- Teacher-restricted grade entry (per assigned section/subject)
- Student read-only grade view
- "GRADUATED" badge for Grade 6 final grades

**Inputs:**
- Student ID
- Subject
- Section
- Quarter (Q1–Q4)
- Grade value (0–100)
- School year

**Outputs:**
- Grade record per subject and quarter
- Final grade per subject
- General average
- Grade table (student and teacher view)
- Grade history by school year
- Grade completion status report

**Business Rules:**
- Only teachers assigned to a subject may enter grades for that subject.
- Grade values must be between 0 and 100.
- Grades below 75 are flagged as "Did Not Meet Expectations."
- Final grades are computed as the average of Q1–Q4.
- General average is the average of all subject final grades.
- Grades are locked after the school year is closed (admin-controlled).
- Students may only view their own grades in read-only mode.

**Grade Scale:**
| Range | Description |
|---|---|
| 90–100 | Outstanding |
| 85–89 | Very Satisfactory |
| 80–84 | Satisfactory |
| 75–79 | Fairly Satisfactory |
| Below 75 | Did Not Meet Expectations |

**School Workflow:**
- Teacher logs in and navigates to the Grade Entry module.
- Teacher selects the section, subject, and quarter.
- Teacher encodes grades for each student.
- System computes final grade and general average automatically.
- Student views grades in read-only mode through the student dashboard.

**ISO 25010 Alignment:**
- Functional suitability: accurate and complete grade recording and computation
- Security: only assigned teachers may modify grades
- Usability: tabular grade entry form reduces input errors
- Reliability: grade history preserved across school years

**Screenshots Required:**
| # | What to Screenshot | Where / What to Show |
|---|---|---|
| 1 | Grade entry page — teacher | `teacher_grades.html` — section/subject selector and grade input table |
| 2 | Grade input table | Show the table with student names and Q1–Q4 input fields |
| 3 | Saved grades confirmation | After saving — show success message or updated grade values |
| 4 | Student grades view (dashboard) | `studentDashboard.html` → My Grades tab — read-only grades table |
| 5 | Final grades — graduated student | Graduated mode → Final Grades tab — show "GRADUATED" badge and grade table |
| 6 | Grade scale reference (optional) | Show a row with grade below 75 flagged as "Did Not Meet Expectations" |

---

### 13. Re-Enrollment Management Module

**Purpose:**
This module manages the re-enrollment confirmation process for currently enrolled students returning for the next school year.

**Features:**
- Student re-enrollment form submission
- Re-enrollment confirmation list for admin
- Filter by grade, section, and status
- Re-enrollment status tracking (Pending, Confirmed)
- Export of re-enrollment confirmations

**Inputs:**
- Student ID
- Confirmation of re-enrollment intent
- Guardian signature or acknowledgment
- School year

**Outputs:**
- Re-enrollment confirmation record
- Confirmation list for admin
- Filtered re-enrollment reports

**Business Rules:**
- Re-enrollment is only available when the administrator has opened the re-enrollment period.
- Only currently enrolled students may submit re-enrollment confirmation.
- Grade 6 students are excluded from re-enrollment (they are for graduation, not re-enrollment).
- Each student may only submit one re-enrollment confirmation per school year.
- Administrators view and manage confirmations in the Re-Enrollment Management module.

**School Workflow:**
- Administrator opens the re-enrollment period in Settings.
- Enrolled students see the re-enrollment form in their dashboard.
- Student submits re-enrollment confirmation.
- Administrator reviews confirmations in the Re-Enrollment Management module.

**ISO 25010 Alignment:**
- Functional suitability: complete re-enrollment confirmation workflow
- Usability: simple one-step form for students
- Reliability: confirmation records preserved and exportable

**Screenshots Required:**
| # | What to Screenshot | Where / What to Show |
|---|---|---|
| 1 | Re-enrollment form (student side) | `studentDashboard.html` → Re-Enrollment tab — show the confirmation form |
| 2 | Re-enrollment management table | `reEnrollmentManagement.html` — list of all re-enrollment confirmations |
| 3 | Filter controls | Show filter dropdown by grade, section, or status |
| 4 | Individual re-enrollment detail | Click a record — show the full re-enrollment detail view |

---

### 14. Promotion and Graduation Module

**Purpose:**
This module manages the end-of-year process of promoting students to the next grade level and graduating Grade 6 students.

**Features:**
- Promotion preview list (students per grade level)
- Promote all students per grade or individually
- Grade 6 graduation list
- Graduate individual or all Grade 6 students
- "Already Graduated" badge for processed students
- Graduation status preserved across school years

**Inputs:**
- Student ID
- Current grade level
- Enrollment status
- School year
- Grades completion confirmation

**Outputs:**
- Updated enrollment status (ENROLLED in next grade)
- GRADUATED status for Grade 6 students
- Promotion summary report
- Graduation confirmation record

**Business Rules:**
- Promotion is only available to students with complete grade records.
- Students are promoted to the next grade level (e.g., Grade 1 → Grade 2).
- Grade 6 students are marked as GRADUATED, not promoted.
- A graduated student retains their record in the system but is removed from active enrollment.
- Promotion and graduation are school-year specific and are performed at year-end.
- Only administrators may execute promotion and graduation.

**School Workflow:**
- Administrator verifies that all grades are complete for the school year.
- Administrator runs promotion for each grade level.
- Grade 6 students are separately graduated through the Graduation process.
- Graduated students' dashboards automatically switch to Graduated mode in the next login.

**ISO 25010 Alignment:**
- Functional suitability: accurate and complete end-of-year academic progression
- Reliability: student records correctly updated and preserved post-promotion
- Usability: batch promotion reduces manual data entry effort
- Maintainability: clear separation of promoted and graduated students

**Screenshots Required:**
| # | What to Screenshot | Where / What to Show |
|---|---|---|
| 1 | Promotion preview list | `settings.html` → Student Management tab — show students to be promoted per grade |
| 2 | Promote all confirmation modal | Click "Promote All" — show the confirmation dialog before executing |
| 3 | Graduation list — Grade 6 | Show Grade 6 students list with "Promote to Graduate" or "Already Graduated" badges |
| 4 | Graduate all confirmation modal | Click "Graduate All" — show the confirmation dialog |
| 5 | Post-graduation result | After graduating — show the updated list with "GRADUATED" badges |

---

### 15. Admin Dashboard Module

**Purpose:**
This module provides the administrator with a real-time overview of key system metrics and quick access to frequently used administrative functions.

**Features:**
- Live stat cards (Enrolled, Pending Applications, Approved, Rejected)
- Recent applications list
- Quick action buttons (Review, Enroll, Manage)
- Navigation to all admin modules

**Inputs:**
- Live enrollment count (from active SY)
- Application status counts
- Recent application records

**Outputs:**
- Dashboard statistics display
- Recent applications list
- Quick action shortcuts

**Business Rules:**
- Enrolled count reflects only students with ENROLLED status in the active school year.
- Pending, Approved, and Rejected counts reflect the current school year applications only.
- Dashboard is accessible only to users with the Admin role.

**School Workflow:**
- Administrator logs in and views the dashboard for a summary of school enrollment status.
- Administrator uses quick action buttons to process pending applications.

**ISO 25010 Alignment:**
- Functional suitability: accurate real-time metrics for decision-making
- Performance efficiency: dashboard statistics load quickly from optimized queries
- Usability: single-screen overview reduces need for navigation

**Screenshots Required:**
| # | What to Screenshot | Where / What to Show |
|---|---|---|
| 1 | Admin dashboard — full view | `adminDashboard.html` — all stat cards visible (Enrolled, Pending, Approved, Rejected) |
| 2 | Recent applications list | Bottom section showing latest applicant names and status |
| 3 | Quick action buttons | Show the quick enroll / review buttons on dashboard |

---

### 16. Teacher Dashboard Module

**Purpose:**
This module provides the teacher-facing interface after login, giving access to assigned classes, student lists, grade entry, schedules, and profile management.

**Features:**
- Home overview with assigned sections and announcements
- My Students — class list per assigned section
- Grade Entry — quarter grade input per subject
- My Schedule — weekly timetable view
- Teacher Settings — profile and password update

**Inputs:**
- Teacher login credentials
- Assigned section and subject data
- Grade entries
- Profile update data

**Outputs:**
- Teacher home dashboard
- Class list per section
- Grade entry form
- Weekly schedule timetable
- Updated teacher profile

**Business Rules:**
- Teachers may only view and grade students in their assigned sections and subjects.
- Teachers may not access admin-only modules (student management, settings, etc.).
- Schedule view shows only the teacher's own assigned schedule.

**School Workflow:**
- Teacher logs in and views their assigned sections and today's schedule.
- Teacher navigates to Grade Entry to input or update student grades.
- Teacher views their class list to monitor students per section.

**ISO 25010 Alignment:**
- Functional suitability: complete teacher workflow within assigned scope
- Security: teachers are restricted to their own data and assigned classes
- Usability: focused dashboard reduces complexity for non-admin users

**Screenshots Required:**
| # | What to Screenshot | Where / What to Show |
|---|---|---|
| 1 | Teacher dashboard — home | `teacherDashboard.html` — home section with assigned sections and announcements |
| 2 | My Students page | `teacher_students.html` — student list per assigned section |
| 3 | My Schedule page | `teacher_schedule.html` — teacher's own weekly timetable |
| 4 | Grade entry page | `teacher_grades.html` — grade input table per subject and quarter |
| 5 | Grade save confirmation | After saving grades — show the success message |
| 6 | Teacher settings page | `teacher_settings.html` — profile update form |

---

### 17. Settings and School Year Management Module

**Purpose:**
This module allows administrators to manage school year records, enrollment periods, re-enrollment periods, and system-wide configurations.

**Features:**
- School year history table (past, active, future)
- Create new school year
- Edit school year details (start/end dates)
- Activate school year
- Open and close enrollment period
- Open and close re-enrollment period
- System configuration settings

**Inputs:**
- School year name (e.g., 2026-2027)
- Start and end dates
- Enrollment open/close toggle
- Re-enrollment open/close toggle
- Active school year selection

**Outputs:**
- School year record
- Active SY indicator
- Enrollment status (open/closed)
- Re-enrollment status (open/closed)
- Settings update confirmation

**Business Rules:**
- Only one school year may be active at a time.
- Past school years cannot be re-activated once a newer SY is active.
- Enrollment can only be opened when a school year is active.
- Editing is only available for the current active school year or a future SY.
- Closing enrollment prevents new applications from being submitted.

**School Workflow:**
- Administrator creates the school year for the upcoming academic period.
- Administrator activates the new school year.
- Administrator opens enrollment to accept new applications.
- Administrator opens re-enrollment for returning students.
- At year-end, administrator closes enrollment and proceeds with promotion/graduation.

**ISO 25010 Alignment:**
- Functional suitability: complete school year lifecycle management
- Reliability: single active SY prevents data conflicts across years
- Usability: clear toggle controls for enrollment and re-enrollment periods
- Maintainability: centralized settings reduce scattered configuration risks

**Screenshots Required:**
| # | What to Screenshot | Where / What to Show |
|---|---|---|
| 1 | Settings page — School Year tab | `settings.html` — school year history table with active, past, and future SYs |
| 2 | Create new SY modal | Click "Add School Year" — show the create SY form modal |
| 3 | Edit SY modal | Click "Edit" on active SY — show the edit form |
| 4 | Activate SY confirmation | Click "Activate" on a future SY — show the confirmation dialog |
| 5 | Enrollment toggle — Open | Show the "Open Enrollment" toggle switched ON |
| 6 | Enrollment toggle — Closed | Show the "Close Enrollment" toggle switched OFF |
| 7 | Re-enrollment toggle | Show the re-enrollment open/close toggle |
| 8 | Student Management tab | Show the Promote and Graduate sections under this tab |

---

### 18. Email Notification Module

**Purpose:**
This module manages the automated sending of email notifications to students and guardians for application status updates, document verification results, and other system events.

**Features:**
- Email queue system for background email processing
- Application status email notifications (Approved, Rejected)
- Document verification status email notifications
- Windows Task Scheduler integration for automated processing
- Manual email queue trigger by administrator

**Inputs:**
- Recipient email address
- Notification type (application status, document status)
- Status value (Approved, Rejected, Verified)
- Student name and application reference

**Outputs:**
- Email notification sent to student/guardian
- Email queue log
- Delivery status record

**Business Rules:**
- Emails are queued and processed asynchronously to avoid blocking user operations.
- Email notifications are triggered automatically on status changes.
- Undelivered emails are retried based on the queue schedule.
- Only system-generated emails are sent; no manual email composition is supported.

**School Workflow:**
- Administrator updates application or document status.
- System adds an email notification to the queue.
- Windows Task Scheduler (or cron job) runs the queue processor at regular intervals.
- Student or guardian receives the email notification with status details.

**ISO 25010 Alignment:**
- Functional suitability: automated notification delivery without manual effort
- Reliability: queue-based system ensures emails are not lost on failure
- Performance efficiency: background processing prevents system slowdowns
- Usability: students are kept informed without needing to log in repeatedly

**Screenshots Required:**
| # | What to Screenshot | Where / What to Show |
|---|---|---|
| 1 | Email queue table (database) | phpMyAdmin — `email_queue` table showing queued email records |
| 2 | Sample email received | Open Gmail/inbox — show a received application status or document status email |
| 3 | Windows Task Scheduler | Show the VPES Email Queue scheduled task in Windows Task Scheduler |
| 4 | Manual trigger (optional) | Admin side — show the manual trigger button for the email queue |

---

*Generated: April 19, 2026*
*System: VPES SIMS — Vinzons Pilot Elementary School Student Information Management System*
