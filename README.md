CVisionary: AI-Powered Resume & Job Matching System
CVisionary is an advanced, AI-driven platform designed to streamline the job application process for candidates. It intelligently parses resumes, extracts key information, generates professional summaries, infers career interests, and provides tailored job recommendations by matching candidate profiles with scraped job listings using large language models (LLMs).

✨ Features
Resume Parsing (ATS-Friendly): Utilizes AI (Google Gemini) to extract structured data (personal info, education, experience, skills, projects, certifications) from PDF, DOCX, DOC, and RTF resumes.

AI-Powered Resume Summarization: Automatically generates concise, professional summaries from parsed resume data.

Career Interest Inference: Infers broad career interests and job categories from the resume to guide job search.

Web Scraping (Scrapy): Scrapes job listings from specified job portals (currently configured for merojob.com) and stores them in a MySQL database.

Intelligent Job Matching:

LLM-Based Matching: Leverages LLMs (Ollama) to perform a detailed analysis of resume content against job descriptions, providing a match score, suitability reasoning, and improvement suggestions.

Keyword-Based Pre-scoring: Filters and prioritizes job listings based on keyword similarity before detailed LLM analysis for efficiency.

User Authentication: Integrates with Firebase for secure user login and signup.

Downloadable Reports: Allows users to download their parsed resume data as a PDF and LLM-recommended jobs as a JSON file.

User-Friendly Web Interface: Built with Flask, providing an intuitive experience for uploading resumes and viewing results.

🚀 Getting Started
These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

Prerequisites
Before you begin, ensure you have the following installed:

Python 3.9+

pip (Python package installer)

MySQL Database Server: Make sure MySQL is running and you have a user with appropriate permissions (e.g., root with password my$qlayush1 as configured in helpers.py and pipelines.py).

Ollama: Install Ollama and pull the llama3.2 model (or your preferred compatible LLM).

Download Ollama from ollama.com.

Run ollama run llama3.2 in your terminal to download the model.

Firebase Project:

Create a Firebase project on the Firebase Console.

Generate a Firebase Admin SDK private key. Download the JSON file and rename it to cvisionary-d034a-firebase-adminsdk-fbsvc-dca53ec298.json (or update the filename in app.py) and place it in the root directory of your project.

Google Gemini API Key:

Obtain an API key from the Google AI Studio.

Set this key as an environment variable GEMINI_API_KEY. (e.g., in a .env file or directly in your system environment).

Installation
Clone the repository:

git clone https://github.com/your-username/CVisionary.git
cd CVisionary

Create a virtual environment (recommended):

python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

Install dependencies:

pip install -r requirements.txt

Database Setup:
The pipelines.py script will automatically create the jobs table in your MySQL database if it doesn't exist when the Scrapy spider is run for the first time. Ensure your MySQL server is running and accessible with the credentials specified in helpers.py and pipelines.py.

Database Name: jobs

User: root

Password: my$qlayush1 (Please change this to a strong password in a production environment and use environment variables for sensitive data!)

Running the Application
Start Ollama: Ensure your Ollama server is running and the llama3.2 model is available.

ollama serve

Set environment variables:

export GEMINI_API_KEY="YOUR_GOOGLE_GEMINI_API_KEY"
# For Flask secret key (IMPORTANT for production)
export FLASK_SECRET_KEY="a_very_strong_random_secret_key"

(Alternatively, create a .env file in the root directory with these variables.)

Run the Flask application:

python app.py

The application will typically run on http://127.0.0.1:5000/.

📂 Project Structure
CVisionary/
├── app.py                      # Main Flask application
├── config.py                   # Configuration settings (upload folder, file limits, LLM settings)
├── requirements.txt            # Python dependencies
├── cvisionary-d034a-firebase-adminsdk-fbsvc-dca53ec298.json # Firebase Admin SDK key
├── uploads/                    # Directory for temporary uploaded files (created automatically)
├── models/
│   └── job_matcher.py          # Handles job matching logic, LLM interaction (Ollama), and Scrapy integration
├── resume_scraper/
│   └── resume_parser.py        # Handles resume text extraction (PyPDF) and AI parsing (Google Gemini)
├── utils/
│   └── helpers.py              # Utility functions (DB connection, file validation, job data fetching)
├── jobscraping/                # Scrapy project for job listing scraping
│   ├── jobscraping/
│   │   ├── __init__.py
│   │   ├── items.py            # Defines Scrapy Items for job data
│   │   ├── middlewares.py      # Scrapy middlewares
│   │   └── pipelines.py        # Scrapy pipelines (for saving to MySQL)
│   │   └── spiders/
│   │       └── jobspider.py    # Scrapy spider for job listing websites (e.g., merojob.com)
│   ├── scrapy.cfg              # Scrapy project configuration
├── templates/                  # HTML templates for Flask
│   ├── index.html
│   ├── features.html
│   ├── login-signup.html
│   ├── howitworks.html
│   ├── pricing.html
│   ├── about-us.html
│   ├── contact-us.html
│   ├── activity2.html
│   ├── upload.html             # Resume upload page
│   ├── result.html             # Displays parsed resume and job matching results
│   └── resume_pdf_template.html # Template for PDF export of parsed resume
└── static/                     # Static files (CSS, JS, images)
    └── css/
    └── js/
    └── img/

🛠️ Usage
Navigate to the home page: Open http://127.0.0.1:5000/ in your browser.

Login/Signup: Use the Firebase authentication system to create an account or log in.

Upload Resume: Go to the /upload page and upload your resume (PDF, DOCX, DOC, RTF).

View Results: After processing, you will be redirected to the /results page, which displays:

Your parsed resume data.

An AI-generated summary of your resume.

LLM-powered job recommendations with match scores, reasoning, and improvement suggestions.

Matches from scraped job listings (if available and enabled).

Download: Download your parsed resume as a PDF or the LLM-recommended jobs as a JSON file.

⚙️ Configuration
The config.py file contains important configuration settings:

UPLOAD_FOLDER: Directory where uploaded resumes are temporarily stored.

MAX_CONTENT_LENGTH: Maximum allowed file size for uploads.

ALLOWED_EXTENSIONS: Supported resume file types.

TOP_N_FOR_LLM: Number of top pre-filtered jobs to send to the LLM for detailed ranking.

DEFAULT_JOB_SCRAPE_URL: The URL used by the Scrapy spider.

Important: For production environments, ensure you:

Change app.secret_key in app.py to a strong, random value.

Use environment variables for sensitive information like database credentials and API keys instead of hardcoding them.

Set debug=False in app.run().

