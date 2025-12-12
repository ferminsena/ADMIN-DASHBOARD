# VPES-SIMS Architecture

```mermaid
flowchart LR
  subgraph Client["User Browser"]
    UI["HTML/CSS/JS pages<br/>(index, login, dashboards, forms)"]
  end

  subgraph Auth["Authentication"]
    FB["Firebase Auth<br/>(email/password, tokens)"]
  end

  subgraph Backend["PHP API (Apache/XAMPP)"]
    API["REST-like PHP endpoints<br/>(api/login.php, students/, sections/, settings/, documents/, applications/ ...)"]
    Queue["Email Queue<br/>process_queue_cron.php / VPES_Email_Queue_Task.xml"]
    Uploads["File Upload Handlers<br/>api/upload_document_enhanced.php -> /uploads"]
  end

  subgraph Data["MySQL Database"]
    DB[("users, applications, students,\nsections, documents, schedules,\ngrades, system_settings,\ndocument_requirements, email_queue ...")]
  end

  subgraph Storage["Local Storage"]
    Files[/uploads folder<br/>(PDF/JPG/PNG docs)]
  end

  UI -->|HTTP+JWT| API
  UI -->|ID token| FB
  API -->|Verify ID token| FB
  API --> DB
  API --> Uploads --> Files
  API --> Queue
  Queue -->|SMTP| Mail[Outgoing Email]
```

## Notes
- Frontend: static HTML/CSS/JS pages served by Apache; JS calls PHP APIs and uses Firebase Auth for ID tokens.
- Backend: PHP endpoints under `api/` handle enrollment, users, sections, documents, schedules, grades, settings; cron/email queue scripts send notifications.
- Data: MySQL stores users, applications, students, sections, documents, schedules, grades, settings, document requirements, email queue.
- Files: uploaded documents saved under `/uploads` (PDF/JPG/PNG); handled by `upload_document_enhanced.php`.
- Auth flow: browser obtains Firebase ID token; PHP APIs validate token/role before DB or file operations.
