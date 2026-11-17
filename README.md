# Assignment 10 - Problem 1

**Name:** Hussein Jawad

Turning an English request into SQL with the OpenAI API and returning the result as JSON:

> "Select all customers who are born in either June, July, October, live in Boston, are senior citizens and hence qualify for Medicare benefit"

## Files

- `Hussein_Jawad_HW10_Problem1.ipynb` - the notebook with all outputs (run in Google Colab)
- `Hussein_Jawad_HW10_Problem1.html` - HTML version of the notebook
- `requirements.txt` - Python packages
- `.env.example` - template for the `.env` file with the API key
- `images/` - screenshots

## How to run it (Google Colab)

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

## Running it locally

```bash
pip install -r requirements.txt
```
```bash
jupyter notebook Hussein_Jawad_HW10_Problem1.ipynb
```

Keep `.env` next to the notebook. It's in `.gitignore`, so it never gets committed.
