2️⃣ Auto Setup (recommended)
bash
Copy
Edit
python setup.py
Installs dependencies, creates MySQL DB campusconnect, seeds sample data, and generates a default admin.

3️⃣ Manual Setup (alternative)
bash
Copy
Edit
pip install -r requirements.txt           # dependencies
mysql -u root -p < database/campus.sql    # schema + seed
🏃‍♂️ Running the Application
Mode	Command	URL
Development	python app.py	http://localhost:5000
Production	Gunicorn / uWSGI + Nginx reverse proxy	your‑domain.com (SSL)

Environment variables (.env):

ini
Copy
Edit
FLASK_SECRET_KEY=super‑secret‑key
DB_USER=root
DB_PASS=your‑mysql‑password
📁 Project Structure
arduino
Copy
Edit
campus-connect/
├── app.py                # Flask entry‑point
├── setup.py              # 1‑click installer / seeder
├── requirements.txt
├── database/
│   └── campus.sql        # schema + sample data
├── backend/              # service / DAO layers
├── routes/               # Flask blueprints
├── templates/            # Jinja2 HTML files
├── static/
│   ├── css/
│   ├── js/
│   └── images/
├── uploads/              # student docs
└── README.md

🔐 Default Credentials

Role	Email	Password
Admin	admin@campus.com	admin123
Student (sample)	student@campus.com	student123

🎯 Usage Guide
Administrators
Login ➜ Dashboard

Manage Programmes → Courses → Semesters

Approve / reject Student Registrations

Verify Documents & generate PDF reports

View Analytics for quick insights

Students
Sign Up → choose programme & upload docs

Track application on Dashboard

Browse Courses, download syllabus / timetable

Submit Service Requests; receive email alerts*

* future‑scope items marked with *

🔧 Configuration Highlights
Allowed uploads: PDF · JPG/PNG · DOCX

Max file size: configurable in app.py (MAX_CONTENT_LENGTH)

Password hashing: Werkzeug generate_password_hash()

SQL Safety: SQLAlchemy / parameterised queries

📊 Database Schema (core tables)
bash
Copy
Edit
users (
  userid PK,
  email UNIQUE,
  password_hash,
  role ENUM('admin','student')
)

programs  (pid PK, pname, total_sem, description)
courses   (cid PK, cname, duration, description)
enrollments (regno FK→users, pid FK→programs, sem, course_ids)
documents (doc_id PK, regno FK→users, filename, verified BOOL, uploaded_at)
Full DDL in database/campus.sql.

🛡️ Security Features
BCrypt‑strength password hashes

Flask‑Login session protection

CSRF tokens on all forms

Strict MIME / extension check on uploads

Environment‑based config (no secrets in VCS)

🚀 Deployment Checklist
 Gunicorn + Nginx (or Apache mod_wsgi)

 HTTPS via Let’s Encrypt

 Daily MySQL dump cron

 .env secrets in Docker / systemd service

 Fail2Ban / ufw for basic hardening

🤝 Contributing
Fork ➜ feature branch

Code + tests

pre‑commit run --all-files

Pull request 🚀

📝 License
Distributed under the MIT License (LICENSE file).

🆘 Support
Issues tab on GitHub

Email: support@campus‑connect.com

Docs: https://docs.campus‑connect.com


