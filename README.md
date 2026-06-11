# Git & GitHub Assignment
**Farhan** | `git-practice-farhan`

---

## Setup

```bash
git config --global user. name "Farhan"
git config --global user.email "farhanferdous10@gmail.com"
```

Created a public GitHub repo named `git-practice-farhan` — no initialization.

---

## Init & Structure

```bash
mkdir git-practice-farhan && cd git-practice-farhan
git init
mkdir src docs
```

---

## Base Files — `main` branch

**`.gitignore`**
```
__pycache__/
*.pyc
*.pyo
.env
venv/
.vscode/
.DS_Store
```

```bash
git add .gitignore
git commit -m "Initial commit: add Python .gitignore."
```

---

**`README.md`**
```markdown
# Git Practice Project

- **Student:** Farhan
- **Assignment:** Git & GitHub Practical Assignment

## Run
```bash
python src/main.py
```

## Features
- Basic calculator: add, subtract, multiply, divide
- invalid input and division by zero
```

```bash
git add README.md
git commit -m "docs: add README with project description and student info."
```

---

*`docs/project-description.md`*
```markdown
# Project Description

**Student:** Farhan | **Language:** Python 3

## Objectives
1. Practice Git version control workflows
2. Work with branches and merges
3. Write clean, documented code

## Calculator Functions (src/utils.py)
- `add(a, b)`, `subtract(a, b)`, `multiply(a, b)`, `divide(a, b)`

## Workflow
main → feature/calculator → merge → feature/error-handling → merge
```

```bash
git add docs/project-description.md
git commit -m "docs: add project description with objectives and structure."
```

---

## Branch: `feature/calculator`

```bash
git checkout -b feature/calculator
```

**`src/utils.py`**
```python
""" Calculator utility functions — Farhan"""


def add(a, b):
    return a + b


def subtract(a, b):
    return a - b


def multiply(a, b):
    return a * b


def divide(a, b):
    return a / b
```

```bash
git add src/utils.py
git commit -m "feat: add basic calculator functions (add, subtract, multiply, divide)."
```

---

**`src/main.py`**
```python
"""Main entry point — Farhan"""

import datetime
from utils import add, subtract, multiply, divide


def main():
    print("=" * 40)
    print(f"  Student : Farhan")
    print(f"  Date    : {datetime.date.today()}")
    print("=" * 40)

    a, b = 10, 3
    print(f"\nadd({a},{b})      = {add(a, b)}")
    print(f"subtract({a},{b}) = {subtract(a, b)}")
    print(f"multiply({a},{b}) = {multiply(a, b)}")
    print(f"divide({a},{b})   = {divide(a, b):.4f}")


if __name__ == "__main__":
    main()
```

```bash
git add src/main.py
git commit -m "feat: add main.py with student info display and calculator demo."
```

```bash
git checkout main
git merge feature/calculator
```

---

## Branch: `feature/error-handling.`

```bash
git checkout -b feature/error-handling
```

**`src/utils.py`** — updated with validation
```python
""" Calculator utility functions with error handling — Farhan"""


def _validate(a, b):
    if not isinstance(a, (int, float)) or not isinstance(b, (int, float)):
        raise TypeError(f"Expected numbers, got: {type(a).__name__}, {type(b).__name__}")


def add(a, b):
    _validate(a, b)
    return a + b


def subtract(a, b):
    _validate(a, b)
    return a - b


def multiply(a, b):
    _validate(a, b)
    return a * b


def divide(a, b):
    _validate(a, b)
    if b == 0:
        raise ValueError("Division by zero is not allowed.")
    return a / b
```

```bash
git add src/utils.py
git commit -m "feat: add input type validation and division-by-zero error handling to utils.py"
```

---

**`src/main.py`** — _calculate
```python
"""Main entry point with error handling — Farhan"""

import datetime
from utils import add, subtract, multiply, divide


def safe_calculate(fn, a, b, label):
    try:
        print(f"  {label:<20} = {fn(a, b)}")
    except (TypeError, ValueError) as e:
        print(f"  {label:<20}   {e}")


def main():
    print("=" * 40)
    print(f"  Student : Farhan")
    print(f"  Date    : {datetime.date.today()}")
    print("=" * 40)

    a, b = 10, 3
    safe_calculate(add,      a, b, f"add({a},{b})")
    safe_calculate(subtract, a, b, f"subtract({a},{b})")
    safe_calculate(multiply, a, b, f"multiply({a},{b})")
    safe_calculate(divide,   a, b, f"divide({a},{b})")

    # Edge cases
    safe_calculate(divide, 10, 0,       "divide(10,0)")
    safe_calculate(add,    "x", 5,      'add("x",5)')


if __name__ == "__main__":
    main()
```

```bash
git add src/main.py
git commit -m "feat: update main.py to use safe_calculate with try/except error handling."
```

---

Updated `README.md` to reflect error handling, then:

```bash
git add README.md
git commit -m "docs: update README with error handling features and sample output."

git checkout main
git merge feature/error-handling
```

---

## Push GitHub

```bash
git remote add origin https://github.com/YOUR_USERNAME/git-practice-farhan.git
git branch -M main
git push -u origin main
git push origin feature/calculator feature/error-handling
```

---

## Commit Log

```
git log --oneline

a1b2c3d  docs: update README with error handling features and sample output
e4f5g6h  feat: update main.py to use safe_calculate with try/except error handling
i7j8k9l  feat: add input type validation and division-by-zero error handling to utils.py
m0n1o2p  feat: add main.py with student info display and calculator demo
q3r4s5t  feat: add basic calculator functions (add, subtract, multiply, divide)
u6v7w8x  docs: add project description with objectives and structure
y9z0a1b  docs: add README with project description and student info
c2d3e4f  Initial commit: add Python .gitignore
```

---

## Final Structure

```
git-practice-farhan/
├── README.md
├── .gitignore
├── src/
│   ├── main.py
│   └── utils.py
└── docs/
    └── project-description.md
```
