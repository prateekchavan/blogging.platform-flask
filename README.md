# Inkwell — Flask Blogging Platform

A responsive, full-stack blogging app built with Flask, SQLite, Flask-Login and SQLAlchemy. Includes authentication, post CRUD, comments, search, sorting, responsive navigation and production deployment configuration.

## Features
- Register, sign in and sign out; passwords are securely hashed.
- Create, read, edit and delete blog posts.
- Only the post owner can edit or delete their posts (403 otherwise).
- Signed-in users can comment on posts.
- Search by post title, content or author; sort newest/oldest.
- SQLite database is created automatically on first run.
- Responsive interface and helpful validation/flash messages.

## Run locally
Requires Python 3.10+.

```bash
# 1. Create and enter a virtual environment
python -m venv .venv
# Windows PowerShell:
.venv\\Scripts\\Activate.ps1
# macOS/Linux:
source .venv/bin/activate

# 2. Install dependencies
python -m pip install --upgrade pip
pip install -r requirements.txt

# 3. Set a secret key (PowerShell)
$env:SECRET_KEY = "replace-with-a-long-random-secret"
# macOS/Linux:
export SECRET_KEY="replace-with-a-long-random-secret"

# 4. Start the development server
python app.py
```
Open http://127.0.0.1:5000.

## Suggested manual test flow
1. Register account A; publish a post.
2. Open the post; add a comment.
3. Edit the post; verify the updated text.
4. Create account B in another browser/private window.
5. Verify account B can read/comment but cannot edit/delete account A's post (403).
6. Search for a title word and test both sort orders.
7. Sign out and verify create/comment actions redirect to sign-in.

## GitHub upload
```bash
git init
git add .
git commit -m "Build Inkwell Flask blogging platform"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/inkwell-blog.git
git push -u origin main
```
Create an empty GitHub repository first and replace the remote URL.

## Deployment
A `Procfile` is included for Gunicorn-compatible hosts. Configure:
- `SECRET_KEY`: a long random secret (never commit it).
- `DATABASE_URL`: persistent database URL if your host provides one. SQLite is suitable for local development; use managed PostgreSQL for production.
- Start command: `gunicorn app:app`

For PostgreSQL, install a compatible driver and use the provider's SQLAlchemy URL. Ensure the database is persistent and run migrations when adopting schema changes.

## Security and production notes
- Never deploy with the development fallback secret key.
- Set `FLASK_DEBUG=0` in production.
- Add CSRF protection (e.g. Flask-WTF), rate limiting, email verification and database migrations before public production use.
- Set secure session cookie flags and serve only over HTTPS.
- The included SQLite database is created at runtime and is intentionally not committed.

## Project structure
```
inkwell_blog/
├── app.py
├── requirements.txt
├── Procfile
├── .gitignore
├── README.md
├── SCREENSHOT_GUIDE.md
├── COMPLETION_VIDEO_SCRIPT.md
├── templates/
│   ├── base.html
│   ├── index.html
│   ├── login.html
│   ├── register.html
│   ├── post.html
│   ├── post_form.html
│   └── error.html
└── static/
    └── style.css
```
