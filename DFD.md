# VPES-SIMS - DATA FLOW DIAGRAM (VISUAL)
**Vinzons Pilot Elementary School - Student Information Management System**

---

## CONTEXT DIAGRAM (Level 0)

### Mermaid Format:
```mermaid
graph TB
    subgraph external["External Entities"]
        AP["👤 Applicant/Parent"]
        ES["👤 Enrolled Student"]
        AD["👤 Admin Staff"]
        T["👤 Teacher"]
        FBA["🔐 Firebase Auth"]
        EMAIL["📧 Email Service"]
    end
    
    subgraph system["VPES-SIMS System (0)"]
        CORE["Core System Engine"]
    end
    
    AP -->|Application Form Data| CORE
    AP -->|Personal/Guardian Info| CORE
    AP -->|Documents Upload| CORE
    CORE -->|Application Status| AP
    CORE -->|Notifications| AP
    
    ES -->|Login Credentials| CORE
    ES -->|Profile Updates| CORE
    CORE -->|Grade Reports| ES
    CORE -->|Schedule Info| ES
    CORE -->|Dashboard Data| ES
    
    AD -->|Review Actions| CORE
    AD -->|Approvals/Rejections| CORE
    AD -->|Student Enrollment| CORE
    CORE -->|Application Lists| AD
    CORE -->|Reports| AD
    CORE -->|System Stats| AD
    
    T -->|Grade Entry| CORE
    T -->|Attendance Records| CORE
    CORE -->|Class Lists| T
    CORE -->|Dashboard Data| T
    
    CORE -->|Auth Requests| FBA
    FBA -->|Auth Response| CORE
    
    CORE -->|Send Email| EMAIL
```

---

## LEVEL 1 DFD - Main Processes

### Mermaid Format:
```mermaid
graph TB
    subgraph external["External Entities"]
        AP["👤 Applicant/Parent"]
        ES["👤 Enrolled Student"]
        AD["👤 Admin Staff"]
        T["👤 Teacher"]
        FBA["🔐 Firebase"]
        EMAIL["📧 Email"]
    end
    
    subgraph processes["Level 1 Processes"]
        P1["<b>1.0</b><br/>Authentication<br/>& Access"]
        P2["<b>2.0</b><br/>Application<br/>Management"]
        P3["<b>3.0</b><br/>Student<br/>Management"]
        P4["<b>4.0</b><br/>Academic<br/>Management"]
        P5["<b>5.0</b><br/>System<br/>Administration"]
    end
    
    subgraph datastores["Data Stores"]
        D1["📊 Users"]
        D2["📊 Applications"]
        D3["📊 Students"]
        D4["📊 Grades"]
        D5["📊 Documents"]
        D6["📊 Sections"]
    end
    
    AP -->|Credentials| P1
    AP -->|Application Data| P2
    ES -->|Credentials| P1
    ES -->|Updates| P3
    AD -->|Commands| P5
    T -->|Grade Data| P4
    
    P1 -->|Auth Request| FBA
    FBA -->|Auth Result| P1
    P1 -->|User Info| D1
    
    P2 -->|Store Application| D2
    P2 -->|Store Documents| D5
    D2 -->|Application Data| P5
    D5 -->|Document Info| P5
    
    P3 -->|Student Data| D3
    D3 -->|Student Info| P4
    D3 -->|Student Info| P3
    
    P4 -->|Grade Data| D4
    D4 -->|Grades| P3
    
    P5 -->|Update Section| D6
    D6 -->|Section Info| P3
    D6 -->|Section Info| P4
    
    P1 -->|Notifications| EMAIL
    P2 -->|Status Updates| EMAIL
    P3 -->|Alerts| EMAIL
```

---

## LEVEL 2 DFD - Detailed Processes

### 1.0 Authentication & Access Control

```mermaid
graph TB
    subgraph input["Input"]
        USER["👤 User Login Request"]
    end
    
    subgraph processes["Processes"]
        P1A["1.1<br/>Validate Credentials"]
        P1B["1.2<br/>Firebase Authentication"]
        P1C["1.3<br/>Check User Role"]
        P1D["1.4<br/>Create Session"]
    end
    
    subgraph stores["Data Stores"]
        D1["📊 Users Table"]
        D2["🔐 Firebase"]
    end
    
    subgraph output["Output"]
        AUTH["✅ Auth Token"]
        ROLE["👤 Role Info"]
        REDIRECT["🔗 Redirect to Dashboard"]
    end
    
    USER -->|Email, Password| P1A
    P1A -->|Validate Request| D1
    D1 -->|User Record| P1A
    P1A -->|Pass/Fail| P1B
    P1B -->|Auth Request| D2
    D2 -->|Auth Response| P1B
    P1B -->|Authenticated| P1C
    P1C -->|Check Role| D1
    D1 -->|Role Data| P1C
    P1C -->|Role Confirmed| P1D
    P1D -->|Session Data| D1
    P1D -->|Token| AUTH
    P1D -->|Role| ROLE
    P1D -->|Dashboard URL| REDIRECT
```

