# SandLock Owner Dashboard

Real-time owner dashboard for the SandLock prototype.

## What is included
- Real-time HiveMQ monitoring for Locker A
- Owner remote unlock command
- Users, reservations, access logs, device events, alerts, payments, feedback
- Excel-backed local database: `data/SandLock_Dashboard_Database.xlsx`
- Same MindForge / beach / teal-gold visual language as the user PWA
- Updated copy of the PWA in `app_patch/` that publishes admin-facing events without changing its UI

## Run on Ubuntu/Linux
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python3 server.py
```
Open: http://localhost:5000

## Run on Windows
```bat
py -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
py server.py
```
Open: http://localhost:5000

## Excel database sheets
Users, Reservations, Access Logs, Device Events, Alerts, Payments, Feedback, Lockers.

## Important
The dashboard currently uses the existing prototype HiveMQ credential so it works immediately with the current broker permission. For a production deployment, create a dedicated dashboard credential and move secrets to environment variables / a backend secret store.

## PWA integration patch
The `app_patch/` folder is the current SandLock PWA with the same UI and user flow, plus silent MQTT admin-event publications under:
- `sandlock/locker/A/app/user/upsert`
- `sandlock/locker/A/app/reservation/upsert`
- `sandlock/locker/A/app/reservation/cancel`
- `sandlock/locker/A/app/reservation/complete`
- `sandlock/locker/A/app/access`
- `sandlock/locker/A/app/payment`
- `sandlock/locker/A/app/feedback`

These topics stay inside the current `sandlock/locker/A/#` permission, so no broker permission change is required for this prototype.
