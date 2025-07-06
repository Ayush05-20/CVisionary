CVisionary: AI-Powered Resume & Job Matching System
CVisionary is an AI platform that helps job seekers by parsing resumes, generating summaries, inferring career interests, and providing tailored job recommendations by matching profiles with scraped job listings.

✨ Features
Resume Processing: Extracts key information and generates summaries from resumes (PDF, DOCX, DOC, RTF) using Google Gemini.

Job Matching: Uses Ollama LLMs to match resumes with scraped job listings, providing scores, reasoning, and improvement suggestions.

Job Scraping: Gathers job listings from websites like merojob.com into a MySQL database.

User Management: Secure login/signup via Firebase.

Reporting: Download parsed resume data (PDF) and AI job recommendations (JSON).

Web Interface: User-friendly Flask application.

🚀 Getting Started
Prerequisites
Python 3.9+ & pip

MySQL Database Server (with root user and password, or update credentials)

Ollama (with llama3.2 model installed)

Firebase Project (Admin SDK JSON key in root directory)

Google Gemini API Key (set as GEMINI_API_KEY environment variable)

Installation
Clone: git clone https://github.com/your-username/CVisionary.git && cd CVisionary

Virtual Environment: python -m venv venv && source venv/bin/activate

Install Dependencies: pip install -r requirements.txt

Database Setup: pipelines.py automatically creates the jobs table on first Scrapy run.

Running the Application
Start Ollama: ollama serve

Set Environment Variables:

export GEMINI_API_KEY="YOUR_GOOGLE_GEMINI_API_KEY"
export FLASK_SECRET_KEY="a_very_strong_random_secret_key"

Run Flask: python app.py (Access at http://127.0.0.1:5000/)
