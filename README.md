# Rewire

Rewire is a mobile application designed to assist individuals in overcoming addictions through a structured, step-by-step approach without the use of medication. The app leverages an AI-driven chatbot and questionnaires to assess addiction levels and categorize addictions into substance-based or behavioral types.

## Features
- Addiction recovery task recommender
- Integrated AI ChatBot
- Community platform
- Emergency support system

---

# Development Guide

## Using Git
### Cloning
- First, make sure you are not in another Git repository. Run the following command to check:
   ```bash
   git status
   ```
  Expected output:
   ```bash
   fatal: not a git repository (or any of the parent directories): .git
   ```
- To clone this repository to your computer, run one of the following commands:
    - HTTPS:
      ```bash
      git clone https://github.com/Project-Rewire/App.git
      ```
    - SSH (Recommended for a persistent and secure connection)
      ```bash
      git clone git@github.com:Project-Rewire/App.git
      ```

### Branching
- View available branches:
  ```bash
  git branch -a
  ```
- Switch to a branch:
  ```bash
  git switch branch_name
  ```
  *(If `git switch` is not available, use `git checkout branch_name` instead.)*
- Create a new local branch:
  ```bash
  git branch new_branch_name
  ```
- Push the newly created branch to the remote repository:
  ```bash
  git push -u origin new_branch_name
  ```

### Staging and Committing
- Stage changes:
    - Stage specific files:
      ```bash
      git add file_name1 file_name2 file_name3
      ```
    - Stage all changes:
      ```bash
      git add .
      ```
- Commit the changes:
  ```bash
  git commit -m "type(scope): A Meaningful Commit Message"
  ```
  **Commit Message Format (Conventional Commits)**:
  ```
  type(scope): A Meaningful Commit Message
  ```
    - **type**: `feat` (new feature), `fix` (bug fix), `chore` (maintenance), `docs` (documentation update), etc.
    - **scope**: Module or feature affected (e.g., `auth`, `dashboard`)
    - **message**: A brief, meaningful description of the changes

  Example:
  ```bash
  git commit -m "feat(auth): Add user login functionality"
  ```
  Refer to [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) for more details.

### Merging to `main`
- Merging branches into `main` should only be done on GitHub.
- To merge, create a "Pull Request" (PR) with a brief description of the changes.
- Always specify a reviewer for the PR.
- Once the PR is approved, merge it yourself.

## Running the Frontend

## Prerequisites
1. Make sure the latest version of `node` is installed:
   ```bash
   node -v
   ```
   You should see an output similar to the following:
   ```
   v22.13.1
   ```
2. Open IDE at the `App/frontend` directory.

## Installing Dependencies
- Install the required `node_modules`
   ```bash
   npm install
   ```

## Start the frontend
- Run the following to start the frontend in the development mode:
   ```bash
   npm start
   ```
- Enter `w` for web view or enter `http://localhost:8081` in the browser.

## Running the Backend with Docker (Recommended)

### Prerequisites
1. Ensure Docker is installed and up to date:
   ```bash
   docker --version
   ```
   Expected output (version may vary):
   ```
   Docker version 27.5.1, build 9f9e405
   ```
2. Ensure Docker is running in the background.
3. Open your IDE at the `App/backend/rewire` directory.

### Build and Start the Backend
1. Build the backend without using cache:
   ```bash
   docker build --no-cache .
   ```
   This may take some time depending on system performance and internet speed.

2. Start the container:
   ```bash
   docker-compose up
   ```
   The first run may require downloading dependencies, so it could take additional time.

3. Once started, the server should be available on port `8000`. Expected output:
   ```
   ✔ rewire                     Built
   ✔ Network rewire_default     Created
   ✔ Container rewire-db-1      Created
   ✔ Container rewire-rewire-1  Created
   Attaching to db-1, rewire-1
   db-1      | PostgreSQL Database directory appears to contain a database; Skipping initialization
   db-1      | LOG:  database system is ready to accept connections
   rewire-1  | Django version 5.1.6, using settings 'admin.settings'
   rewire-1  | Starting development server at http://0.0.0.0:8000/
   ```

### Handling Errors
If you encounter an error like:
   ```
   django.db.utils.OperationalError: connection failed: connection to server at "172.18.0.2", port 5432 failed: Connection refused
   ```
1. Stop the container by pressing `ctrl+c`.
2. Restart it:
   ```bash
   docker-compose up
   ```

3. Verify the server is running by opening `http://localhost:8000`. You should see a Django 404 page.

---

## Running the Backend Without Docker
### Prerequisites
1. Ensure Python 3.9 or above is installed:
   ```bash
   python --version
   ```
   You should get something like this:
   ```
   Python 3.13.0
   ```
2. Open your IDE at the `App/backend/rewire` directory.

### Setting Up a Virtual Environment
1. Install virtualenv (if not installed):
   ```bash
   pip install virtualenv
   ```
2. Create a virtual environment:
   ```bash
   python -m venv .venv
   ```
3. Confirm `.venv` folder exists.
4. Activate the virtual environment:
   - **Mac/Linux:**
     ```bash
     source .venv/bin/activate
     ```
   - **Windows (PowerShell):**
     ```bash
     .venv/Scripts/Activate.ps1
     ```
   - **Windows (CMD):**
     ```
     C:/Users/<USER>/<PATH>/App/backend/rewire/.venv/Scripts/activate.bat
     ```
   You should now see `(.venv)` at the beginning of your terminal prompt.

### Installing Dependencies
1. Install required packages from `requirements.txt`:
   ```bash
   pip install -r requirements.txt
   ```

### Configuring the Database
1. Ensure a PostgreSQL database is running.
2. Use the provided `.env` file (not included in the repository for security reasons) to configure credentials.
3. Database setup is beyond the scope of this guide; refer to the appropriate documentation.

### Running the Server
1. Start the backend:
   ```bash
   python manage.py runserver 8000
   ```
   Expected output:
   ```
   Watching for file changes with StatReloader
   Performing system checks...
   System check identified no issues.
   Django version 5.1.6, using settings 'admin.settings'
   Starting development server at http://0.0.0.0:8000/
   ```
2. Stop the server using `Ctrl+C`.

---

## Managing Migrations
### Handling Initial Migrations
When starting the server for the first time, you may see:
```
You have 18 unapplied migration(s). Your project may not work properly until you apply the migrations.
Run 'python manage.py migrate' to apply them.
```

#### If Using Docker
1. Open a new terminal in the same directory and enter the Docker shell:
   ```bash
   docker-compose exec rewire sh
   ```
2. Apply migrations:
   ```bash
   python manage.py makemigrations core
   ```
   ```bash
   python manage.py migrate
   ```
3. Restart the server, and the warning should be gone.

#### If Running Without Docker
1. Apply migrations directly:
   ```bash
   python manage.py makemigrations core
   ```
   ```bash
   python manage.py migrate
   ```
2. Restart the server and verify that the warning disappears.

---
