# Client Onboarding Consistency Checker

Automated KYC check for private banking. For each new client, the system reads
four documents, cross checks every field between them and decides whether to
accept or reject the client.

> SwissHacks 2025 · Julius Baer Challenge · Finalist\
> Team: Bilal Moussaoui El Azrak, Xinshen Xiang Chen, Pau López Pujals,
> Anouar El Haddadi El Yahyati

## About the project

Before a bank onboards a client, an employee checks that the client's documents
tell the same story: same name, same passport number, same address, same job.
The challenge turned this into a game. An API sent client cases one by one,
each with four documents, and teams scored points for every correct accept or
reject decision.

## How it works

1. The program requests a new client from the challenge API.
2. Each document is decoded and its fields are extracted:
   * **Passport** (image): OCR with Tesseract after image preprocessing.
   * **Account opening form** (PDF): form fields read with PyPDF2.
   * **Client profile** (Word): text read from the document XML and parsed
     field by field.
   * **Description** (free text): an LLM extracts the facts it mentions.
3. Every field is checked against the value found in the other documents.
   Differences only in casing or accents count as minor. Different values count
   as inconsistencies. Free text fields like education and employment are
   compared by an LLM.
4. The client is accepted if no inconsistencies are found, and the decision is
   sent back to the API.

## Tech stack

* **Language:** Python
* **Document processing:** Tesseract OCR, Pillow, PyPDF2, PyMuPDF, lxml
* **AI:** Llama 4 Maverick through OpenRouter
* **Other:** REST API client with requests, unidecode

The challenge API is no longer available, so the code can't be run today.
