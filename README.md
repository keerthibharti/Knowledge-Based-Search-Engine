# Knowledge-base Search Engine

## Setup Instructions
1. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

2. Run the API:
   ```bash
   uvicorn main:app --reload
   ```

3. Endpoints:
   - `/upload` → Upload documents
   - `/query` → Ask questions

4. Example query prompt:
   ```
   Using these documents, answer the user's question succinctly.
   ```
