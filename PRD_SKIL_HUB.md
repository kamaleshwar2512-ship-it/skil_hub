# 1. Product Overview
Student Knowledge Integration Learning Hub (SKIL Hub) is a web platform designed to facilitate team formation for student projects through an AI-based skill matching engine. The system allows students to create extensive profiles and post projects defining clear constraints for skills, roles, and deadlines. It then programmatically recommends the best teammate combinations available.

# 2. Problem Statement
Students lack centralized, data-driven platforms to locate peers with complementary skills for collaborative projects. Relying on organic networking restricts diverse skill crossover and optimal resource allocation, often resulting in uncompleted projects or poorly balanced development teams.

# 3. Objectives
- Eliminate friction in student-led project team formation.
- Automate optimal teammate discovery based on exact skill matches and availability parameters.
- Provide end-to-end functionality for discovery, communication, and post-project peer ratings.

# 4. Target Users
- Students seeking to join projects to build portfolios.
- Project originators requiring specific technical or creative skill sets.

# 5. User Personas
- **The Architect:** A student with a project vision missing specific execution capabilities (e.g., backend developer needing a frontend specialist).
- **The Specialist:** A student with defined skills and free time looking to contribute to a structured project.

# 6. Core Features
- **User Profiles Definition:** Data models mapping skills, experience level, and availability.
- **Projects Board & Requirements:** CRUD operations for team requirements and timelines.
- **AI-Based Teammate Recommender:** Scikit-learn similarity matching engine.
- **Messaging Micro-Framework:** Internal REST-based text communication among matched users.
- **Peer Rating Algorithm:** Bi-directional rating after task completion adjusting aggregate user scores.

# 7. Functional Requirements
- System must authenticate accounts using stateless JWT via HTTP headers.
- System must compute AI recommendations upon a GET request with targeted project role requirements.
- System must conditionally render team acceptance workflows (Invite -> Pending -> Accepted/Rejected).
- System must persist real-time-like messaging logic via database polling or repeated REST fetches on the local environment.

# 8. Non Functional Requirements
- **Local Isolation:** Must operate with zero cloud dependencies; utilizing local host environments.
- **Performance:** DB queries and AI inference scoring must return within 500ms locally.
- **Modularity:** API endpoints and ML endpoints must be strictly separated for future containerization.

# 9. System Architecture Overview
Client-Server model strictly mapped to local ports:
- **Frontend (Vite/React):** Running on `localhost:5173`. Interacts exclusively through REST APIs.
- **Backend (Node/Express):** Running on `localhost:3000`. Acts as the central logic layer and Database driver.
- **ML Engine (Python):** Running on `localhost:5000`. Exposes specific internal REST routes for the backend to query candidate similarity matrices.
- **Database:** Local SQLite file (`.sqlite`) queried directly by the Node backend.

# 10. Technology Stack
- **Frontend:** React.js (via Vite)
- **Backend:** Node.js, Express.js
- **Database:** SQLite
- **AI/Machine Learning:** Python, Scikit-learn (Flask/FastAPI wrapper)
- **Authentication:** JWT, bcrypt
- **Communication:** REST API, JSON payloads

# 11. AI Matching Engine Design
- **Inputs:**
  1. Base Profile Vector (Candidate's listed skills, explicitly declared interests).
  2. Request Vector (Project role requirements, hard constraints).
- **Scoring Logic:**
  - Tokenize skills.
  - Apply TF-IDF (Term Frequency-Inverse Document Frequency) against a local corpus of skills.
  - Compute Cosine Similarity between Candidate Vectors and Request Vectors.
  - Absolute Penalty Filters applied for 0% availability overlaps.
- **Execution:** Python service returns a structured array of JSON objects `[{ "user_id": X, "match_score": 0.89 }]`.

# 12. Database Design Overview
Relational Schema mapped to SQLite:
- `users`: `id` (PK), `email`, `password_hash`, `rating`.
- `profiles`: `id` (PK), `user_id` (FK), `skills` (JSON text), `interests` (JSON text), `availability`.
- `projects`: `id` (PK), `owner_id` (FK), `title`, `description`, `deadline`.
- `project_roles`: `id` (PK), `project_id` (FK), `role_name`, `required_skills` (JSON text).
- `team_members`: `id` (PK), `project_id` (FK), `user_id` (FK), `status` (ENUM: Pending, Accepted).
- `messages`: `id` (PK), `sender_id`, `receiver_id`, `content`, `created_at`.

# 13. API Design Overview
- `POST /api/auth/register` - Create user and profile.
- `POST /api/auth/login` - Returns JWT.
- `GET /api/projects/:id` - Fetch project details and roles.
- `POST /api/projects/:id/match` - Node backend proxies constraints to Python ML Engine (`localhost:5000/score`) and aggregates the DB profiles.
- `POST /api/teams/invite` - Initiates team status change to Pending.
- `PUT /api/teams/accept` - Changes team status to Accepted.

# 14. User Flow
1. User sets up local environment (React, Node, Python).
2. Registers account. Fills UI component for technical capacities.
3. User views Dashboard. Chooses "Create Project".
4. Submits Project logic. Hits "Discover Candidates".
5. Backend hands context to Python service, returns top mathematically sound profiles.
6. User clicks "Send Invite", creating relational map in `team_members`.
7. Receiving user logs in, accepts invite, project dashboard opens communication window.

# 15. Security Considerations
- Local HTTP communication but standard best practices strictly implemented for future cloud readiness.
- Parameterized SQL queries universally applied via sqlite3 library to prevent SQL injection.
- Passwords universally hashed via bcrypt with salt limits defined locally. 
- Stateless JWTs configured with discrete expiration lifecycles.

# 16. Success Metrics
- Successfully spinning up the three independent local servers natively.
- Verification of accurate TF-IDF Cosine Similarity logic outputs matching distinct project requests.
- Fluid execution of full application lifecycle from User Registration to Team Formation.

# 17. Future Improvements
- Refactor SQLite queries into a formal ORM mapping strategy (Prisma or Sequelize) for PostgreSQL migration.
- Containerize application modules with internal virtual networks via `docker-compose`.
- Refactor stateless HTTP polling messaging to Websockets (Socket.io).
- Broaden ML logic incorporating natural language inference (Transformers) instead of discrete frequency mapping.
