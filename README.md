[langchain_environment_setup_guide.md](https://github.com/user-attachments/files/28175222/langchain_environment_setup_guide.md)
# LangChain Project Setup Guide — Windows PowerShell + VS Code

## Goal
Is guide me hum zero se ek clean LangChain project setup karenge:

1. Project directory banana
2. Virtual environment (`venv`) banana aur activate karna
3. `requirements.txt` file create karna
4. Packages install karna
5. VS Code me correct Python interpreter select karna
6. Python file bana kar LangChain import verify karna

---

## Important Naming Rules

In mistakes ko avoid karna hai:

- Python file ka naam **`langchain.py`** mat rakhna, warna installed LangChain library se conflict hoga.
- Code files ko **`__pycache__`** folder ke andar mat rakhna. Ye Python ka auto-generated cache folder hota hai.
- Requirement file ka standard naam **`requirements.txt`** rakhenge. Agar tumhari existing file `requirement.txt` hai, use rename karke `requirements.txt` kar do.

---

# Step 1: VS Code Me Terminal Open Karo

VS Code me:

```text
Terminal → New Terminal
```

Terminal PowerShell me open hona chahiye.

---

# Step 2: Documents Folder Me Jao

PowerShell terminal me ye command run karo:

```powershell
cd C:\Users\H.Shaikh\Documents
```

---

# Step 3: Project Directory Create Karo

Naya project folder banao:

```powershell
mkdir LANGCHAIN_MODELS
```

Us folder ke andar jao:

```powershell
cd LANGCHAIN_MODELS
```

Confirm karne ke liye current location check karo:

```powershell
pwd
```

Expected location:

```text
C:\Users\H.Shaikh\Documents\LANGCHAIN_MODELS
```

---

# Step 4: Virtual Environment Create Karo

Project folder ke andar ye command run karo:

```powershell
python -m venv venv
```

Is command ke baad project me `venv` naam ka folder create ho jayega.

Check karne ke liye:

```powershell
ls
```

Expected:

```text
venv
```

### Virtual Environment Kya Hai?

`venv` ek isolated Python environment hai. Is project ke packages isi ke andar install honge, global Python me mix nahi honge.

---

# Step 5: Virtual Environment Activate Karo

PowerShell me exact command:

```powershell
.\venv\Scripts\Activate.ps1
```

Successful activate hone ke baad terminal ke start me `(venv)` dikhna chahiye:

```text
(venv) PS C:\Users\H.Shaikh\Documents\LANGCHAIN_MODELS>
```

### Important

Har baar jab project par kaam start karo, terminal me pehle venv activate karna hoga:

```powershell
.\venv\Scripts\Activate.ps1
```

---

# Step 6: Pip Upgrade Karo

`(venv)` active hone ke baad pip upgrade karo:

```powershell
python -m pip install --upgrade pip
```

### Why `python -m pip`?

Ye ensure karta hai ki package isi activated virtual environment me install ho.

---

# Step 7: `requirements.txt` File Create Karo

Project root folder me file create karo:

```powershell
New-Item requirements.txt
```

Ab VS Code Explorer me `requirements.txt` open karo aur niche wala content paste karo:

```txt
# LangChain Core
langchain
langchain-core

# OpenAI Integration
langchain-openai
openai

# Anthropic Integration
langchain-anthropic

# Google Gemini Integration
langchain-google-genai
google-generativeai

# Hugging Face Integration
langchain-huggingface
transformers
huggingface-hub

# Environment Variable Management
python-dotenv

# Machine Learning Utilities
numpy
scikit-learn
```

File save karna mat bhoolna:

```text
Ctrl + S
```

### Expected Structure Abhi Tak

```text
LANGCHAIN_MODELS/
│
├── venv/
└── requirements.txt
```

---

# Step 8: Requirements File Se Packages Install Karo

Ensure karo terminal me `(venv)` dikh raha hai. Phir run karo:

```powershell
python -m pip install -r .\requirements.txt
```

### Command Samjho

```text
python -m pip install -r .\requirements.txt
```

- `python` = current virtual environment ka Python
- `-m pip` = Python se pip run karna
- `install` = package install karna
- `-r` = file ke andar listed packages read karna
- `.\requirements.txt` = dependency file ka path

### Common Wrong Commands

Ye wrong hai:

```powershell
python -m pip install .\requirements.txt
```

Kyunki isme `-r` missing hai.

Ye bhi wrong hai:

```powershell
pip install -m .\requirements.txt
```

Kyunki `-m` pip ke baad nahi, `python` ke baad use hota hai; aur requirements file ke liye `-r` chahiye.

---

# Step 9: Packages Verify Karo

Installation complete hone ke baad run karo:

```powershell
python -m pip list
```

Specific LangChain package check karne ke liye:

```powershell
python -m pip show langchain
```

Expected: package name, version aur virtual environment ka location show hona chahiye.

---

# Step 10: Application Folder Create Karo

Project code alag folder me rakhne ke liye `app` folder banao:

```powershell
mkdir app
```

App folder ke andar test file create karo:

```powershell
New-Item .\app\test_langchain.py
```

### Important

File ka naam inme se kuch rakh sakte ho:

```text
test_langchain.py
main.py
app.py
```

File ka naam kabhi bhi ye mat rakhna:

```text
langchain.py
```

---

# Step 11: LangChain Import Test Code Likho

VS Code me `app/test_langchain.py` open karo aur ye code paste karo:

```python
import langchain
from importlib.metadata import version

print("LangChain imported successfully!")
print("LangChain version:", version("langchain"))
print("Loaded from:", langchain.__file__)
```

Save karo:

```text
Ctrl + S
```

---

# Step 12: Test File Run Karo

Tum project root folder me ho aur `(venv)` active hai. Run karo:

```powershell
python .\app\test_langchain.py
```

Expected output kuch is type ka hoga:

```text
LangChain imported successfully!
LangChain version: <installed-version>
Loaded from: C:\Users\H.Shaikh\Documents\LANGCHAIN_MODELS\venv\Lib\site-packages\langchain\__init__.py
```

Agar loaded path me `venv\Lib\site-packages\langchain` aa raha hai, matlab setup correct hai.

---

# Step 13: VS Code Me Correct Interpreter Select Karo

Ye important hai, warna VS Code run button se global Python run kar sakta hai aur error aa sakta hai:

```text
ModuleNotFoundError: No module named 'langchain'
```

VS Code me:

1. `Ctrl + Shift + P` press karo
2. Search karo: `Python: Select Interpreter`
3. Apne project ka ye interpreter select karo:

```text
LANGCHAIN_MODELS\venv\Scripts\python.exe
```

Ab VS Code ka Run button bhi isi virtual environment se code execute karega.

---

# Final Project Structure

```text
LANGCHAIN_MODELS/
│
├── venv/                        # Virtual environment; GitHub par push nahi karna
│
├── requirements.txt             # Required Python packages
│
└── app/
    └── test_langchain.py        # LangChain installation/import verification
```

---

# Optional but Recommended: `.gitignore` Create Karo

Agar project GitHub par push karna hai, `venv` aur Python cache push nahi karna chahiye.

Project root me `.gitignore` file create karo:

```powershell
New-Item .gitignore
```

Iske andar paste karo:

```gitignore
# Virtual Environment
venv/

# Python Cache
__pycache__/
*.pyc

# Environment Variables / API Keys
.env
```

Save karo:

```text
Ctrl + S
```

Ab project structure:

```text
LANGCHAIN_MODELS/
│
├── venv/
├── app/
│   └── test_langchain.py
├── requirements.txt
└── .gitignore
```

---

# All Commands Together — Copy/Paste Reference

> Commands ek-ek karke run karo. `requirements.txt` me package list paste aur save karna manually required hai.

```powershell
# Go to Documents
cd C:\Users\H.Shaikh\Documents

# Create and enter project directory
mkdir LANGCHAIN_MODELS
cd LANGCHAIN_MODELS

# Create virtual environment
python -m venv venv

# Activate virtual environment
.\venv\Scripts\Activate.ps1

# Upgrade pip
python -m pip install --upgrade pip

# Create requirements file
New-Item requirements.txt

# After pasting and saving package list in requirements.txt, install packages
python -m pip install -r .\requirements.txt

# Verify LangChain installation
python -m pip show langchain

# Create application folder and test file
mkdir app
New-Item .\app\test_langchain.py

# After pasting and saving test code, run the file
python .\app\test_langchain.py

# Create gitignore file for GitHub project
New-Item .gitignore
```

---

# Error Troubleshooting Notes

## Error 1: `The term 'venv\Script\Activate' is not recognized`

Wrong command:

```powershell
venv\Script\Activate
```

Correct command:

```powershell
.\venv\Scripts\Activate.ps1
```

Reason: Folder name `Scripts` plural hai aur PowerShell activate file `Activate.ps1` hai.

---

## Error 2: `Invalid requirement: '.\requirements.txt'`

Wrong command:

```powershell
python -m pip install .\requirements.txt
```

Correct command:

```powershell
python -m pip install -r .\requirements.txt
```

Reason: `-r` flag pip ko batata hai ki file ke andar packages listed hain.

---

## Error 3: `ModuleNotFoundError: No module named 'langchain'`

Possible reason: VS Code global Python use kar raha hai, virtual environment wala Python nahi.

Fix:

1. `(venv)` activate karo.
2. VS Code me `Python: Select Interpreter` se `venv\Scripts\python.exe` select karo.
3. Terminal me run karo:

```powershell
python .\app\test_langchain.py
```

---

## Error 4: Local File Conflict With Installed Package

Agar Python file ka naam `langchain.py` rakha, to import issue aa sakta hai.

Wrong:

```text
app/langchain.py
```

Correct:

```text
app/test_langchain.py
```

Agar pehle wrong name se file banayi thi, rename karne ke baad cache delete karo:

```powershell
Remove-Item -Recurse -Force .\app\__pycache__ -ErrorAction SilentlyContinue
```

---

# Completion Checklist

- [ ] `LANGCHAIN_MODELS` project directory created
- [ ] `venv` created
- [ ] Virtual environment activated and `(venv)` visible in terminal
- [ ] `requirements.txt` created and saved with package names
- [ ] Packages installed using `python -m pip install -r .\requirements.txt`
- [ ] `app/test_langchain.py` created
- [ ] LangChain import test successfully executed
- [ ] VS Code interpreter changed to `venv\Scripts\python.exe`
- [ ] `.gitignore` created before GitHub commit

---

# Next Step After This Setup

Jab import test successful run ho jaye, next step hoga:

1. `.env` file create karna
2. API key securely store karna
3. LangChain ke through first model call run karna
4. GitHub par project ka initial commit push karna