### 2.0 Application Management

```mermaid
graph TB
    subgraph input["Input"]
        APPFORM["📝 Application Form"]
        DOCS["📄 Documents"]
        REVIEW["✅ Admin Review"]
    end
    
    subgraph processes["Processes"]
        P2A["2.1<br/>Form Validation"]
        P2B["2.2<br/>Document Upload"]
        P2C["2.3<br/>Application Storage"]
        P2D["2.4<br/>Review Decision"]
        P2E["2.5<br/>Status Update"]
    end
    
    subgraph stores["Data Stores"]
        D1["📊 Applications"]
        D2["📊 Documents"]
        D3["📊 Application Status"]
    end
    
    subgraph output["Output"]
        STATUS["📊 Application Status"]
        NOTIF["📧 Notification"]
        APPROVE["✅ Approval/Rejection"]
    end
    
    APPFORM -->|Form Data| P2A
    P2A -->|Validate| D1
    D1 -->|Application Rules| P2A
    P2A -->|Valid Data| P2C
    DOCS -->|Upload Files| P2B
    P2B -->|Store Documents| D2
    P2C -->|Save Application| D1
    D1 -->|Application ID| P2C
    P2C -->|Application Created| P2E
    REVIEW -->|Review Decision| P2D
    P2D -->|Update Status| D3
    D3 -->|Status Info| P2E
    P2E -->|Status| STATUS
    P2E -->|Send Notification| NOTIF
    P2D -->|Approve/Reject| APPROVE
```

### 3.0 Student Management

```mermaid
graph TB
    subgraph input["Input"]
        LOGIN["🔐 Student Login"]
        UPDATE["✏️ Profile Update"]
        ENROLL["📝 Enrollment"]
    end
    
    subgraph processes["Processes"]
        P3A["3.1<br/>Student Lookup"]
        P3B["3.2<br/>Dashboard Prep"]
        P3C["3.3<br/>Profile Update"]
        P3D["3.4<br/>Enrollment Process"]
    end
    
    subgraph stores["Data Stores"]
        D1["📊 Students"]
        D2["📊 Grades"]
        D3["📊 Sections"]
        D4["📊 Schedule"]
    end
    
    subgraph output["Output"]
        DASH["📊 Dashboard Data"]
        GRADES["📈 Grade Info"]
        SCHED["📅 Schedule"]
    end
    
    LOGIN -->|Student ID| P3A
    P3A -->|Lookup| D1
    D1 -->|Student Record| P3A
    P3A -->|Prepare Data| P3B
    P3B -->|Get Grades| D2
    P3B -->|Get Section| D3
    P3B -->|Get Schedule| D4
    P3B -->|Dashboard| DASH
    D2 -->|Grades| GRADES
    D3 -->|Classmates| SCHED
    D4 -->|Class Times| SCHED
    
    UPDATE -->|New Info| P3C
    P3C -->|Validate| D1
    P3C -->|Update| D1
    
    ENROLL -->|Enrollment Data| P3D
    P3D -->|Add to Student| D1
    P3D -->|Assign Section| D3
```

### 4.0 Academic Management

```mermaid
graph TB
    subgraph input["Input"]
        GRADES["📝 Grade Entry"]
        ATTENDANCE["✅ Attendance"]
        SCHEDULE["📅 Schedule"]
    end
    
    subgraph processes["Processes"]
        P4A["4.1<br/>Grade Validation"]
        P4B["4.2<br/>Attendance Record"]
        P4C["4.3<br/>Schedule Mgmt"]
        P4D["4.4<br/>Report Generation"]
    end
    
    subgraph stores["Data Stores"]
        D1["📊 Grades"]
        D2["📊 Attendance"]
        D3["📊 Schedule"]
        D4["📊 Students"]
    end
    
    subgraph output["Output"]
        REPORT["📈 Grade Report"]
        ATTEND_REPORT["📊 Attendance"]
        TEACHER_VIEW["👨‍🏫 Teacher Dashboard"]
    end
    
    GRADES -->|Grade Data| P4A
    P4A -->|Validate| D1
    P4A -->|Calculate GPA| D1
    D1 -->|Grade Info| P4A
    P4A -->|Store| D1
    P4A -->|Generate| P4D
    
    ATTENDANCE -->|Attendance Data| P4B
    P4B -->|Record| D2
    P4B -->|Summary| ATTEND_REPORT
    
    SCHEDULE -->|Class Times| P4C
    P4C -->|Validate| D3
    P4C -->|Store| D3
    
    P4D -->|Get Grades| D1
    P4D -->|Get Student Info| D4
    P4D -->|Generate| REPORT
    
    D3 -->|Class List| TEACHER_VIEW
    D1 -->|Grades| TEACHER_VIEW
```

### 5.0 System Administration

