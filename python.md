
# API Request Examples in Python

This directory contains Python scripts that demonstrate how to make various types of HTTP requests to an API, including handling authentication with access and refresh tokens.

A mock API server is also included so you can run and test these examples locally.

## Requirements

- Python 3

## Setup Instructions

All commands should be run from the root directory of this project (`/Users/efulgencio/Documents/gemini/`).

### 1. Create a Python Virtual Environment

To keep dependencies isolated, we use a virtual environment. This only needs to be done once.

```bash
python3 -m venv api/venv
```

### 2. Install Required Libraries

Install the necessary Python libraries (`Flask` for the mock server and `requests` for the client scripts) into the virtual environment.

```bash
# The requests library is likely already installed, but this ensures it's in the venv
api/venv/bin/pip install requests

# Flask is needed for the mock server
api/venv/bin/pip install Flask
```

## How to Run the Examples

You will need **two separate terminal windows** open to run the mock server and the client scripts simultaneously.

**Important**: Before running the commands below, make sure your terminal's current working directory is the root of this project.

- You can check your current directory by running: `pwd`
- It should show: `/Users/efulgencio/Documents/gemini`
- If you are in a different directory, navigate to the correct one using: `cd /Users/efulgencio/Documents/gemini`

---

### Terminal 1: Start the Mock API Server

First, activate the virtual environment in this terminal.

```bash
source api/venv/bin/activate
```

Your terminal prompt should now start with `(venv)`.

Now, start the mock API server. This server will listen for requests from the client scripts.

```bash
python api/mock_api_server.py
```

You should see output indicating the server is running, like `* Running on http://127.0.0.1:5000`. Leave this terminal running.

---

### Terminal 2: Run the Client Scripts

Open a new terminal window and **make sure you are in the project root directory** as described above. Then, activate the virtual environment here as well.

```bash
source api/venv/bin/activate
```

Now you can run any of the example scripts.

#### A. Login Example

This script simulates a simple login request.

```bash
python api/login_example.py
```

#### B. Authenticated Request Example

This script attempts to fetch data with the token from the login. It will fail, which is the expected behavior to demonstrate an expired token.

```bash
python api/products_example.py
```

#### C. Token Refresh and Retry Example

This is the complete flow. The script will first attempt to get data, fail because the token is expired, automatically use the refresh token to get a new access token, and then successfully retry the request.

```bash
python api/token_refresh_example.py
```

---

### When You're Done

When you are finished, you can stop the mock server in the first terminal by pressing `Ctrl + C`.

To exit the virtual environment in either terminal, simply run:

```bash
deactivate
```
