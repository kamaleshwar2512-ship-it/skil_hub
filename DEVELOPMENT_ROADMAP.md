## SECTION 1 — PROJECT FOLDER STRUCTURE

```text
/skil-hub
├── /frontend      # Contains the Vite + React.js web application, UI logic, and API consumption.
├── /backend       # Contains Node.js + Express.js APIs, authentication middleware, and database connections.
├── /ml-engine     # Contains Python API wrapper, Scikit-learn logic, and matching inference models.
├── /database      # Contains raw SQLite database files, schema designs, and mock seeding scripts.
└── /docs          # Contains PRD, Architecture roadmaps, and ongoing developer documentation.
```

---

## SECTION 2 — DEVELOPMENT PHASES

- Phase 1 — Local Environment Setup
- Phase 2 — Database Design
- Phase 3 — Backend API Development
- Phase 4 — Frontend Development
- Phase 5 — AI Matching Engine
- Phase 6 — Integration
- Phase 7 — Testing
- Phase 8 — Deployment Preparation

---

## SECTION 3 — TASK DEFINITIONS

TASK_ID: PH1-T1
TASK_NAME: Initialize Subdirectories and Package Managers
DESCRIPTION: Create base folders. Initialize `npm` for frontend/backend and `pip`/`venv` for the ML engine.
TECHNOLOGIES_USED: Node.js, Python, CLI
EXPECTED_OUTPUT: Folder structure mapped with baseline configuration files.
DEPENDENCIES: None
NEXT_TASK: PH1-T2

TASK_ID: PH1-T2
TASK_NAME: Scaffold Frontend Application
DESCRIPTION: Generate React boilerplate via Vite in the isolated frontend folder.
TECHNOLOGIES_USED: Vite, React.js
EXPECTED_OUTPUT: Running local Vite server rendering default React landing page.
DEPENDENCIES: PH1-T1
NEXT_TASK: PH2-T1

TASK_ID: PH2-T1
TASK_NAME: Define SQLite Relational Schema
DESCRIPTION: Write raw SQL definitions outlining `users`, `profiles`, `projects`, `project_roles`, `team_members`, and `messages`.
TECHNOLOGIES_USED: SQLite, SQL
EXPECTED_OUTPUT: A unified `schema.sql` defining correct data types, keys, and foreign relationships.
DEPENDENCIES: PH1-T1
NEXT_TASK: PH2-T2

TASK_ID: PH2-T2
TASK_NAME: Instantiate Local SQLite Database
DESCRIPTION: Run local CLI utility to compile `schema.sql` into a `.sqlite` datastore in the database local folder.
TECHNOLOGIES_USED: SQLite3 CLI
EXPECTED_OUTPUT: `.sqlite` file generated and queryable.
DEPENDENCIES: PH2-T1
NEXT_TASK: PH3-T1

TASK_ID: PH3-T1
TASK_NAME: Initialize Express Application
DESCRIPTION: Create server definitions, middleware inclusion, SQLite client connector, and error routers.
TECHNOLOGIES_USED: Node.js, Express, `sqlite3`
EXPECTED_OUTPUT: Express node successfully executing and connected to the SQLite file.
DEPENDENCIES: PH2-T2
NEXT_TASK: PH3-T2

TASK_ID: PH3-T2
TASK_NAME: Develop Authentication Module
DESCRIPTION: Generate Registration and Login logic binding bcrypt hashing and jsonwebtoken signatures.
TECHNOLOGIES_USED: Node.js, Bcrypt, JWT
EXPECTED_OUTPUT: Validated, stateless auth routes tested effectively via Postman/cURL.
DEPENDENCIES: PH3-T1
NEXT_TASK: PH3-T3

TASK_ID: PH3-T3
TASK_NAME: Construct Application CRUD APIs
DESCRIPTION: Design specific REST routes mapping project creation, user profiles extraction, and messaging routing.
TECHNOLOGIES_USED: Node.js, Express
EXPECTED_OUTPUT: Extensive API surface for logic state mutations.
DEPENDENCIES: PH3-T2
NEXT_TASK: PH4-T1

TASK_ID: PH4-T1
TASK_NAME: Develop Frontend Architecture & Auth Routing
DESCRIPTION: Instantiate React Router, integrate API fetch utility, state mechanisms, and complete JWT-bound login workflows.
TECHNOLOGIES_USED: React, React Router
EXPECTED_OUTPUT: Local UI handles secured rendering locked behind valid Logins.
DEPENDENCIES: PH3-T2
NEXT_TASK: PH4-T2

