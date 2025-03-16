# Self-Hosting Guide for Hopon Music

This guide provides step-by-step instructions for self-hosting Hopon Music on your own server or local machine. The app allows users to register, log in, upload and play songs, manage their profiles, and includes moderator functionalities for managing users and songs.

---

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Installation](#installation)
3. [Configuration](#configuration)
4. [Running the App](#running-the-app)
5. [Deployment](#deployment)
6. [Troubleshooting](#troubleshooting)
7. [Contributing](#contributing)
8. [License](#license)

---

## Prerequisites

Before you begin, ensure you have the following installed:
- **Python 3.8+**: [Download Python](https://www.python.org/downloads/)
- **pip**: Python package installer (usually comes with Python)
- **SQLite**: Lightweight database (usually pre-installed on most systems)
- **Git**: [Download Git](https://git-scm.com/downloads)

---

## Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/Virus01Official/HopOnMusic.git
   cd HopOnMusic
   ```

2. **Create a Virtual Environment**:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
   ```

3. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

---

## Configuration

1. **Set Up Environment Variables**:
   - Create a `.env` file in the root directory.
   - Add the following variables:
     ```env
     SECRET_KEY=your_secret_key_here
     UPLOAD_FOLDER=static/uploads
     ```
   - Replace `your_secret_key_here` with a secure secret key for Flask sessions.

2. **Initialize the Database**:
   - The app will automatically create a `database.db` file and initialize the required tables on the first run.

3. **Configure Upload Folder**:
   - Ensure the `static/uploads` directory exists. The app will create it automatically if it doesn't.

---

## Running the App

1. **Run the Development Server**:
   ```bash
   python app.py
   ```
   - The app will be available at `http://127.0.0.1:5000`.

2. **Access the App**:
   - Open your browser and navigate to `http://127.0.0.1:5000`.
   - Register a new user or log in with existing credentials.

---

## Deployment

For production deployment, consider using a WSGI server like **Gunicorn** and a reverse proxy like **Nginx**.

1. **Install Gunicorn**:
   ```bash
   pip install gunicorn
   ```

2. **Run the App with Gunicorn**:
   ```bash
   gunicorn --workers 4 app:app
   ```

3. **Set Up Nginx**:
   - Configure Nginx to proxy requests to Gunicorn. Example configuration:
     ```nginx
     server {
         listen 80;
         server_name yourdomain.com;

         location / {
             proxy_pass http://127.0.0.1:8000;
             proxy_set_header Host $host;
             proxy_set_header X-Real-IP $remote_addr;
             proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
         }
     }
     ```

4. **Secure with HTTPS**:
   - Use **Let's Encrypt** to obtain a free SSL certificate and configure Nginx to serve the app over HTTPS.

---

## Troubleshooting

- **Database Issues**:
  - If the database is not initialized, delete the `database.db` file and restart the app.
  
- **File Upload Issues**:
  - Ensure the `static/uploads` directory has the correct permissions.
  - Check the allowed file types in the `allowed_file` and `allowed_image` functions.

- **Session Issues**:
  - Ensure the `SECRET_KEY` is set in the `.env` file.

---

## Contributing

Contributions are welcome! Please follow these steps:
1. Fork [this](https://github.com/Virus01Official/HopOnMusic) repository.
2. Create a new branch for your feature or bugfix.
3. Submit a pull request with a detailed description of your changes.

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
