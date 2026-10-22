<div align="center">

# 📚 Assignmentor

**Write, convert, edit, and store all your college assignments in one place.**

[![Platform](https://img.shields.io/badge/platform-Android-3DDC84?logo=android&logoColor=white)](#-download--install)
[![Built with](https://img.shields.io/badge/built%20with-React%20Native%20%2B%20Expo-61DAFB?logo=react&logoColor=black)](https://expo.dev)
[![Backend](https://img.shields.io/badge/backend-FastAPI-009688?logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com)
[![License](https://img.shields.io/badge/license-MIT-blue)](#-license)

[**⬇️ Download the APK**](https://github.com/YOUR_USERNAME/assignmentor/releases/latest) · [Report a bug](https://github.com/YOUR_USERNAME/assignmentor/issues) · [Request a feature](https://github.com/YOUR_USERNAME/assignmentor/issues)

<!-- Add a banner or 3-4 screenshots here, e.g. ![Screenshots](docs/screenshots.png) -->

</div>

---

## 📖 About

Students juggle assignments across WhatsApp chats, random folders, email attachments, and half a dozen converter websites. **Assignmentor** puts the whole workflow in one app:

- draft an assignment with AI help,
- convert it to whatever format your professor wants,
- tidy up the formatting,
- and keep every assignment in a single searchable place, **stored on your own phone**.

> **Privacy first:** your assignments are stored locally on your device. We don't keep copies of your documents on any server.

---

## ✨ Features

> Status legend: ✅ available · 🚧 in progress · 🗓️ planned. Update this table as you ship.

| Feature | What it does | Status |
|---|---|---|
| **✍️ AI Writer** | Chat with an AI assistant to draft, outline, and improve answers to assignment questions. Save the result straight to your assignments. | 🚧 |
| **🔄 Document Converter** | Image → PDF, Word → PDF, PPT → PDF, and more. | 🚧 |
| **🗂️ All Assignments** | One searchable library of every assignment, stored on your device. Create, rename, edit, delete. | 🚧 |
| **📄 PDF Tools** | Add headers/footers and page numbers, crop pages, merge, split, reorder, and delete pages. | 🗓️ |
| **🧹 Format Cleaner** | Normalize fonts, spacing, and margins of Word documents to a standard assignment layout. | 🗓️ |
| **💾 Backup & Restore** | Export all your assignments to a single file and restore them on a new phone. | 🗓️ |
| **⏰ Deadline Reminders** | Local notifications before assignments are due. | 🗓️ |

---

## ⬇️ Download & Install

Assignmentor is currently distributed as an Android APK through GitHub Releases.

1. Go to the [**Releases page**](https://github.com/YOUR_USERNAME/assignmentor/releases/latest).
2. Under **Assets**, download `assignmentor-vX.Y.Z.apk` to your phone.
3. Open the downloaded file. If Android blocks it, allow **"Install unknown apps"** for your browser or file manager when prompted.
4. Tap **Install**, then open **Assignmentor**.

**Requirements:** Android 8.0+ and an internet connection for AI writing and Word/PPT conversion. Viewing, storing, and PDF editing work offline.

> ⚠️ Because the app isn't on the Play Store yet, Android or Play Protect may show a warning for apps installed outside the store. Only install APKs from this repository's official Releases page.

---

## 🚀 How to Use

### 1. Write with AI
1. Open the **Write** tab.
2. Paste or type your assignment question, and optionally add details such as subject, word count, and tone.
3. Read the generated draft, ask follow-ups to refine it, then tap **Save as assignment**.

> Use the AI as a drafting and study aid. Always review, fact-check, and rewrite in your own words, and follow your institution's academic integrity policy.

### 2. Convert documents
1. Open **Tools → Converter**.
2. Pick a file (or take a photo), choose the output format, and tap **Convert**.
3. Save the result to your assignments or share it.

| From | To |
|---|---|
| Images (JPG/PNG) | PDF |
| Word (.docx) | PDF |
| PowerPoint (.pptx) | PDF |

Word and PPT conversions are processed on our server and deleted right after the converted file is returned.

### 3. Manage your assignments
- **Search** by title, subject, or content.
- **Organize** with subjects and tags.
- **Open, edit, rename, share, or delete** from the assignment menu.

### 4. Edit PDFs
Open a PDF assignment and choose **Edit** to add a header/footer, crop pages, or merge/split/reorder pages. This all happens on your device.

### 5. Back up your data
Go to **Settings → Export backup**, then choose where to save or send the `.zip` (Google Drive, Files, WhatsApp, email). To restore, use **Settings → Restore backup** and pick the file.

---

## 🔒 Privacy

- **Your assignments stay on your phone.** They are never uploaded for storage.
- **Sent to our server (only when you use the feature):** AI prompts, and files you ask us to convert. Converted files are not stored.
- **Account and usage data:** basic account details and anonymous action types (for example "converted a Word file to PDF", with file size and success/failure) to prevent abuse and improve the app. We do **not** log your file names or document contents.
- **AI provider:** prompts are forwarded to a third-party AI API to generate responses.

Read the full [Privacy Policy](PRIVACY.md).

---

## 🏗️ Architecture

Assignmentor is a **local-first mobile app** backed by a thin, stateless API.

```
┌──────────────────────── Mobile (React Native + Expo) ────────────────────────┐
│ UI (screens)  →  Hooks / Services  →  Repositories (SQLite + file system)    │
│                                    →  API client (HTTPS + auth token)        │
└──────────────────────────────────────┬───────────────────────────────────────┘
                                       │
┌──────────────────────────────────────▼───────────────────────────────────────┐
│ Backend (FastAPI):  Routers → Services → Repositories → PostgreSQL           │
│    ├── AI provider (NVIDIA API)                                              │
│    └── LibreOffice · python-docx · Pandoc (stateless file processing)        │
└──────────────────────────────────────────────────────────────────────────────┘
```

### Tech stack

| Layer | Technology |
|---|---|
| Mobile app | React Native, Expo, Expo Router, TypeScript |
| On-device storage | `expo-sqlite`, `expo-file-system` |
| PDF tools | `pdf-lib`, `react-native-pdf` |
| Backend | Python, FastAPI |
| Database | PostgreSQL (users, usage, quotas only) |
| Document processing | LibreOffice (headless), python-docx, Pandoc |
| AI | NVIDIA API |
| Packaging and hosting | EAS Build (APK), Docker, Render/Railway/Fly.io |

---

## 📁 Project Structure

```
assignmentor/
├── mobile/                  # React Native app
│   ├── app/                 # Expo Router screens
│   ├── src/
│   │   ├── features/        # assignments, ai-writer, converter, pdf-tools, ...
│   │   ├── db/              # SQLite client, schema, migrations
│   │   ├── api/             # API client
│   │   ├── components/ui/
│   │   └── lib/
│   ├── app.json
│   └── eas.json
├── backend/                 # FastAPI service
│   ├── app/
│   │   ├── api/v1/          # routers
│   │   ├── services/        # business logic
│   │   ├── repositories/    # DB access
│   │   ├── models/ schemas/ core/ db/
│   ├── alembic/             # migrations
│   ├── tests/
│   ├── Dockerfile
│   └── docker-compose.yml
├── docs/                    # screenshots, diagrams
├── PRIVACY.md
└── README.md
```

---

## 🛠️ Development Setup

### Prerequisites
- Node.js 20+ and npm
- Python 3.11+
- Docker (for LibreOffice and local PostgreSQL)
- An Android device or emulator
- An NVIDIA API key

### 1. Clone

```bash
git clone https://github.com/YOUR_USERNAME/assignmentor.git
cd assignmentor
```

### 2. Backend

```bash
cd backend
cp .env.example .env        # fill in the values below
docker compose up --build   # starts the API and PostgreSQL
```

`.env` variables:

```env
DATABASE_URL=postgresql://user:password@db:5432/assignmentor
NVIDIA_API_KEY=your_key_here
JWT_SECRET=change_me
MAX_UPLOAD_MB=15
AI_DAILY_LIMIT=30
```

The API runs at `http://localhost:8000`, with interactive docs at `/docs`.

### 3. Mobile app

```bash
cd mobile
npm install
cp .env.example .env        # set EXPO_PUBLIC_API_URL
npx expo start
```

Because the app uses native modules (such as `react-native-pdf`), run it as a **development build** rather than Expo Go:

```bash
npx expo run:android
```

---

## 📦 Building the APK

Cloud build with EAS:

```bash
npm i -g eas-cli
eas login
cd mobile
eas build -p android --profile preview
```

`eas.json` must set the preview profile to produce an APK:

```json
{ "build": { "preview": { "android": { "buildType": "apk" } } } }
```

Download the APK from the build link, then publish it:

1. Create a new **Release** on GitHub with a version tag (e.g. `v1.0.0`).
2. Attach the APK as a release asset.
3. Add release notes describing what's new.

---

## 🗺️ Roadmap

- [ ] AI Writer with streaming responses
- [ ] Local assignment library with search
- [ ] Image/Word/PPT → PDF conversion
- [ ] PDF header/footer, crop, merge, split
- [ ] Format Cleaner for Word documents
- [ ] Backup & Restore
- [ ] Deadline reminders
- [ ] Subject folders and tags
- [ ] Assignment templates (cover page, lab report, essay)
- [ ] Google Drive backup
- [ ] Play Store release

Have an idea? [Open an issue](https://github.com/YOUR_USERNAME/assignmentor/issues).

---

## 🤝 Contributing

Contributions are welcome.

1. Fork the repo and create a branch: `git checkout -b feature/your-feature`
2. Commit your changes with a clear message
3. Push and open a Pull Request describing what and why

---

## ❓ FAQ

**Are my assignments uploaded anywhere?**
No. They live on your device. Only the text you send to the AI writer and files you choose to convert pass through our server, and converted files aren't stored.

**What happens if I lose or reset my phone?**
Local data is lost unless you've exported a backup. Use **Settings → Export backup** regularly.

**Is it free?**
Yes for now. AI usage has a daily limit to keep the service sustainable.

**Does the AI write assignments for me to submit as-is?**
It's built as a drafting and study aid. Check your institution's policy on AI use and always review and rewrite the output.

---

## 📄 License

Distributed under the MIT License. See [`LICENSE`](LICENSE) for details.

---

<div align="center">

Built by [YOUR_NAME](https://github.com/YOUR_USERNAME) · Made for students, by a student 🎓

</div>