TaskFlow — Task Management Application
A clean, responsive task management web app built as a single-file HTML application. Includes user authentication, full CRUD task management, multiple views, and a Kanban board — all running in the browser with localStorage persistence.

Features
Authentication

User registration and sign-in with email and password
Session persistence across page reloads via localStorage
Demo account pre-configured: demo@taskflow.io / demo1234
Per-user task isolation (each user only sees their own tasks)

Task Management (CRUD)

Create tasks with title, description, status, priority, tag, and due date
Read tasks across multiple filtered views
Update tasks inline — click any card to open the edit modal
Delete tasks with a single action
Toggle task completion directly from the checkbox on each card

Views
ViewDescriptionDashboardStats overview and today's active tasksAll TasksFull task list with status filters and sortingTodayTasks due todayUrgentHigh-priority and overdue tasksBoardKanban-style 3-column view (To Do / In Progress / Done)
Filtering & Sorting

Filter by status: All, To Do, In Progress, Done
Filter by tag from the sidebar: Work, Personal, Design, Development
Sort by: latest created, due date, or priority
Live search across task titles and descriptions

Task Properties
FieldOptionsTitleFree text (required)DescriptionFree text (optional)StatusTo Do, In Progress, DonePriorityHigh, Medium, LowTagWork, Personal, Design, Development, OtherDue DateDate picker

Getting Started
No build tools or dependencies required. This is a self-contained single HTML file.
Run locally
bash# Option 1 — open directly
open taskflow.html

# Option 2 — serve with Python
python3 -m http.server 8080
# then visit http://localhost:8080/taskflow.html

# Option 3 — serve with Node
npx serve .
Demo login
Email:    demo@taskflow.io
Password: demo1234

Technical Overview
Stack

HTML / CSS / JavaScript — no frameworks, no build step
localStorage — all data persisted in the browser
Google Fonts — Playfair Display (headings) + DM Sans (body)
Tabler Icons — outline icon set loaded via CDN

Data Model
Tasks are stored as a JSON array in localStorage under the key tf_tasks:
json{
  "id": 1748345600000,
  "title": "Review Q3 design mockups",
  "desc": "Check all screens for consistency",
  "status": "in-progress",
  "priority": "high",
  "tag": "design",
  "due": "2026-05-27",
  "owner": "demo@taskflow.io",
  "created": 1748345600000
}
Users are stored under tf_users and the active session under tf_session.
Key Functions
FunctionPurposelogin()Validates credentials and initialises the appregister()Creates a new user accountsaveTask()Creates or updates a task (handles both new and edit)deleteTask()Removes a task by IDtoggleDone()Flips task status between done and todorenderAll()Re-renders all views and updates sidebar badgesfilterTasks()Applies search, status filter, and sort to the All Tasks viewshowPage()Switches the active view

Project Structure
taskflow.html        ← entire application (HTML + CSS + JS)
README.md            ← this file

Customisation
Adding a new tag

Add an <option> to the #task-tag select in the modal
Add a .tag-{name} CSS class with background and text color
Optionally add a sidebar nav item that calls filterByTag('{name}')

Adding a new priority level

Add the option to the #task-priority select
Add a .priority-{name} CSS rule for the card's left border color
Update the priority sort order in the sortTasks() function

Replacing localStorage with a backend
Swap out these four functions to point at your API:
javascriptfunction saveTasks()   { /* POST /api/tasks */ }
function myTasks()     { /* GET  /api/tasks?owner=... */ }
function login()       { /* POST /api/auth/login */ }
function register()    { /* POST /api/auth/register */ }

Browser Support
Works in all modern browsers (Chrome, Firefox, Safari, Edge). Requires JavaScript enabled. No polyfills needed.

Limitations

Data is stored in the browser's localStorage — clearing site data will erase all tasks
No real-time sync across devices or tabs
No file attachments or rich text in descriptions
Single-user per browser session (multi-user requires a backend)


License
MIT — free to use, modify, and distribute.