TASK_ID: PH4-T2
TASK_NAME: Create Core Dashboard User Interfaces
DESCRIPTION: Develop layout elements enabling users to mutate profiles, publish projects, and browse boards.
TECHNOLOGIES_USED: React
EXPECTED_OUTPUT: Connected UI layers executing accurate HTTP queries to local Backend.
DEPENDENCIES: PH3-T3, PH4-T1
NEXT_TASK: PH5-T1

TASK_ID: PH5-T1
TASK_NAME: Define ML Local Service
DESCRIPTION: Instantiate Flask or FastAPI environment capturing REST invocations in Python natively.
TECHNOLOGIES_USED: Python, Flask/FastAPI
EXPECTED_OUTPUT: Root Python service answering HTTP calls successfully.
DEPENDENCIES: PH1-T1
NEXT_TASK: PH5-T2

TASK_ID: PH5-T2
TASK_NAME: Integrate Scikit-Learn Engine
DESCRIPTION: Write TF-IDF text vectorizers and Cosine metrics scoring lists of profiles against targeted string criteria.
TECHNOLOGIES_USED: Python, Scikit-learn, Pandas
EXPECTED_OUTPUT: ML mathematical API yielding structurally typed lists of JSON objects sorted by compatibility.
DEPENDENCIES: PH5-T1
NEXT_TASK: PH6-T1

TASK_ID: PH6-T1
TASK_NAME: Inter-Service System Connectivity
DESCRIPTION: Connect Node Backend logic specifically bypassing match determinations to Python engine REST URL natively.
TECHNOLOGIES_USED: Node.js, Axios/Fetch
EXPECTED_OUTPUT: Multi-tier architectural success requesting matches from Frontend -> Backend -> ML -> Backend -> Frontend.
DEPENDENCIES: PH3-T3, PH5-T2
NEXT_TASK: PH6-T2

TASK_ID: PH6-T2
TASK_NAME: Frontend AI Matching Feedback Loop UI
DESCRIPTION: Interface matching algorithms output into visual cards representing top teammate candidates.
TECHNOLOGIES_USED: React.js
EXPECTED_OUTPUT: Beautiful UI resolving mathematical match scores into viable User Profile elements.
DEPENDENCIES: PH4-T2, PH6-T1
NEXT_TASK: PH7-T1

TASK_ID: PH7-T1
TASK_NAME: Finalize Full Stack Testing Procedures
DESCRIPTION: Iterate through isolated components natively connecting user mapping from creation to team-acceptance fully manually.
TECHNOLOGIES_USED: Postman, Web Browser
EXPECTED_OUTPUT: Verified robust flow capable of zero structural errors logic executions.
DEPENDENCIES: PH6-T2
NEXT_TASK: PH8-T1

TASK_ID: PH8-T1
TASK_NAME: Documentation Completion
DESCRIPTION: Audit codebase, provide runtime scripts (e.g., `npm run dev:all` concurrently) simplifying localized system bootup.
TECHNOLOGIES_USED: Markdown, Package.json
EXPECTED_OUTPUT: Refined project enabling instant resuming configurations.
DEPENDENCIES: PH7-T1
NEXT_TASK: None

---

## SECTION 4 — PROGRESS TRACKING TABLE

| TASK_ID | STATUS       | LAST_UPDATED |
|---------|--------------|--------------|
| PH1-T1  | NOT_STARTED  |              |
| PH1-T2  | NOT_STARTED  |              |
| PH2-T1  | NOT_STARTED  |              |
| PH2-T2  | NOT_STARTED  |              |
| PH3-T1  | NOT_STARTED  |              |
| PH3-T2  | NOT_STARTED  |              |
| PH3-T3  | NOT_STARTED  |              |
| PH4-T1  | NOT_STARTED  |              |
| PH4-T2  | NOT_STARTED  |              |
| PH5-T1  | NOT_STARTED  |              |
| PH5-T2  | NOT_STARTED  |              |
| PH6-T1  | NOT_STARTED  |              |
| PH6-T2  | NOT_STARTED  |              |
| PH7-T1  | NOT_STARTED  |              |
| PH8-T1  | NOT_STARTED  |              |
