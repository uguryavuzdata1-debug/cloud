# Personal Cloud Desktop

Personal Cloud Desktop is a modern, light-themed web interface that directly integrates with Google Drive API. It provides a clean and beautiful environment to view, manage, and interact with your personal files.

## Features

- **Google Drive Integration:** Real-time fetching, uploading, creating folders, renaming, and deleting files directly from your Google Drive.
- **Two-Factor Authentication (2FA):** Session persistence is intentionally disabled. Users must authenticate through Google every time, ensuring high security and preventing unauthorized access.
- **Dynamic Storage Tracking:** Accurately reflects your Google Drive storage limits and used space dynamically.
- **File Previews & Icons:** Visually identifies file types—like PDFs, Images, Google Forms, Google Scripts, Excel Sheets, and Word Docs—with unique and aesthetically pleasing icons.
- **Pagination Support:** Supports downloading your full library of Google Drive files seamlessly, bypassing the initial pagination limits.
- **Restricted Access:** Access is limited specifically to authorized emails, protecting against random logins.

## Technical Stack

- **Frontend:** HTML, CSS (Vanilla), JavaScript
- **API Integration:** Google Identity Services (GSI) for Auth, Google API Client Library (GAPI) for Drive Integration.

## Deployment

This application is ready to be deployed on any static hosting provider like GitHub Pages. Ensure that your Google Cloud Console has your specific deployment URL added to the "Authorized JavaScript Origins" and "Authorized Redirect URIs".

## Setup Instructions

1. Configure your Google Cloud Console Project and Enable the Google Drive API.
2. Obtain your `Client ID` and `API Key`.
3. In `index.html`, set your specific credentials:
   ```javascript
   const CLIENT_ID = 'YOUR_CLIENT_ID';
   const API_KEY = 'YOUR_API_KEY';
   ```
4. Define your allowed email address:
   ```javascript
   const ALLOWED_EMAIL = 'your-authorized-email@gmail.com';
   ```
5. Deploy to your preferred hosting provider.
