# Prefects-Voting-System
Prefects Voting System  A professional, secure Django web application for conducting school prefect elections through a kiosk-based digital voting system. Built for schools that need a transparent, auditable, and easy-to-use platform to replace paper ballots.
# Prefects Voting System

A professional, secure Django web application for conducting school prefect elections through a kiosk-based digital voting system. Built for schools that need a transparent, auditable, and easy-to-use platform to replace paper ballots.

## Overview

The system supports two distinct user roles: **voters** (students and teachers) and **administrators** (election officials). Voters identify themselves using unique personal codes, cast their ballot on a touch-friendly kiosk interface, and immediately receive confirmation before the device is handed to the next voter. Administrators manage candidates, voters, and results through a protected staff dashboard.

## Key Features

- **Code-based authentication** — Each voter receives a unique alphanumeric code (auto-generated or pre-assigned via CSV). Codes are single-use: once a ballot is cast, the code cannot be reused.
- **Gender-grouped ballots** — Candidates are displayed in separate male and female categories. Voters may select up to **5 candidates per gender**, with server-side and client-side enforcement of the selection limit. Abstaining in either category is allowed.
- **Identity confirmation** — After entering a valid code, the voter's name is displayed on screen before they proceed, ensuring they are voting as themselves.
- **CSV import/export** — Bulk import candidates and voters from CSV files. Candidate images can be uploaded individually or in bulk via the management interface. Results are downloadable as a timestamped CSV.
- **Printable voter slips** — Generate and print slips containing each voter's name and code for distribution.
- **Full audit trail** — Every code lookup, successful vote, and failed attempt is logged with IP address and timestamp. Each vote records its cast time and originating IP.
- **Kiosk session tracking** — Each browser session is assigned a unique kiosk identifier, allowing administrators to trace activity across shared devices.

## Technical Stack

- **Backend:** Django 4.2+ (Python 3.10–3.12)
- **Database:** SQLite by default (easily swappable for PostgreSQL)
- **Frontend:** Server-rendered templates with vanilla JavaScript and CSS — no framework dependencies
- **Image handling:** Pillow for candidate photo uploads

## Security & Integrity

Votes are protected by database-level transactions and row-level locking. Each voter can submit exactly one ballot, enforced by a unique constraint and a locked check. Voter identity is bound to the session server-side, preventing code swapping on the ballot page. All management views require staff authentication.

## Getting Started

```bash
git clone <repo>
cd prefects_voting
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python manage.py migrate
python manage.py createsuperuser
python manage.py demo_data        # optional sample data
python manage.py runserver
```

Import your candidates and voters using `import_candidates` and `import_voters` management commands, then distribute codes to voters and open the kiosk at `/`.

## License

Released under the MIT License. Suitable for school, church, and community elections.
