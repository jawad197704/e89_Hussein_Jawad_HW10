# Assignment 10

**Name:** Hussein Jawad

## Files

| File | Problem |
|---|---|
| `Hussein_Jawad_HW10_Problem1.ipynb` / `.html` | Problem 1: English request to SQL with the OpenAI API, JSON response |
| `Hussein_Jawad_HW10_Problem2.ipynb` | Problem 2: DeepSeek-R1 running locally with Ollama, answer + chain of thought |
| `requirements.txt` | Python packages |
| `.env.example` | template for the `.env` file with the OpenAI API key (Problem 1) |

## Problem 1 - how to run it (Google Colab)

1. Put the repo folder in Google Drive as `MyDrive/CSCI-E-89-1-Deep-Learning/HW10`. If it's somewhere else, change `PROJECT_DIR` in the notebook.
2. Make a `.env` file in that folder (same folder as the notebook):
   ```
   OPENAI_API_KEY=sk-...
   OPENAI_KEY_NAME=e89-hw10-key
   ```
   On Windows, save it from Notepad as `".env"` with **Save as type: All Files**, then upload it to the Drive folder.
3. Open the notebook in Colab and run all cells (**Runtime → Run all**). The Drive cell asks for permission to mount Drive and then checks that `.env` is found.
4. Export to HTML by running this in a cell:
   ```bash
   !jupyter nbconvert --to html "/content/drive/MyDrive/CSCI-E-89-1-Deep-Learning/HW10/Hussein_Jawad_HW10_Problem1.ipynb"
   ```

## Problem 2 - how to run it

The assignment asks for Ollama on your own machine, so option A is the one that matches it. Option B (Colab) is a fallback if your computer has less than about 8 GB of free memory.

### Option A - on your own Windows computer (recommended)

1. **Install Ollama:** download the Windows installer from <https://ollama.com/download>, run `OllamaSetup.exe`, and finish the install. Ollama then runs in the background (llama icon in the system tray).
2. **Check it** in PowerShell:
   ```bash
   ollama --version
   ```
3. **Pull the model** (about 5.2 GB, a few minutes). Doing it here shows a progress bar; the notebook also pulls it, but this is quicker to watch:
   ```bash
   ollama pull deepseek-r1:8b
   ```
4. **Install Python and Jupyter** if you don't have them: install Python 3.11+ from <https://www.python.org/downloads/> (tick **Add python.exe to PATH**), then:
   ```bash
   pip install notebook ollama psutil
   ```
5. **Open the notebook:** in PowerShell, go to the folder with `Hussein_Jawad_HW10_Problem2.ipynb` and run:
   ```bash
   jupyter notebook Hussein_Jawad_HW10_Problem2.ipynb
   ```
6. **Run all cells:** **Kernel → Restart Kernel and Run All Cells**. Step 5 (the question) can take one to a few minutes, because the model writes its whole chain of thought first.
7. **Save** the notebook (Ctrl+S) and send it back so the observations can be written from the real results.
8. **HTML version:**
   ```bash
   jupyter nbconvert --to html Hussein_Jawad_HW10_Problem2.ipynb
   ```

If your machine shows less than 8 GB of RAM available in Step 2, change `MODEL` to `"deepseek-r1:1.5b"` (and pull that tag instead).

### Option B - Google Colab (if your computer is too small)

1. Upload `Hussein_Jawad_HW10_Problem2.ipynb` to your Drive folder and open it in Colab.
2. **Runtime → Change runtime type → T4 GPU** (or L4), then **Runtime → Run all**. The second code cell installs Ollama and starts it; the pull downloads the model into the Colab machine each session.
3. **File → Download → Download .ipynb** and send it back.

### Troubleshooting

| Problem | Fix |
|---|---|
| `ollama` is not recognized | Close and reopen PowerShell / Jupyter after the install, or restart the computer |
| `Connection refused` / `Failed to connect to Ollama` | Ollama isn't running: start the Ollama app from the Start menu |
| `ollama ps` shows a large CPU share, very slow answer | The model doesn't fit in GPU memory. It still works, just slower; or use `deepseek-r1:1.5b` |
| `model "deepseek-r1:8b" not found` | Run the pull step again |

## Running locally (both problems)

```bash
pip install -r requirements.txt
```

Keep `.env` next to the notebooks. It's in `.gitignore`, so it never gets committed.
