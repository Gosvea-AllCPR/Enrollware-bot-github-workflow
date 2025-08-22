# Enrollware Bot

An automated Enrollware student data export tool with cloud deployment and Google Drive integration support.

## 🚀 Features

- **Automated Login**: Intelligently handles Enrollware system authentication
- **Smart Date Selection**: Automatically exports data from the last 30 days
- **Excel Export**: Exports student data to Excel format (.xlsx)
- **Cloud Deployment**: Supports GitHub Actions for automated daily runs
- **Google Drive Integration**: Optional automatic upload to Google Drive
- **Error Handling**: Robust error handling with screenshot capture on failure
- **Flexible Input**: Supports both paste and character-by-character input for better compatibility

## 📋 Prerequisites

- Node.js 18 or higher
- Google Chrome browser (for local runs)
- Valid Enrollware account credentials

## 🔧 Local Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/enrollware-bot.git
   cd enrollware-bot
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Configure environment variables:**
   Create a `.env` file in the root directory:
   ```env
   EW_USER=your_enrollware_username
   EW_PASS=your_enrollware_password
   
   # Optional: Google Drive integration
   GOOGLE_DRIVE_CREDENTIALS={"type":"service_account",...}
   GOOGLE_DRIVE_FOLDER_ID=your_folder_id
   ```

4. **Run the script:**
   ```bash
   npm start
   ```

## ☁️ Cloud Deployment (GitHub Actions)

### 1. Repository Setup

1. Create a new GitHub repository
2. Push your code to the repository:
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/your-username/enrollware-bot.git
   git push -u origin main
   ```

### 2. Configure GitHub Secrets

Go to your repository's **Settings > Secrets and variables > Actions** and add:

#### Required Secrets:
- `EW_USER`: Your Enrollware username
- `EW_PASS`: Your Enrollware password

#### Optional (Google Drive):
- `GOOGLE_DRIVE_CREDENTIALS`: Google Drive API service account JSON credentials
- `GOOGLE_DRIVE_FOLDER_ID`: Target Google Drive folder ID

### 3. Google Drive Setup (Optional)

#### 3.1 Create Google Cloud Project
1. Visit [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project or select existing one
3. Enable the Google Drive API

#### 3.2 Create Service Account
1. Go to IAM & Admin > Service Accounts
2. Create a new service account
3. Download the JSON key file
4. Copy the JSON content to `GOOGLE_DRIVE_CREDENTIALS` secret

#### 3.3 Get Folder ID
1. Create a target folder in Google Drive
2. Get the folder ID from the URL (the long string in the URL)
3. Add it to `GOOGLE_DRIVE_FOLDER_ID` secret

### 4. Automated Schedule

Once configured, the script will:
- Run automatically every day at 2:00 AM UTC
- Export the last 30 days of student data
- Upload files to Google Drive (if configured)
- Store files as GitHub Actions artifacts

## 🎯 Manual Execution

You can manually trigger the workflow:
1. Go to your repository's **Actions** tab
2. Select "Enrollware Data Export" workflow
3. Click "Run workflow"

## 📁 Project Structure

```
enrollware-bot/
├── .github/workflows/
│   └── export.yml          # GitHub Actions workflow
├── chrome-data/             # Chrome user data directory
├── downloads/               # Downloaded files directory
├── enrollware-bot/
│   └── upload-to-drive.js   # Google Drive upload functionality
├── login_and_export.js      # Main script
├── package.json             # Dependencies and scripts
├── DEPLOYMENT.md            # Deployment guide (Chinese)
└── README.md               # This file
```

## 🔍 How It Works

1. **Authentication**: The script navigates to Enrollware and handles login automatically
2. **Date Configuration**: Sets up a custom date range (last 30 days)
3. **Export Process**: Configures export settings and triggers the download
4. **File Management**: Monitors download completion and manages files
5. **Upload**: Optionally uploads files to Google Drive
6. **Cleanup**: Handles errors and cleanup processes

## 🛠️ Troubleshooting

### Common Issues:

1. **Chrome Launch Failed**: 
   - Check Chrome installation path
   - Verify Chrome binary location in environment variables

2. **Login Failed**: 
   - Verify username and password in secrets/environment
   - Check for CAPTCHA or additional security measures

3. **Google Drive Upload Failed**: 
   - Verify API credentials format
   - Check folder ID and permissions
   - Ensure service account has access to the folder

4. **File Download Failed**: 
   - Check network connectivity
   - Verify Enrollware site structure hasn't changed

### Debug Methods:

1. Check GitHub Actions logs for detailed error information
2. Use manual workflow triggers for testing
3. Review environment variable configuration
4. Check error screenshots (automatically captured on failure)

## 🔒 Security Notes

- Never commit sensitive credentials to the repository
- Regularly update passwords and API keys
- Use minimal permissions for Google Drive API
- Monitor GitHub Actions usage and logs
- Keep dependencies updated

## 📊 Dependencies

- **puppeteer-real-browser**: ^1.0.0 - Browser automation
- **dotenv**: ^16.0.0 - Environment variable management
- **googleapis**: ^128.0.0 - Google Drive API integration

## 📄 License

MIT License - see LICENSE file for details.

## 👨‍💻 Author

**Boyi Wang**  
Email: [boyiwanglance@gmail.com](mailto:boyiwanglance@gmail.com)

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## 📞 Support

If you encounter any issues or have questions, please:
1. Check the troubleshooting section above
2. Review GitHub Actions logs
3. Create an issue in the repository
4. Contact the author via email

---
