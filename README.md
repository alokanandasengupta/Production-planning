# Film Script Production Breakdown

An AI-powered tool that turns a screenplay (pasted text or a scanned PDF)
into a structured production breakdown: every location, the scenes that
happen there, and the props each scene needs — the kind of breakdown a
production coordinator would otherwise build by hand, scene by scene.

## How it works

1. **Input**: paste script text directly, or upload a PDF — scanned pages
   are run through Mistral's OCR API first to extract text.
2. **Extraction**: the script is chunked and sent to OpenAI with a
   structured-output prompt (a system prompt framed as a "senior film
   production coordinator") that returns each chunk's locations, scenes,
   and props as JSON.
3. **Breakdown**: results are merged across chunks into a single
   location-by-location breakdown, plus a consolidated unique-props list
   for the whole script.
4. **Export**: the breakdown can be exported to Excel, Word, or PDF for
   handoff to a production team.

## Stack

Streamlit (UI), OpenAI API (extraction), Mistral OCR API (scanned-script
text extraction), `python-docx` / `openpyxl` / `reportlab` (exports),
`pdfplumber` / `PyPDF2` (PDF text extraction).

## Running it

```bash
pip install -r requirements.txt
streamlit run app.py
```

Needs `OPENAI_API_KEY` and `MISTRAL_API_KEY` set via Streamlit secrets
(`.streamlit/secrets.toml`) — the app reads them through `st.secrets`, never
hardcoded. The app includes a lightweight login gate (email-domain check);
it's a demo-grade access control, not production auth.
