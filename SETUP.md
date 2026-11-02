# Set up your lab: GPU Optimization for AI-ML Systems

When you finish, you will be able to run the labs for Modules 1 to 3 on your own laptop with plain Python. It takes about 10 minutes.

## What you need

- A laptop running macOS, Windows or Linux. You can also use GitHub Codespaces in a browser.
- **Python 3.9 or newer** and **git**.
- A free GitHub account, only if you use Codespaces or want to keep your work on GitHub.
- A few hundred MB of free disk. Most of it is for `numpy` in Module 2.
- Packages: Modules 1 and 3 use only the Python standard library, so there is nothing to install. Module 2 needs `numpy` (`pip install -r requirements.txt`).
- **No NVIDIA GPU is needed for Modules 1 to 3:**
  - Module 1: `gpu_snapshot.py` reads `nvidia-smi` live if your machine has a GPU. If it does not, it reads a recorded sample from four A100s instead.
  - Module 2: you shrink a real, laptop-sized model on your CPU with numpy.
  - Module 3: the serving labs are seeded simulators that model the scheduler. They are not GPU benchmarks.
- **Optional:** every lab has an Optional GPU track (nvidia-smi, DCGM, vLLM) for a machine with an NVIDIA GPU. A cloud GPU works. The course materials do not name a free GPU service.
- **No API keys** and no model downloads for the core labs.

## Step 1 · Pick where to run it

### Option A: GitHub Codespaces (any computer)
1. Sign in to github.com and open this repo.
2. Click **Code > Codespaces > Create codespace on main**.
3. Python and git are already installed. Check with `python3 --version`.

### Option B: Windows (PowerShell)
1. Install Python and git with winget, which comes with Windows 11:
```powershell
winget install Python.Python.3.12
winget install Git.Git
```
2. Close PowerShell, open it again, and check with `py --version`.
3. On Windows, type `py` wherever this guide says `python3`. WSL Ubuntu also works if you prefer Linux. In that case, follow the Linux commands.

### Option C: Mac (Terminal)
1. Install Homebrew first (https://brew.sh), then:
```bash
brew install python git
python3 --version
```

## Step 2 · Get the lab files

Download [gpu-ai-optimization-labs.zip](downloads/gpu-ai-optimization-labs.zip) from the `downloads/` folder of this repo. Then unzip it and go into the folder.

macOS / Linux / Codespaces:
```bash
unzip gpu-ai-optimization-labs.zip
cd gpu-ai-optimization
```
Windows PowerShell:
```powershell
Expand-Archive gpu-ai-optimization-labs.zip -DestinationPath .
cd gpu-ai-optimization
```

## Step 3 · Install and check

Each module has its own folder under `labs/`. You make a virtual environment inside each one: a private box of Python packages for that lab.

macOS / Linux:
```bash
cd labs/module-1-measure
python3 -m venv .venv && source .venv/bin/activate
python3 --version
```
Windows PowerShell:
```powershell
cd labs\module-1-measure
py -m venv .venv; .venv\Scripts\Activate.ps1
py --version
```
You should see your prompt start with `(.venv)` and a version of `3.9` or newer. Module 1 needs nothing else.

## Step 4 · Quick test for each module

Run each test from the `gpu-ai-optimization` folder.

**Module 1 · Measure Before You Optimize**
```bash
cd labs/module-1-measure
python3 scorecard.py data/usage_baseline.csv --out reports/baseline.md
python3 gpu_snapshot.py --sample
```
You should see `chat-assistant   $0.952 per 1M tokens` and `! 17% of doc-summarizer spend bought zero requests.` After that, a 4-GPU table that flags GPU 2 as `IDLE` and GPU 3 as `THROTTLED`.

**Module 2 · Shrink the Model** (needs numpy)
```bash
cd labs/module-2-shrink
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python3 data/make_data.py
```
This takes about 20 to 60 seconds. It should end with `teacher: test accuracy 91.4% | rare slice 86.4% | saved data/teacher.npz`. Then run `python3 quantize.py`. The table should show `INT8 per-tensor` marked `<- moved`.

**Module 3 · Serve It Smarter**
```bash
cd labs/module-3-serve
python3 -m venv .venv && source .venv/bin/activate
python3 kv_calc.py --model llama-3-8b --context 8192 --users 32
```
You should see `KV per token   = 2 x 32 x 8 x 128 x 2 B = 131,072 B = 128 KiB` and `per sequence   = 128 KiB x 8,192 tokens = 1.00 GiB`.

## If something goes wrong

- **PowerShell will not run `Activate.ps1`**: run `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` once, then try again.
- **`python3` not found on Windows**: use `py` instead.
- **`ModuleNotFoundError: No module named 'numpy'`** (Module 2): activate the `.venv` in `labs/module-2-shrink`, then run `pip install -r requirements.txt`.
- **`gpu_snapshot.py` shows the recorded sample**: this is expected without an NVIDIA GPU. The lab works the same way.
- **Your numbers differ in the last digit**: everything is seeded, but different math libraries can move the last digit. The patterns will not change.
- **Stuck for more than 15 minutes?** Switch to Codespaces. It works the same way in any browser.

## Official guides

- GitHub Codespaces: https://docs.github.com/codespaces
- Python downloads: https://www.python.org/downloads/
- Homebrew: https://brew.sh
- Install WSL (optional on Windows): https://learn.microsoft.com/windows/wsl/install
