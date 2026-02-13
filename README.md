Quick Start Guide
Step 1: Install Python Requirements

Open your terminal and run:

bashpip install pandas litellm google-genai boto3 python-dotenv


### Step 2: Get Your API Keys

You need two things:

**A) Google Gemini API Key**
1. Go to https://aistudio.google.com/app/apikey
2. Click "Create API Key"
3. Copy the key

**B) AWS Credentials**
1. Log into AWS Console
2. Go to IAM > Users > Your User > Security Credentials
3. Create Access Key
4. Copy both the Access Key ID and Secret Access Key

### Step 3: Create Your `.env` File

Create a file named `.env` in the same folder as your code:
```
API_KEY=paste_your_gemini_key_here
AWS_ACCESS_KEY=paste_your_aws_access_key_here
AWS_SECRET_KEY=paste_your_aws_secret_key_here
Important: Replace the placeholder text with your actual keys!

Step 4: Update the Bucket Name
In the code, find this line and change it to your S3 bucket name:
pythonBUCKET_NAME = "linqia-video-analyser-bucket"  # Change this to YOUR bucket name
If your bucket is in a different region than us-east-2, also update:
pythonvideo_urls = get_public_s3_urls(BUCKET_NAME, AWS_ACCESS_KEY, AWS_SECRET_KEY, region="your-region")

Step 5: Run the Code
If using Jupyter Notebook:

Open the notebook
Run all cells

If using a Python script:
bashpython video_analysis.py
```

---

## What Happens When You Run It

1. ✅ Connects to your S3 bucket
2. ✅ Finds all video files (.mp4, .mov, .avi, .mkv)
3. ✅ Analyzes each video with AI
4. ✅ Saves individual JSON files for each video
5. ✅ Creates a summary CSV spreadsheet

**Output location:** A folder called `testing_20` will be created with all results.

---

## Example Output

After running, you'll get:
```
testing_20/
├── video1_analysis.json
├── video2_analysis.json
├── video3_analysis.json
└── video_analysis_summary_20.csv  ← Open this in Excel!

Common Issues & Fixes
"No module named 'litellm'"
Fix: Run pip install litellm
"No credentials found"
Fix:

Make sure your .env file is in the same folder as your code
Check that you didn't add any extra spaces in the .env file
Verify the keys are correct

"Access Denied" to S3
Fix:

Make sure your AWS user has permission to access the S3 bucket
Check that the bucket name is spelled correctly
Verify the region is correct

Videos aren't being found
Fix:

Check that videos are in formats: .mp4, .mov, .avi, or .mkv
Make sure the bucket isn't empty
Verify the bucket name is correct


Customize the Output Folder
To save results to a different folder, change this line:
pythonresults, analysis_df = analyze_s3_videos_with_csv(video_urls, output_folder="my_folder_name")
```

---