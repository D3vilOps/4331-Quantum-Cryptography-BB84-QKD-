# BB84 Quantum Key Distribution — README

## Project Overview
This project simulates the BB84 Quantum Key Distribution (QKD) protocol using IBM's Qiskit framework. It demonstrates how quantum mechanics can be used to generate truly random cryptographic keys and detect eavesdropping through measurable error rates.

---

## System Requirements

- **Operating System:** Windows 10/11, macOS 12+, or Linux (Ubuntu 20.04+)
- **Python Version:** 3.9 or higher
- **RAM:** 8GB minimum recommended
- **Disk Space:** ~500MB for packages and environment

---

## Required Software

### 1. Python
Download and install Python 3.9 or higher from [python.org](https://www.python.org/downloads/).
During installation on Windows, check **"Add Python to PATH"**.

### 2. Visual Studio Code (Recommended)
Download from [code.visualstudio.com](https://code.visualstudio.com).
Install the following VS Code extensions:
- **Python** (by Microsoft)
- **Jupyter** (by Microsoft)

### 3. Required Python Packages
All packages are installed via pip inside a virtual environment (see setup below):

| Package | Version | Purpose |
|---|---|---|
| `qiskit` | >=1.0 | Core quantum computing SDK — builds and manages quantum circuits |
| `qiskit-ibm-runtime` | latest | Connects to IBM Quantum hardware and cloud services |
| `qiskit-aer` | latest | High-performance local quantum circuit simulator |
| `jupyterlab` | latest | Browser-based notebook interface (optional if using VS Code) |
| `matplotlib` | latest | Visualization — circuit diagrams and result graphs |

---

## Setup Instructions

### Step 1 — Create Project Folder
```bash
mkdir quantum-crypto
cd quantum-crypto
```

### Step 2 — Create a Virtual Environment
**Windows (PowerShell):**
```powershell
# If scripts are disabled, run this first:
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser

python -m venv qiskit-env
qiskit-env\Scripts\Activate.ps1
```

**macOS/Linux:**
```bash
python3 -m venv qiskit-env
source qiskit-env/bin/activate
```

You will know the environment is active when your terminal prompt shows:
```
(qiskit-env) PS C:\Users\...\quantum-crypto>
```

### Step 3 — Install All Packages
Run this single command inside the activated environment:
```bash
pip install 'qiskit>=1' qiskit-ibm-runtime qiskit-aer jupyterlab matplotlib
```

### Step 4 — Connect to IBM Quantum
1. Create a free account at [quantum.ibm.com](https://quantum.ibm.com)
2. Copy your API token from your profile page
3. Open Python and run:
```python
from qiskit_ibm_runtime import QiskitRuntimeService

QiskitRuntimeService.save_account(
    channel="ibm_quantum_platform",
    token="YOUR_API_TOKEN_HERE",
    overwrite=True
)
```
This only needs to be done once — your token is saved locally for future sessions.

### Step 5 — Open the Notebook in VS Code
1. Open VS Code
2. Click **File → Open Folder** and select your `quantum-crypto` folder
3. Press **Ctrl + Shift + P** → type **"Python: Select Interpreter"**
4. Select `qiskit-env (Python 3.x.x)` or enter the path manually:
   ```
   C:\Users\<your username>\quantum-crypto\qiskit-env\Scripts\python.exe
   ```
5. Open `bb84_demo.ipynb` from the left sidebar
6. Confirm the kernel in the top right shows `qiskit-env`

---

## Running the Notebook

Open `bb84_demo.ipynb` and click **"Run All"** in the toolbar, or run each cell
in order using **Shift + Enter**. Cells must always be run from top to bottom —
skipping cells will cause `NameError` since variables depend on previous cells.

### Expected Runtime
| Key Length | Estimated Runtime |
|---|---|
| 20 bits | ~2 seconds |
| 256 bits | ~10 seconds |
| 1024 bits | ~30-60 seconds |

---

## No Special Data Files Required
This project generates all data programmatically using quantum random number
generation. No external datasets or file paths are needed.

---

## Troubleshooting

| Error | Cause | Fix |
|---|---|---|
| `ModuleNotFoundError: No module named 'qiskit'` | Wrong Python interpreter selected | Select `qiskit-env` in VS Code interpreter selector |
| `NameError: name 'bob_bases' is not defined` | Cells run out of order | Run all cells from Cell 1 downward |
| `InvalidAccountError: invalid channel` | Outdated channel name | Use `channel="ibm_quantum_platform"` |
| PowerShell script blocked | Execution policy restriction | Run `Set-ExecutionPolicy RemoteSigned -Scope CurrentUser` |

---

## File Structure
```
quantum-crypto/
├── qiskit-env/          ← Virtual environment (do not edit)
├── bb84_demo.ipynb      ← Main experiment notebook
└── README.md            ← This file
```

---

## References
- Bennett, C.H. & Brassard, G. (1984). Quantum Cryptography: Public Key Distribution and Coin Tossing.
- IBM Quantum Documentation: [docs.quantum.ibm.com](https://docs.quantum.ibm.com)
- Qiskit GitHub: [github.com/Qiskit](https://github.com/Qiskit)
