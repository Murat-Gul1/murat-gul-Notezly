# 📒 Notezly – Android Note-Taking and Cloud Backup Application

Notezly is a modern **note-taking application for Android devices**.  
It allows users to securely store and organize their notes, and back them up to the cloud using **Google Drive integration**.  

---

## 🚀 Features

- ✍️ **Create notes** with drawings, text, and pages  
- 🗂️ **Workspace cards** and page management  
- 🎨 Free drawing, shapes, color & pen customization  
- 📥 **Import and edit PDFs**  
- 📤 **Backup to Cloud (Google Drive)**  
  - Automatically create `Notezly` folder if missing  
  - Upload Room database files as a ZIP  
  - Versioning & hash check with `meta/index.json`  
- 📥 **Restore from Cloud**  
  - Download the latest backup ZIP  
  - Extract Room DB files safely to local storage  
  - Keep previous files with `.before_restore` suffix  
- 🔄 **Conflict Resolution**  
  - If local data is newer → upload to cloud  
  - If cloud data is newer → restore to device  
- 👤 **Google Account Management**  
  - Sign in with Google  
  - Switch account option available  
- 📊 **User Experience**  
  - Progress bar during backup/restore  
  - Notifications on success or failure  

---

## 📂 Google Drive Folder Structure

```
Notezly/
 ├── db/
 │   ├── latest.zip
 │   ├── backup_YYYY-MM-DD_HH-mm-ss.zip
 ├── meta/
 │   └── index.json
```

- **latest.zip** → Most recent backup  
- **backup_*** → Timestamped archive copies  
- **index.json** → Contains `updatedAt`, DB version, and hash  

---

## 🔐 Security & Backup Policy

- At least **500 MB of free space** is required in Drive.  
- For large files, **resumable upload** ensures safe transfer.  
- Old backups are automatically cleaned to prevent bloating.  
- Only the most recent **X number of backups** are kept (e.g., last 5).  

---

## 📱 User Scenarios

1. **Backup to Cloud**  
   - User signs in with Google.  
   - Notes are zipped and uploaded to Drive.  
   - On success:  
     > “Backup completed. Last backup: [date]”  

2. **Restore from Cloud**  
   - The app detects the most recent `latest.zip`.  
   - Downloads, extracts, and applies DB files.  
   - On success:  
     > “Restore completed. Cloud backup from [date]”  

3. **Switch Account**  
   - User logs out of the current account.  
   - Signs in with a different Google account.  

---

## 🛠️ Technical Details

- **Language**: Java (Android)  
- **Database**: Room  
- **Cloud**: Google Drive API (`drive.file` scope)  
- **Auth**: Google Sign-In + OAuth 2.0  
- **File Management**: ZIP archives, JSON metadata  
- **UI/UX**:  
  - Cloud operations popup  
  - Icons:  
    - `ic_uploadtocloud.png` → Backup to Cloud  
    - `ic_clouddownload.png` → Restore from Cloud  
    - `ic_account.png` → Change Account  

---

## ✅ Acceptance Criteria

- If **Notezly folder** does not exist in Drive → create automatically.  
- Database files must be fully backed up as a ZIP.  
- Restore process must apply DB files without issues.  
- Conflict resolution must be correctly enforced.  
- User must be clearly notified at every step.  

---

## 📌 Future Improvements

- 🔄 **Automatic background backups**  
- 🔔 **Backup reminders**  
- 📑 **View backup history**  
- 🌐 **Allow users to configure their own API key**  

---