```mermaid
graph TB
    subgraph input["Input"]
        ADMIN_CMD["⚙️ Admin Commands"]
        CONFIG["⚙️ Configuration"]
        REPORT_REQ["📊 Report Request"]
    end
    
    subgraph processes["Processes"]
        P5A["5.1<br/>User Management"]
        P5B["5.2<br/>Section Mgmt"]
        P5C["5.3<br/>Settings"]
        P5D["5.4<br/>Report Generation"]
    end
    
    subgraph stores["Data Stores"]
        D1["📊 Users"]
        D2["📊 Sections"]
        D3["📊 Settings"]
        D4["📊 Audit Log"]
    end
    
    subgraph output["Output"]
        USER_LIST["👥 User List"]
        SECTION_LIST["📚 Sections"]
        REPORTS["📈 Reports"]
        ADMIN_DASH["📊 Admin Dashboard"]
    end
    
    ADMIN_CMD -->|Create/Update User| P5A
    P5A -->|User Data| D1
    P5A -->|Log Action| D4
    D1 -->|User Info| USER_LIST
    
    ADMIN_CMD -->|Section Commands| P5B
    P5B -->|Section Data| D2
    P5B -->|Log Action| D4
    D2 -->|Section Info| SECTION_LIST
    
    CONFIG -->|System Settings| P5C
    P5C -->|Save Config| D3
    P5C -->|Log Action| D4
    
    REPORT_REQ -->|Query Request| P5D
    P5D -->|Get Data| D1
    P5D -->|Get Data| D2
    P5D -->|Generate| REPORTS
    P5D -->|Dashboard| ADMIN_DASH
```

---

## DATA STORES REFERENCE

| ID | Name | Purpose | Key Fields |
|---|---|---|---|
| D1 | Users | User accounts & credentials | user_id, email, password_hash, role |
| D2 | Applications | Enrollment applications | app_id, applicant_email, status, submitted_date |
| D3 | Students | Enrolled student records | student_id, LRN, full_name, grade_level |
| D4 | Grades | Academic grades | grade_id, student_id, subject, score |
| D5 | Documents | Uploaded documents | doc_id, application_id, document_type, file_path |
| D6 | Sections | Class sections | section_id, grade_level, teacher_id |
| D7 | Schedule | Class schedule | schedule_id, section_id, subject, time_slot |
| D8 | Attendance | Attendance records | attendance_id, student_id, date, present |
| D9 | Settings | System configuration | setting_key, setting_value |
| D10 | Audit Log | Admin action logs | log_id, admin_id, action, timestamp |

---

## DATA FLOWS SUMMARY

### From Applicant/Parent:
- **Application Form Data** → P2.0 (Application Management)
- **Documents** → P2.0 (Application Management)
- **Login Credentials** → P1.0 (Authentication)

### From Enrolled Student:
- **Login Credentials** → P1.0 (Authentication)
- **Profile Updates** → P3.0 (Student Management)

### From Admin:
- **Admin Commands** → P5.0 (System Administration)
- **Review Actions** → P2.0 (Application Management)
- **User Management** → P5.0 (System Administration)

### From Teacher:
- **Grade Entry** → P4.0 (Academic Management)
- **Attendance Records** → P4.0 (Academic Management)

### To External Systems:
- **Authentication Requests** → Firebase Auth Service
- **Email Notifications** → Email Service

---

## SYSTEM FLOWS DIAGRAM

```
APPLICANT → [Application Form] → SYSTEM → [Application Review] → ADMIN
                                    ↓
                            [Document Storage]
                                    ↓
                            [Send Notification] → EMAIL
                                    ↓
                          [Enrollment Decision]
                                    ↓
                              APPROVED ↓ REJECTED
                                    ↓
                            [Create Student] 
                                    ↓
                            [Assign Section]
                                    ↓
                          [Welcome Email] → EMAIL
                                    ↓
                            STUDENT ACCOUNT READY
                                    ↓
STUDENT → [Login] → [View Dashboard] → [Grades, Schedule, Info]
            ↓
      [Firebase Auth] → [Session]
            ↓
      [Access Student Module]
            ↓
      [View Grades, Schedule, Section]

TEACHER → [Login] → [View Classes] → [Enter Grades]
            ↓
      [View Student List]
            ↓
      [Mark Attendance]
            ↓
      [System Updates D4.0]

ADMIN → [Login] → [Admin Dashboard]
          ↓
      [Review Applications] → [Approve/Reject]
          ↓
      [Manage Users] → [Create/Edit/Delete]
          ↓
      [Manage Sections] → [Create Classes]
          ↓
      [View Reports] → [Statistics]
```

---

## TECHNICAL ARCHITECTURE REFERENCE

### Technology Stack:
- **Frontend:** HTML, CSS, JavaScript
- **Backend:** PHP
- **Database:** MySQL
- **Authentication:** Firebase Authentication
- **Server:** Apache (XAMPP)

### Key Tables in System:
```
users → Applications → Documents
        ↓
      Students → Grades
        ↓        ↓
      Sections ← Schedule
        ↓
    Attendance
```

---

**Generated:** December 12, 2025  
**Format:** Mermaid Diagrams + ASCII Flow Diagrams  
**Notation:** Gane-Sarson (adapted for web system)
