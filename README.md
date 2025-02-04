# sports-scheduler
Sports Session Management App
Description
This is a web-based application for managing sports sessions, allowing users to register, log in, create sessions, and join them. It features two types of users: Admins and Players. Admins can create sports, manage sessions, and view reports, while players can join available sessions. The application uses Express, PostgreSQL, bcryptjs for authentication, and EJS for rendering dynamic content.

Features
Authentication: Users can register, log in, and log out.
Admin Dashboard: Admins can manage sports, sessions, and view detailed reports.
Player Dashboard: Players can view available sessions and join them.
Session Management: Admins can create, delete, and cancel sessions. Players can join and leave sessions.
Reports: Admins can view reports about session popularity by sport.
Technologies Used
Node.js: Backend framework to run the application.
Express: Web framework for building the app.
bcryptjs: For hashing passwords.
PostgreSQL: Database for storing user data, sports, sessions, and other related data.
EJS: Template engine for rendering dynamic HTML.
express-session: For handling user sessions.
Installation
Prerequisites
Node.js (>=14.x)
npm (Node package manager)
PostgreSQL (>=12.x)
Steps to Setup
Clone this repository:

bash
Copy code
git clone https://github.com/your-username/sports-session-management-app.git
Navigate to the project directory:

bash
Copy code
cd sports-session-management-app
Install the required dependencies:

bash
Copy code
npm install
Set up PostgreSQL:

Create a PostgreSQL database (e.g., sports_sessions).
Update the database connection configuration in the ./database.js file.
Run the migrations to create the necessary tables (example for users and sessions):

sql
Copy code
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  email VARCHAR(100) UNIQUE NOT NULL,
  password VARCHAR(255) NOT NULL,
  role VARCHAR(50) CHECK (role IN ('admin', 'player')) NOT NULL
);

CREATE TABLE sports (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL
);

CREATE TABLE sessions (
  id SERIAL PRIMARY KEY,
  sport_id INT REFERENCES sports(id),
  creator_id INT REFERENCES users(id),
  team1 VARCHAR(100),
  team2 VARCHAR(100),
  additional_players INT DEFAULT 0,
  date TIMESTAMP,
  venue VARCHAR(255),
  cancelled BOOLEAN DEFAULT FALSE,
  cancellation_reason TEXT
);

CREATE TABLE session_players (
  session_id INT REFERENCES sessions(id),
  player_id INT REFERENCES users(id),
  PRIMARY KEY (session_id, player_id)
);
Start the server:

bash
Copy code
npm start
The app will run on http://localhost:3000.

Application Routes
GET /: Home page.
GET /login: Login page.
POST /login: Login action.
GET /register: Register page.
POST /register: Registration action.
GET /admin-dashboard: Admin dashboard to manage sessions and sports.
POST /create-sport: Action to create a new sport.
POST /delete-session: Action to delete a session.
GET /player-dashboard: Player dashboard to view and join sessions.
POST /create-session: Action to create a new session.
POST /join-session: Action to join a session.
POST /cancel-session: Action to cancel a session.
GET /reports: Admin can view reports about session popularity.
User Roles
Admin:

Create and manage sports and sessions.
View reports on session popularity.
Delete or cancel sessions.
Player:

Register and log in.
Join available sessions.
View session details and other players.
Security Considerations
Passwords are hashed using bcryptjs to ensure security.
Sessions are managed using express-session to keep users authenticated.
Contributing
Contributions are welcome! Please fork the repository and submit a pull request with any improvements or features.