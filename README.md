# CSL System

CSL System is a bilingual Django application for administering language-tutoring and teaching-practicum programs. It combines eligibility-controlled registration, privacy-aware matching, class scheduling, mutual attendance verification, hour accounting, certificate generation, and administrative review in one auditable workflow.

This repository is the public, privacy-scrubbed open-source edition. It contains no production database, real participant records, credentials, uploaded qualification documents, private institutional material, official logos, or certificate artwork.

> **Status:** Active development. Review the deployment and security settings before operating the application with real personal data.

## Features

- Roster-based registration with role and program eligibility
- Bilingual tutor and student profiles
- Qualification-document review with protected downloads
- Privacy-aware candidate browsing and invitations
- Pairing lifecycle and release requests
- One-time and recurring class scheduling
- Mutual check-in, class records, and confirmation
- Late-entry and exception review workflows
- Semester and program-scoped hour accounting
- Administrative exports and audit history
- Configurable bilingual certificate generation

## Technology

- Python 3.12
- Django 5.2 LTS
- PostgreSQL
- Server-rendered HTML, CSS, and focused JavaScript
- ReportLab and pypdf for optional PDF generation
- openpyxl for spreadsheet exports
- GitHub Actions for linting, tests, dependency auditing, and deployment checks

## Repository Structure

```text
accounts/    Authentication, rosters, profiles, and registration
tutoring/    Matching, classes, records, messages, hours, and reports
templates/   Server-rendered bilingual templates
static/      CSS and JavaScript
config/      Django settings and URL configuration
```

Official branding, proprietary templates, and institution-specific operational documents are intentionally not included. See [NOTICE](NOTICE).

## Local Development

### Prerequisites

- Python 3.12
- PostgreSQL
- Git

### Set up the application

```bash
git clone https://github.com/Karma-1827/CSL-System.git
cd CSL-System
python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install -r requirements-dev.txt
```

Create a PostgreSQL database and user, then export configuration values based on [`.env.example`](.env.example). The application does not automatically load `.env` files.

```bash
export DJANGO_DEBUG=1
export DJANGO_SECRET_KEY='replace-with-a-development-only-secret'
export DJANGO_ALLOWED_HOSTS='localhost,127.0.0.1'
export POSTGRES_DB='csl_system_dev'
export POSTGRES_USER='csl_system_dev'
export POSTGRES_PASSWORD='replace-with-your-local-password'
export POSTGRES_HOST='localhost'
export POSTGRES_PORT='5432'

python manage.py migrate
python manage.py createsuperuser
python manage.py runserver 127.0.0.1:8000
```

Open <http://127.0.0.1:8000/>. The development administration interface is at <http://127.0.0.1:8000/system-admin/>.

## Quality Checks

```bash
ruff check .
python manage.py makemigrations --check --dry-run
python manage.py test --verbosity 1
pip check
pip-audit
```

## Privacy and Security

This application can process identity data, class records, messages, and uploaded documents. Operators are responsible for obtaining a lawful basis, limiting collection and retention, securing storage and transport, restricting administrative access, maintaining backups, and complying with applicable privacy law.

Never commit real participant data, credentials, database dumps, uploaded documents, or production configuration. Please report suspected vulnerabilities privately according to [SECURITY.md](SECURITY.md), rather than opening a public issue.

## Certificate and Branding Assets

Certificate generation is designed for operator-supplied templates and fonts. The public repository does not grant rights to any university name, logo, seal, certificate design, or other third-party asset. Before enabling certificate generation, supply assets that you own or are licensed to redistribute and use.

## Contributing

Contributions are welcome. Keep migrations reviewable, include tests for permission-sensitive changes, use fictional data in tests and examples, and do not submit institutional or participant information.

## License

The source code in this repository is licensed under the [Apache License 2.0](LICENSE), except where a file explicitly states otherwise. Names, logos, trademarks, personal data, and excluded third-party materials are not licensed under Apache-2.0; see [NOTICE](NOTICE).
