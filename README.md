# Personal Cloud Desktop - Google Drive API Integration

## Walkthrough

The Personal Cloud Desktop application has been successfully integrated with the Google Drive API.

### Changes Made

#### 1. External Library Integration
- Added **Google Identity Services (GSI)** for modern OAuth2.0 authentication.
- Added **Google API Client Library (GAPI)** for Drive API interaction.

#### 2. Authentication Flow
- Implemented `handleLogin` using `tokenClient.requestAccessToken()`.
- Added user validation to ensure only the `ALLOWED_EMAIL` can access the app.
- Implemented session persistence that remembers the access token for up to 12 hours.

#### 3. Real-time File Operations
- **Listing:** The app now fetches files from Google Drive using `gapi.client.drive.files.list`.
- **Upload:** Implemented multipart upload to Drive with a progress indicator.
- **Context Actions:**
  - **Rename:** Uses `files.update`.
  - **Star:** Uses `files.update` (starred property).
  - **Delete:** Uses `files.delete`.
  - **Download:** Fetches file media as a blob and triggers a browser download.

#### 4. View Filtering
- Navigating between "My Drive", "Starred", "Trash", and "Shared" now triggers filtered API queries (`q` parameter in Drive API).

### How to Test

1. Set up a project in Google Cloud Console.
2. Enable Drive API.
3. Replace `CLIENT_ID` and `API_KEY` in the file.
4. Run the file using a local web server (e.g., Live Server).
5. Login with your Google account.
6. Manage your real files through the UI!

---

## Implementation Plan

This plan transitions the "Personal Cloud Desktop" from a simulated demo to a real-world application that interacts with the user's Google Drive.

### User Review Required

> **IMPORTANT**  
> You will need to provide a Client ID and API Key from the Google Cloud Console for this to work.
> 1. Go to Google Cloud Console.
> 2. Create a Project.
> 3. Enable Google Drive API.
> 4. Create API Key and OAuth 2.0 Client ID (Web Application).
> 5. Add your file's origin (e.g., `file://` or `http://localhost`) to the Authorized JavaScript Origins.

### Proposed Changes

#### Core Integration

**`personal-cloud-desktop.html`**

- **External Scripts:** Add GSI and GAPI script tags.
- **Initialization Logic:**
  - `initGapiClient()`: Initializes the Google API client.
  - `initTokenClient()`: Initializes the Google Identity Services token client.
- **Authentication Flow:**
  - Update `handleLogin` to use `tokenClient.requestAccessToken()`.
  - Handle token expiration and refresh.
- **File Operations (GAPI):**
  - `listDriveFiles()`: Replaces `loadFiles`. Fetches real file metadata from Drive.
  - `uploadDriveFile()`: Replaces `simulateUpload`. Performs a real multipart upload to Drive.
  - `deleteDriveFile()`: Replaces local deletion.
  - `renameDriveFile()`: Replaces local renaming.
  - `starDriveFile()`: Replaces local starring (using Drive's starred property).
- **UI Mapping:**
  - Adapt the existing `fileCard` and `renderFiles` functions to handle Drive API's file object structure (e.g., `id`, `name`, `mimeType`).
  - Add a "Loading" state for file lists.

#### Detailed Steps

1. **Script Integration:** Add `<script src="https://apis.google.com/js/api.js"></script>` and `<script src="https://accounts.google.com/gsi/client"></script>`.
2. **State Management:** Remove `DEMO_FILES` and `localStorage` dependencies for the file list. Use a global `accessToken` and `gapi` state.
3. **Drive API Methods:**
   - `files.list`: Fetch files with specific fields (`id`, `name`, `mimeType`, `size`, `modifiedTime`, `starred`, `iconLink`).
   - `files.create`: For file uploads.
   - `files.update`: For renaming and starring.
   - `files.delete`: For deleting.
4. **Working Hours Integration:** The session timer will remain. If the time expires, we will clear the `accessToken` and sign out.

### Verification Plan

**Automated/Manual Testing**
- **Login:** Verify Google Login popup appears and returns a valid token.
- **Listing:** Verify files from the user's Google Drive appear in the grid.
- **Upload:** Verify dragging a file correctly uploads it to Drive.
- **Rename/Star:** Verify changes persist on the real Google Drive.
- **Delete:** Verify files are moved to trash or deleted in Drive.
- **Working Hours:** Verify the app logs out at the specified end time.
