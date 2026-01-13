# Taurunner Installation Guide 

This repository documents a **stable, classroom-tested installation workflow** for running **Taurunner** with **PROPOSAL** on macOS.

> ⚠️ Important:  
> Taurunner depends on **specific versions** of Python, PROPOSAL, and CMake.  
> **Do NOT upgrade versions unless you know exactly what you are doing.**

---

## ✅ Reference Environment (Do Not Change)

This guide assumes the following environment:

- **OS**: macOS  
- **Python**: 3.10  
- **PROPOSAL**: 6.1.6  
- **CMake**: 3.20 – 3.27  
- **Compiler**: AppleClang (Xcode Command Line Tools)

This exact combination has been verified to work reliably.

---

## Part 0. System Prerequisites (One-Time Setup)

### 0.1 Install Xcode Command Line Tools

```bash
xcode-select --install
```
**Verify installation:**
```
xcode-select -p
```
**Expected output (example):**
```
/Library/Developer/CommandLineTools
```
## Part 1. Create Conda Environment
### 1.1 Create a new environment with Python 3.10
```
conda create -n taurunner310 python=3.10 -y
```

### 1.2 Activate the environment
```
conda activate taurunner310
```
### 1.3 Verify Python version and path
```
which python
python -V
```

**Expected:**
Python version: ```3.10.x```

Path contains: ```miniconda3/envs/taurunner310```

## Part 2. Install Build Tools (Critical)
### 2.1 Install CMake and Ninja (Version Locked)
```
conda install -c conda-forge -y "cmake>=3.20,<3.28" ninja
```

### 2.2 Verify CMake version
```
cmake --version
```

**Valid examples:**
```
cmake version 3.22.x
cmake version 3.25.x
cmake version 3.27.x
```

## Part 3. Install Python Dependencies
### 3.1 Install numerical libraries
```
python -m pip install numpy scipy
```
### 3.2 Install PROPOSAL (Pinned Version)
```
python -m pip install "proposal==6.1.6"
```

**Verify:**
```
python -c "import proposal; print(proposal.__version__)"
```

**Expected output:**
```
6.1.6
```

### 3.3 Install Taurunner
```
python -m pip install taurunner
```

## Part 4. Verification (Must Pass)
### 4.1 Import Test
```
python -c "import proposal, taurunner; print('proposal', proposal.__version__); print('taurunner ok')"
```

**Expected output:**
```
proposal 6.1.6
taurunner ok
```
### 4.2 Inspect Taurunner Modules (Optional)
```
python - <<'PY'
import taurunner, pkgutil
print("taurunner:", taurunner.__file__)
print("submodules:", [m.name for m in pkgutil.iter_modules(taurunner.__path__)])
PY
```

## Part 5. Command-Line Usage (Important)

- ⚠️ Taurunner does NOT install a standalone CLI binary

- ✅ Correct way to run Taurunner
  ```
  python -m taurunner.main --help
  ```

  <img width="1854" height="828" alt="image" src="https://github.com/user-attachments/assets/8f4079c7-d250-4634-a3c1-2307360f7f18" />











