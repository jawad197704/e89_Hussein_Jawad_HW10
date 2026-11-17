# CSCI E-89 Deep Learning, Assignment 10: Problem 1

**Student:** Hussein Jawad
**Problem 1:** Use the OpenAI Python API to turn an English request into SQL, and return the result as a JSON response.

> *"Select all customers who are born in either June, July, October, live in Boston, are senior citizens and hence qualify for Medicare benefit"*

The solution uses the Lecture 10 / Lab 10 material: the slides (OpenAI account and API key), **OpenAI Notebook 1** (prompting principles; temperature, top_p and reasoning effort) and **OpenAI Notebook 2** (SQL generation with the schema in the system message, then verifying the SQL).

## Files

| File | Purpose |
|---|---|
| `Hussein_Jawad_HW10_Problem1.ipynb` | The solution notebook (parts a–d), with an explanation before every step |
| `requirements.txt` | Python packages to install |
| `.env.example` | Template for your `.env` file (API key and key name) |
| `results/` | The notebook writes the documented JSON response and experiment results here |
| `images/` | Put your API-key screenshot here |

## How the solution works

| Part | What the notebook does |
|---|---|
| **Account / key** | Step 0 repeats the Lab 10 slide 9–10 steps. The key and its name are stored in `.env`, and only a masked version is printed. |
| **a)** | `%pip install --upgrade openai python-dotenv pandas`, then prints the library version. |
| **b)** | *Baseline:* the Notebook 2 pattern (schema in the system message, request in the user message, `temperature=0`). *Engineered:* a prompt built with the Notebook 1 tactics (delimiters, structured output, condition check, "work it out first") that targets SQLite. |
| **c)** | Every query is **run on a small SQLite test database** and compared with ground truth computed in Python (Notebook 2: *"Don't trust generated SQL. Verify it."*). A grid of 11 configurations × 3 runs compares baseline and engineered prompts, `gpt-5.4` and `gpt-5.4-mini`, temperature 0 / 0.7 / 1.5 / 2.0, `top_p=0.1`, and reasoning effort low/medium. It reports accuracy, whether the SQL runs, whether the JSON is valid, how many distinct queries each setting produces, tokens and latency. |
| **d)** | The answer is forced to be JSON with **Structured Outputs** (`text.format = json_schema, strict: true`). The full API response is shown with `show_json` and saved to `results/problem1_final_response.json` and `results/problem1_full_api_response.json`. |

My reference answer (hand-written; the notebook uses it to check that the grader works):

```sql
SELECT *
FROM Customers
WHERE CAST(strftime('%m', DateOfBirth) AS INTEGER) IN (6, 7, 10)   -- June, July, October
  AND City = 'Boston' AND State = 'MA'                             -- lives in Boston
  AND DateOfBirth <= date('now', '-65 years');                     -- age >= 65 -> Medicare
```

---

## Step-by-step: what you need to do on your machine

The notebook calls the OpenAI API with **your** key, so it must be run on your computer. It was not executed when the repository was prepared: there was no key available, and putting a key in the repository would be unsafe. The plumbing was checked offline with a mock client. Everything below takes about 15 minutes; the API calls cost only a few cents.

### 1. Create the OpenAI account and API key (Lab 10, slides 9–10)
1. Sign up at <https://platform.openai.com/signup> (email address and phone number).
2. Add credits under **Settings → Organization → Billing** (<https://platform.openai.com/settings/organization/billing/overview>). API usage is billed separately from ChatGPT Plus.
3. Open **API keys → Create new secret key**, name it **`e89-hw10-key`** (or any name you like), and click *Create*.
4. **Copy the key right away.** It is shown only once.
5. Take a screenshot of the API-keys page that shows the **key name** (the secret is masked there). Save it as `images/api_key.png`.

### 2. Get the code and install the libraries (part a)
```bash
git clone https://github.com/jawad197704/e89_Hussein_Jawad_HW10.git
```
```bash
cd e89_Hussein_Jawad_HW10
```
```bash
python -m venv .venv && source .venv/bin/activate
```
(On Windows: `.venv\Scripts\activate`)
```bash
pip install -r requirements.txt
```
The notebook's first code cell also runs `%pip install --upgrade openai python-dotenv pandas`, as shown in the lecture.

### 3. Save the key and its name in `.env`
```bash
cp .env.example .env
```
Open `.env` and paste your key:
```
OPENAI_API_KEY=sk-...your key...
OPENAI_KEY_NAME=e89-hw10-key
```
`.env` is in `.gitignore`, so it is **never committed**. Never paste the key into the notebook.

### 4. Run the notebook
```bash
jupyter notebook Hussein_Jawad_HW10_Problem1.ipynb
```
Then use **Kernel → Restart & Run All**. Check these points:
- **Step 1:** prints the key name and a masked key (`sk-...abcd`), and shows `available: True` for both models. If a model is missing, change `MODEL` / `SMALL_MODEL` in that cell to a model your key lists. You can print the list with the model-listing cell from Notebook 1.
- **Step 3:** the JSON answer should list the conditions, including the assumption **age ≥ 65 for Medicare**.
- **Step 4:** the engineered SQL should show `'correct': True`. The baseline usually fails on SQLite because it uses MySQL/PostgreSQL functions; this is expected and is discussed in the notebook.
- **Step 5:** the experiment table (about 33 short API calls).
- **Step 6:** the final JSON response, saved in `results/`.

In Step 0, replace the line `[insert screenshot images/api_key.png here]` with:
```
![API key](images/api_key.png)
```

If an experiment configuration gets an API error (for example, a model that does not accept a parameter), it is recorded in the table with the error message instead of stopping the notebook.

### 5. Make the HTML version (required by the assignment)
```bash
jupyter nbconvert --to html Hussein_Jawad_HW10_Problem1.ipynb
```
If an output is very long, the assignment asks you to copy its first and/or last lines into a Markdown cell and delete the long output. The `show_json(final_response)` cell is the most likely candidate.

### 6. Commit your results (without the key)
```bash
git add Hussein_Jawad_HW10_Problem1.ipynb Hussein_Jawad_HW10_Problem1.html results/ images/
```
```bash
git commit -m "Problem 1: executed notebook, HTML and JSON results"
```
```bash
git push origin main
```
Before you push, check with `git status` that `.env` is **not** listed.
