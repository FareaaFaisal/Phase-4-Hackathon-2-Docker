# TO-DO Full Stack Web App (Phase 4)

A modern full-stack To-Do web application built with Next.js / React for the frontend and FastAPI + SQLModel for the backend.  
This project was developed following **Spec-Driven Development (SDD)** using **Gemini-CLI with SpecKit Plus**, and includes **Phase 4 enhancements** for containerization using Docker, orchestration, and AI automation.

The UI features beautiful moving animations, and the backend uses a **Neon serverless database** for storage along with **enhanced authentication** for secure user management. Users can create, update, complete, and delete tasks with real-time updates and a smooth, visually appealing interface.

---

## Phase 4 Highlights

- **Docker Containerization:** The backend and frontend are containerized for consistent deployments across environments.
- **Kubernetes Deployment:** Full app deployment on a Kubernetes cluster with scalable pods and services.
- **Helm Charts:** Simplified cluster deployment using Helm charts with configurable values.
- **AI Agents & Skills:** Automated task handling and AI chatbot enhancements using Cohere integration and custom agents.
- **Continuous Integration/Deployment Ready:** Easy to integrate with CI/CD pipelines for automated deployments.

---

## Features

- **User Authentication:** Sign up and log in with JWT tokens.
- **CRUD Operations:** Create, Read, Update, Delete tasks.
- **Task Completion:** Mark tasks as completed or pending.
- **Filtering & Sorting:** Filter tasks by status and sort by date or title.
- **Responsive UI:** Works on desktop and mobile devices.
- **Secure API:** Backend validates users and protects task access.
- **Phase 4 Automation:** Chatbot and agents automate task creation and management.

---

## Tech Stack

**Frontend:**

- Next.js (React)
- TypeScript
- Tailwind CSS
- Axios for API requests
- Docker for containerization

**Backend:**

- FastAPI
- SQLModel + PostgreSQL
- JWT/Better Auth Authentication
- Uvicorn server
- Dockerized backend container
- Kubernetes deployment configuration
- Helm charts for deployment
- Cohere AI integration for chatbot

**Database:**

- NEON Serverless POSTGRES Database

**DevOps & Deployment:**

- Docker
- Kubernetes
- Helm
- CI/CD pipelines compatible

---

## Getting Started

### **Backend Setup**

1. Go to the backend folder:
   ```bash
   cd backend
   ```

2. Create virtual environment and activate:

```bash
python -m venv venv
venv\Scripts\activate      # Windows
source venv/bin/activate   # Mac/Linux
```

3. Install dependencies:

```bash
pip install -r requirements.txt
```

4. Set up environment variables (.env):

```env
DATABASE_URL=postgresql://username:password@localhost:5432/todo_db
SECRET_KEY=your_secret_key
COHERE_API_KEY=YOUR_COHERE_API_KEY
```

5. Run the backend server:

```bash
uvicorn app.main:app --reload --port 8000
```

---

### **Backend Setup**

1. Go to the frontend folder:

```bash
cd frontend
```

2. Install dependencies:
   
```bash
npm install
```

3. Set up environment variables (.env):

```env
NEXT_PUBLIC_API_URL=http://localhost:8000/api/v1
```

4. Run the frontend:

```bash
npm run dev
```

5. Open your browser at http://localhost:3000

### **Docker & Kubernetes (Phase 4)**

_Run containers locally:_

```bash
docker run -p 8000:8000 todo-backend
docker run -p 3000:3000 todo-frontend
```

### **Database Migrations for Chatbot**

If this is a fresh setup or adding the chat feature to an existing Phase-2 application:

Ensure backend virtual environment is activated.

Navigate to backend/ directory.

### **Run Alembic migrations:**

```bash
alembic revision --autogenerate -m "Add Conversation and Message tables for AI Chatbot"
alembic upgrade head
```

### **AI Chatbot Usage**

- Ensure both backend and frontend servers are running.
- Log in to the application.
- Locate the chatbot icon in the UI and click it to open the chat panel.
- Type natural language commands to manage your to-do tasks (e.g., "Add 'buy groceries'", "List my pending tasks", "Complete task 5").
- Observe chatbot responses and updates to the task list.

### **Usage**

- Sign up or log in.
- Create a new task using the Add Task button.
- Edit or delete tasks as needed.
- Filter tasks by status (All, Pending, Completed) and sort them.
- Mark tasks as completed using the Mark Done / Completed button.
- Use the AI chatbot for automating task management (Phase 4 feature).

### **License**

This project is open source and available under the MIT License.

### **Author**

**Fareaa Faisal**
GitHub: https://github.com/FareaaFaisal
