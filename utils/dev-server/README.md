# Local development server

## Setup

Perform the following steps from the terminal

### 1) Create and activate python 3 virtual environment

```bash
python3 -m venv venv
source venv/bin/activate
```

### 2) Install dependencies

```bash
pip install -r utils/dev-server/requirements.txt
```

## Run local server

```bash
source venv/bin/activate
./utils/dev-server/server.py -l info -r ..
```

Local instance of site will be available on http://localhost:8080