# rpa-actions-template

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![Ruff](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/ruff/main/assets/badge/v2.json)](https://github.com/astral-sh/ruff)
[![BotCity](https://img.shields.io/badge/BotCity-SDK-red.svg)](https://www.botcity.dev/)

Official template for creating BotCity automation projects with Python. Includes pre-configured CI/CD, automated linting, and integration with the BotCity platform.

## 🚀 Features

- ✅ CI/CD pipeline integrated with GitHub Actions
- ✅ Automated linting with Ruff and Pydocstyle
- ✅ Automatic deployment to BotCity
- ✅ Automatic semantic versioning using GitHub tags 
- ✅ Organized project structure
- ✅ Semantic versioning configuration
- ✅ Support for multiple environments (dev/prod)

## 📋 Prerequisites

- Python 3.11 or higher
- [BotCity](https://www.botcity.dev/) account
- GitHub account
- Git installed locally

## 🛠️ Installation

1. **Use this template**:
- Click the "Use this template" button on GitHub or:
- git clone https://github.com/your-username/botcity-python-template.git


2. **Set up the environment**:
```bash
cd botcity-python-template
python -m venv venv
source venv/bin/activate  # Linux/Mac
# or
venv\Scripts\activate  # Windows
```

3. **Install dependencies**:
- Using pip
```bash
pip install -r requirements.txt
```

- Using poetry
```bash
poetry install
```

4. **Configure GitHub secrets**:
- **LOGIN:** Your BotCity login
- **SERVER:** BotCity server URL
- **KEY:** BotCity API key

## 📁 Project Structure

```text
botcity-python-template/
├── .github/
│   └── workflows/
│       ├── linter.yaml         # Linting only
│       └── botcity-ci-cd.yaml  # BotCity deployment
├── src/
│   └── main.py                 # Main bot code
├── requirements.txt            # Project dependencies
├── build.sh                    # Build script
└── README.md
```

## ⚙️ Available Workflows

1. **Linting Only** `(.github/workflows/linter.yaml)`
Ideal for RPA projects that only need code validation.

    Features:
    - Code validation with Ruff
    - Docstring checking with Pydocstyle
    - Runs on every push or pull request


2. **Botcity CI-CD** `(.github/workflows/full-pipeline.yaml)`
For projects with automated deployment to BotCity.
    
    Features:
    - All linting validations
    - Automatic deployment to botcity-dev branch
    - Versioned deployment to main branch
    - Automatic semantic versioning using GitHub tags
    - Automatic releases

### 🚦 How to Use

#### For linting only:
- Use the `inter.yaml` file
- Push to see the validations in action
- Remove `botcity-ci-cd.yaml` from `.github\workflows` folder

#### For local tests use these commands in your bash and fix your code:
```bash
# Basic code checking
ruff check .

# Return type validation (ignoring RET504)
ruff check . --select RET --ignore RET504

# Additional code quality checks
ruff check . --select ARG,C4,PD,ERA,SIM,N

# Docstring validation (with specific ignores)
pydocstyle --ignore=D100,D200,D401,D212,D400,D406,D407,D413,D415,D205,D203,D202 .
```

#### For the full pipeline:
- Use the `botcity-ci-cd.yaml` file
- Configure secrets in the repository
- Add your code to the src/ folder
- Adjust build.sh as needed

**Alternates in `botcity-ci-cd.yaml`**:
   - `botId`: Replace your-bot-id with your real BotCity bot ID
   - `technology`: Define the language (e.g., python, javascript)
   - `botPath`: Define the bot's file path
   - `version`: DSpecify the desired bot version


### 🔧 Deployment Configuration

`botcity-dev` **branch:**

- Automatic release to the same version (e.g., 1.2.4-T)
- Ideal for testing and development

`main` **branch:**
- Requires you update uyour version manually in `botcity-ci-cd.yaml` 
- Deployment with release
- For production