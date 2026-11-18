# Assignment 10

**Name:** Hussein Jawad

## Files

| File | Problem |
|---|---|
| `Hussein_Jawad_HW10_Problem1.ipynb` / `.html` | Problem 1: English request to SQL with the OpenAI API, JSON response |
| `Hussein_Jawad_HW10_Problem2.ipynb` / `.html` | Problem 2: DeepSeek-R1 running locally with Ollama, answer + chain of thought |
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

## Problem 2 - how to run it (on my own Windows computer, with Anaconda)

1. **Install Ollama:** download the Windows installer from <https://ollama.com/download>, run `OllamaSetup.exe`, and finish the install. Ollama then runs in the background (llama icon in the system tray).
2. **Open Anaconda Prompt** (after the install) and check Ollama:
   ```bash
   ollama --version
   ```
3. **Pull the model** (about 5.2 GB, shows a progress bar):
   ```bash
   ollama pull deepseek-r1:8b
   ```
4. **Install the Ollama Python library:**
   ```bash
   pip install ollama
   ```
5. **Open the notebook:** go to the folder with `Hussein_Jawad_HW10_Problem2.ipynb` and start Jupyter:
   ```bash
   jupyter notebook Hussein_Jawad_HW10_Problem2.ipynb
   ```
6. **Run all cells:** **Kernel → Restart Kernel and Run All Cells**. Step 5 (the question) can take one to a few minutes, because the model writes its whole chain of thought first.
7. **Save** the notebook (Ctrl+S).
8. **HTML version:**
   ```bash
   jupyter nbconvert --to html Hussein_Jawad_HW10_Problem2.ipynb
   ```

If Step 2 in the notebook shows less than about 8 GB of RAM available, change `MODEL` to `"deepseek-r1:1.5b"` and pull that tag instead.

### Troubleshooting

| Problem | Fix |
|---|---|
| `ollama` is not recognized | Jupyter was started before Ollama was installed: close Jupyter and Anaconda Prompt, open a new Anaconda Prompt and start Jupyter again |
| `Connection refused` / `Failed to connect to Ollama` | Ollama isn't running: start the Ollama app from the Start menu |
| `ollama ps` shows a large CPU share, very slow answer | The model doesn't fit in GPU memory. It still works, just slower; or use `deepseek-r1:1.5b` |
| `model "deepseek-r1:8b" not found` | Run the pull step again |

## Running locally (both problems)

```bash
pip install -r requirements.txt
```

Keep `.env` next to the notebooks. It's in `.gitignore`, so it never gets committed.
