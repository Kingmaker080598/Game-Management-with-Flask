# Game-Management-with-Flask
# Flask Game Management Application

## Overview

This is a Flask-based web application designed for managing and playing a simple multiplayer game. It includes features for user authentication, game setup, and tracking the game state. The app uses a **MySQL** database for data persistence, and it allows users with different roles (players and judge) to interact with the game.

The application has routes for registering and logging in users, setting up the game by the judge, and playing the game by the players. 

The app is built in Python using Flask and SQLAlchemy (for handling MySQL), and it's deployed on the **Azure Cloud Platform** for easy accessibility.

## Features

1. **User Registration & Login**: Users can register with a username, password, and role (player or judge). A login system is implemented using Flask session handling.
2. **Role-Based Views**:
   - **Players**: Can play the game, make moves, and view game status.
   - **Judge**: Can set up the game, view game state, and monitor players.
3. **Game Setup**: The judge sets up the game, defining players, piles of stones, and the game's parameters (minimum and maximum pickups).
4. **Game Play**: Players take turns picking stones from piles. The game keeps track of the players' scores and ensures valid moves.
5. **Game State Persistence**: The game state, including the number of stones left in each pile and the players' scores, is saved to the MySQL database.
6. **End of Game Detection**: The game ends when all piles are empty, and the app declares the winner based on the final scores.

## Technologies Used

- **Flask**: A lightweight web framework for Python.
- **MySQL (pymysql)**: The application connects to a MySQL database for storing user data and game state.
- **HTML & Jinja2**: Used for rendering the dynamic content of the web pages.
- **Azure Cloud Platform**: The application is hosted on Azure for high availability and scalability.

## Project Structure

```
.
├── app.py                   # Main application file
├── templates/               # HTML templates for rendering views
│   ├── index.html           # Home page
│   ├── login.html           # Login page
│   ├── register.html        # Registration page
│   ├── set_up_game.html     # Game setup page for the judge
│   ├── players_home.html    # Home page for players
│   ├── play_game.html       # Page for playing the game
│   └── game_over.html       # Page displayed when the game ends
├── static/                  # Static assets (CSS, images)
└── requirements.txt         # Python dependencies
```

## Setup and Installation

### Requirements

- Python 3.x
- Flask
- pymysql (MySQL connection library)
- A running MySQL database (local or cloud-based)

### Steps to Install and Run Locally

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/yourusername/flask-game-management.git
   cd flask-game-management
   ```

2. **Create a Virtual Environment** (optional):
   ```bash
   python -m venv venv
   source venv/bin/activate   # On Windows: venv\Scripts\activate
   ```

3. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Set Up Database**:
   - The application uses a MySQL database hosted on FreeSQLDatabase. You can configure your database connection details by updating the following section in `app.py`:
     ```python
     db_host = 'your_database_host'
     db_user = 'your_database_user'
     db_password = 'your_database_password'
     db_name = 'your_database_name'
     ```
   - Run the application once and visit `/create_table` to create the necessary tables in the database.

5. **Run the Application**:
   ```bash
   python app.py
   ```
   The app will run on `http://127.0.0.1:5000/`.

6. **Access the App**:
   - Open a browser and visit `http://127.0.0.1:5000/index`.
   - Register a user and log in to access the game features.

### Database Schema

The application uses the following tables:

- **`users`**:
  - `id`: User ID (Primary Key)
  - `username`: Username
  - `password`: Password (plain text for simplicity, recommend hashing in production)
  - `role`: Enum (`player`, `judge`)

- **`game_state`**:
  - `game_name`: Name of the game
  - `player1_name`: Name of player 1
  - `player2_name`: Name of player 2
  - `pile1`, `pile2`, `pile3`: The number of stones in each pile
  - `turn`: Whose turn it is (`player1` or `player2`)
  - `score1`, `score2`: Scores of player 1 and player 2
  - `min_pickup`, `max_pickup`: Minimum and maximum stones that can be picked per turn

## Usage

1. **Register**: Players and judges can register using the registration form. After registration, users can log in using their credentials.
2. **Judge Setup**: The judge sets up the game, defining players, piles, and other rules.
3. **Game Play**: Players take turns picking stones from piles according to the game rules. The game ensures valid moves and updates the game state.
4. **Game End**: When all piles are empty, the game ends and the winner is declared based on the scores.

## Security Considerations

- Passwords are currently stored in plain text. It is highly recommended to implement password hashing for production use.
- Sessions are used to manage user authentication, but for added security, you may want to add HTTPS and stronger session handling.

## License

This project is licensed under the MIT License. Feel free to use, modify, and distribute this code.

## Contributions

Contributions are welcome! Please submit issues or pull requests to contribute to this project.

---

This application provides a simple platform for multiplayer game management, with separate roles for players and judges. The flexible design allows for easy customization and extension for other game types or additional features.
