# RecruitlyAI

	A smart recruitment platform designed to assist HR teams and recruiters in identifying the best-fit candidates for open roles. Leveraging advanced AI, it analyzes resumes in relation to job descriptions, delivering a clear match score and in-depth insights. This helps simplify and speed up the hiring process with more confidence and precision.


## Features

- Upload candidate resumes directly or via Google Drive links (both single files and folders)
- Support for PDF, DOCX, and TXT resume formats
- AI-powered candidate evaluation based on job requirements (using Google's Gemini model)
- Customizable qualification threshold for candidate filtering
- Comprehensive talent assessment results with detailed feedback
- Export assessment reports as CSV for integration with your ATS

## Setup Instructions

### 1. Clone the repository

```bash
git clone git@github.com:jamesoyanna/RecruitlyAI.git
cd ai_recruiter
```

### 2. Setting up virtual environment

```bash
# For Python 3 on macOS/Linux
python3 -m venv venv
source venv/bin/activate

# For Windows
python -m venv venv
venv\Scripts\activate
```

After activating the virtual environment, your command prompt should show `(venv)` at the beginning of the line, indicating that the virtual environment is active.

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Set up environment variables

Create a `.env` file in the root directory with the following content:

```
GEMINI_API_KEY=your_gemini_api_key_here
```

Replace `your_gemini_api_key_here` with your actual Google Gemini API key.

### 5. Set up Google Drive API credentials

#### A. Creating the Google Cloud Project and Credentials

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project:
   - Click on the project dropdown at the top of the page
   - Click "New Project"
   - Enter a name for your project and click "Create"

3. Enable the Google Drive API:
   - Select your project
   - Go to "APIs & Services" > "Library"
   - Search for "Google Drive API"
   - Click on "Google Drive API" and then "Enable"

4. Create service account credentials:
   - Go to "APIs & Services" > "Credentials"
   - Click "Create Credentials" > "Service Account"
   - Enter a name for your service account, optionally add a description
   - Click "Create and Continue"
   - For the role, select "Project" > "Editor" (or a more restrictive role if needed)
   - Click "Continue" and then "Done"

5. Generate a key for your service account:
   - On the Credentials page, click on the service account you just created
   - Go to the "Keys" tab
   - Click "Add Key" > "Create new key"
   - Choose "JSON" as the key type
   - Click "Create". This will download a JSON file containing your credentials

#### B. Setting up the credentials in the application

You have two options for setting up the credentials:

##### Option 1: Using Streamlit secrets (Recommended for deployment)

1. Create a `.streamlit` directory and a `secrets.toml` file inside it:

```bash
mkdir -p .streamlit
touch .streamlit/secrets.toml
```

2. Add your Google Drive credentials to the `secrets.toml` file:

```toml
[google_credentials]
type = "service_account"
project_id = "your-project-id"
private_key_id = "your-private-key-id"
private_key = "your-private-key"
client_email = "your-client-email"
client_id = "your-client-id"
auth_uri = "https://accounts.google.com/o/oauth2/auth"
token_uri = "https://oauth2.googleapis.com/token"
auth_provider_x509_cert_url = "https://www.googleapis.com/oauth2/v1/certs"
client_x509_cert_url = "your-client-cert-url"
```

Fill in the values from the JSON file you downloaded.

##### Option 2: Using environment variables (Recommended for local development)

Add the following to your `.env` file:

```
GOOGLE_DRIVE_TYPE=service_account
GOOGLE_DRIVE_PROJECT_ID=your-project-id
GOOGLE_DRIVE_PRIVATE_KEY_ID=your-private-key-id
GOOGLE_DRIVE_PRIVATE_KEY=your-private-key
GOOGLE_DRIVE_CLIENT_EMAIL=your-client-email
GOOGLE_DRIVE_CLIENT_ID=your-client-id
GOOGLE_DRIVE_AUTH_URI=https://accounts.google.com/o/oauth2/auth
GOOGLE_DRIVE_TOKEN_URI=https://oauth2.googleapis.com/token
GOOGLE_DRIVE_AUTH_PROVIDER_CERT_URL=https://www.googleapis.com/oauth2/v1/certs
GOOGLE_DRIVE_CLIENT_CERT_URL=your-client-cert-url
```

Fill in the values from the JSON file you downloaded.

#### C. Sharing Google Drive files with the service account

To access candidate resumes in Google Drive, you need to share them with the service account:

1. Find the `client_email` value in your credentials JSON file (it looks like `name@project-id.iam.gserviceaccount.com`)
2. In Google Drive, right-click on the file or folder you want to share
3. Click "Share"
4. Enter the service account email address
5. Set the permission to "Viewer" (or "Editor" if needed)
6. Click "Send"

### 6. Run the application

```bash
streamlit run app.py
```

## Usage

1. Enter the position requirements in the provided text area
2. Choose how to upload candidate resumes:
   - Upload files directly: Select and upload candidate resumes from your computer
   - Google Drive link: Provide a link to a Google Drive file or folder containing resumes
3. Adjust the qualification threshold using the slider
4. Click "Evaluate Candidates" to start the talent assessment process
5. View the assessment results, sorted by qualified and non-qualified candidates
6. Download the talent assessment report as a CSV file if needed

## Why Recruiters Love It

- **Save Time**: Cut down on resume screening by as much as 75%
- **Fair & Consistent**: Bring objectivity to your hiring process with standardized candidate evaluations
- **Actionable Insights**: Receive detailed reports highlighting each candidate’s strengths and growth areas
- **Flexible Criteria**: Tailor qualification benchmarks to match your hiring goals
- **Easy Integration**: Fits right into your current recruitment tools and ATS workflow

## Note

- The platform uses Google's advanced Gemini AI model for talent evaluation
- Supports common resume formats (PDF, DOCX, TXT)
- For Google Drive access, ensure the service account has proper access to the files/folders
- When using the private key in environment variables, you may need to replace newlines with "\n" 