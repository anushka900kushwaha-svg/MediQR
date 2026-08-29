# MediQR 🏥

## Digital Emergency Medical ID & QR Emergency Response System

MediQR is a **QR-based digital emergency medical identification system** designed to provide quick and controlled access to essential medical information during emergency situations.

A user can create a digital emergency medical profile containing information such as **blood group, allergies, medications, medical conditions, and emergency contacts**. A unique QR code is generated for the profile, which can be displayed on a phone lock screen, printed as a card, sticker, wallet card, or placed in another easily accessible location.

During an emergency, a bystander or responder can simply **scan the QR code using a smartphone** and access the user's emergency information through a web browser without installing an application.

---

## 🚨 Why MediQR?

In an emergency, a person may be:

* Unconscious or unable to communicate
* Unable to unlock their phone
* Unable to provide their medical history
* Without immediate access to emergency contacts
* Carrying medical information that is scattered or unavailable

MedQR provides a simple solution:

> **Scan the QR → View approved emergency information → Contact an emergency contact**

The system also gives users control over **which medical information is visible** to someone scanning their QR code.

---

## ✨ Key Features

### 🩺 Digital Medical Profile

Users can maintain important emergency information including:

* Blood group
* Allergies
* Medications
* Medical conditions
* Emergency contacts

### 📱 QR-Based Emergency Access

Each user receives a unique QR code linked to their emergency profile.

The QR code can be:

* Displayed on a phone lock screen
* Downloaded
* Printed
* Used on a medical card
* Placed on a sticker or wallet card

### 🚑 Emergency Card

Scanning the QR code opens an emergency-focused webpage containing the medical information allowed by the profile owner.

### 🔐 Privacy Controls

Users can control the visibility of individual medical fields.

For example:

* Blood group → Visible
* Allergies → Visible
* Medications → Hidden
* Other information → Hidden

This helps balance **emergency accessibility and privacy**.

### 📞 Emergency Contacts

The emergency page provides a direct option to contact a trusted emergency contact through the phone's dialer.

### 🔄 QR Lifecycle Management

Users can:

* Generate a QR token
* Deactivate an existing token
* Regenerate a new token

### 📊 Scan History

The system records QR scan events, providing an audit trail for the profile owner.

### 🔔 Notifications

The profile owner can receive notifications when their emergency QR is scanned.

### 📱 Mobile Application

MediMate also includes a cross-platform **React Native/Expo mobile application** for account and medical-profile management.

---

## 🔄 System Workflow

```text
User Registration
       ↓
Create Medical Profile
       ↓
Add Emergency Contacts
       ↓
Generate QR Code
       ↓
Download / Print / Display QR
       ↓
Emergency Occurs
       ↓
Responder Scans QR
       ↓
Emergency Profile Retrieved
       ↓
Privacy Rules Applied
       ↓
Critical Information Displayed
       ↓
Emergency Contact Can Be Called
```

---

## 🏗️ System Architecture

```text
                    ┌──────────────────────┐
                    │   User / Responder   │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   Web / Mobile UI    │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │     Next.js 16       │
                    │       React 19       │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Next.js Route        │
                    │ Handlers / APIs      │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │      Prisma ORM      │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │      SQLite DB       │
                    └──────────────────────┘
```

---

## 🛠️ Technology Stack

| Component             | Technology                 |
| --------------------- | -------------------------- |
| Web Frontend          | **Next.js 16**             |
| UI Library            | **React 19**               |
| Mobile                | **React Native + Expo**    |
| Programming Language  | **TypeScript**             |
| Backend               | **Next.js Route Handlers** |
| Database              | **SQLite**                 |
| ORM                   | **Prisma ORM**             |
| Authentication        | **JWT + jose**             |
| Password Security     | **bcrypt**                 |
| Mobile Secure Storage | **Expo SecureStore**       |
| Styling               | **Vanilla CSS**            |

> **Important:** The current implementation uses **Next.js 16 with React 19**. It does **not** currently use AI, ML, OCR, NLP, embeddings, vector databases, or LLM integrations.

---

## 📂 Project Structure

A simplified structure of the project is:

```text
MediMate/
│
├── app/
│   ├── api/
│   │   ├── auth/
│   │   ├── dashboard/
│   │   ├── profile/
│   │   ├── qr/
│   │   └── notifications/
│   │
│   ├── e/
│   │   └── [token]/
│   │
│   └── ...
│
├── components/
│   └── ...
│
├── lib/
│   ├── auth/
│   ├── prisma/
│   └── ...
│
├── mobile/
│   └── ...
│
├── prisma/
│   └── schema.prisma
│
├── public/
│   └── ...
│
├── package.json
├── tsconfig.json
└── README.md
```

> The exact folder structure may vary depending on the current branch and implementation.

---

## 🗄️ Database Design

MediMate uses **SQLite** with **Prisma ORM**.

### Main Models

| Model              | Purpose                                         |
| ------------------ | ----------------------------------------------- |
| `User`             | Stores user account information                 |
| `EmergencyProfile` | Stores emergency medical information            |
| `EmergencyContact` | Stores trusted emergency contacts               |
| `QrToken`          | Stores QR token information and lifecycle state |
| `ScanEvent`        | Records QR scan activity                        |
| `Notification`     | Stores profile-owner notifications              |

### Relationships

```text
User
 │
 └── EmergencyProfile
        │
        ├── EmergencyContact
        │
        └── QrToken
               │
               └── ScanEvent
```

---

## 🔗 Important API Endpoints

| Endpoint                      | Purpose                               |
| ----------------------------- | ------------------------------------- |
| `/api/auth/register`          | Create a user account                 |
| `/api/auth/login`             | Authenticate a user                   |
| `/api/auth/logout`            | Clear authentication                  |
| `/api/dashboard`              | Retrieve profile and QR information   |
| `/api/profile/save`           | Save medical information and contacts |
| `/api/qr/deactivate`          | Deactivate QR token                   |
| `/api/qr/regenerate`          | Generate a new QR token               |
| `/api/notifications/read-all` | Mark notifications as read            |
| `/e/[token]`                  | Public emergency profile route        |

---

## 🔐 Security

MediQR uses several security mechanisms:

* Password hashing using `bcrypt`
* JWT-based authentication
* JWT verification
* HttpOnly cookies for web authentication
* SameSite cookie configuration
* Expo SecureStore for mobile authentication storage
* Field-level medical information visibility
* QR token lifecycle management

### ⚠️ Important Security Requirement

The application must use a strong `JWT_SECRET` in the production environment.

A fallback JWT secret should **not** be used in production because a predictable or exposed secret could allow attackers to forge authentication tokens.

Production deployment should:

1. Configure a strong `JWT_SECRET`.
2. Remove insecure fallback secrets.
3. Validate required environment variables.
4. Keep secrets outside source control.
5. Use secure environment/secret management.

---

## 🌐 Emergency Access

The emergency profile is available through:

```text
/e/[token]
```

When a QR code is scanned:

```text
QR Scan
   ↓
Emergency URL
   ↓
Token Verification
   ↓
Database Lookup
   ↓
Scan Event Recorded
   ↓
Privacy Settings Applied
   ↓
Emergency Information Displayed
   ↓
Emergency Contact Action
```

The emergency route is designed to work through a **web browser**, so the responder does not need to install the MediQR application.

---

## 📱 Mobile Application

The project includes a React Native/Expo application.

### Mobile Features

* User registration
* Login
* Dashboard
* Medical profile management
* QR viewing
* Emergency view
* Secure authentication storage

The mobile application communicates with the Next.js backend through API requests.

---

## ⚙️ Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR-USERNAME/MediMate.git
```

Move into the project directory:

```bash
cd MediQR
```

---

### 2. Install Dependencies

```bash
npm install
```

---

### 3. Configure Environment Variables

Create a `.env` file in the project root.

Example:

```env
DATABASE_URL="file:./dev.db"
JWT_SECRET="your-strong-secret-key"
```

> Never commit `.env` or other files containing secrets to GitHub.

---

### 4. Setup Prisma

Run:

```bash
npx prisma generate
```

Then initialize/update the database:

```bash
npx prisma migrate dev
```

---

### 5. Start the Development Server

```bash
npm run dev
```

The application should then be available at:

```text
http://localhost:3000
```

---

## 🧪 Development

Useful commands:

```bash
npm run dev
```

Start the development server.

```bash
npm run build
```

Create a production build.

```bash
npm start
```

Start the production server.

```bash
npx prisma studio
```

Open the Prisma database interface.

---

## ⚠️ Current Known Issues

The current codebase has a few integration issues that should be fixed before production deployment.

### 1. Mobile QR Endpoint Mismatch

The mobile application currently uses:

```text
/qr/revoke
/qr/generate
```

while the backend provides:

```text
/api/qr/deactivate
/api/qr/regenerate
```

These endpoints need to be aligned.

### 2. Mobile Emergency View Mismatch

The mobile emergency view expects JSON data, while the current:

```text
/e/[token]
```

route returns an HTML emergency page.

The mobile client and backend response format should be made consistent.

### 3. Emergency Contact Payload Mismatch

The mobile application sends:

```text
contacts
```

while the backend expects:

```text
emergencyContacts
```

The field name should be standardized to prevent emergency contacts from being lost.

### 4. JWT Secret

The production environment must provide a secure:

```text
JWT_SECRET
```

and the insecure fallback secret should be removed.

---

## 🚧 Limitations

MediQR currently has some limitations:

* Emergency access requires network connectivity.
* A completely powered-off phone cannot display a screen-based QR.
* Medical information depends on the accuracy of information provided by the user.
* Hospital and ambulance systems are not currently integrated.
* AI-based medical diagnosis is not implemented.
* Some mobile/backend integration issues remain.
* The system should not be treated as a replacement for professional medical advice.

---

## 🔮 Future Scope

Future improvements may include:

* 👨‍👩‍👧 Caregiver and family account management
* 🏥 Hospital integration
* 🚑 Ambulance integration
* ⌚ Wearable medical identification
* 📡 NFC-based medical identification
* 🌐 Multilingual emergency profiles
* 📍 Improved emergency location functionality
* 🪪 Stronger identity verification
* 📋 Advanced audit and access-control mechanisms
* 📶 Secure offline emergency information
* 🔗 Integration with authorized healthcare systems

Any future AI functionality should be designed responsibly and should **not replace professional medical judgment**.

---

## 🎯 Expected Benefits

MediQR can provide:

* Faster access to critical medical information
* Better awareness of allergies and medical conditions
* Quick access to emergency contacts
* Reduced dependence on unlocking a phone
* Easy information sharing through QR
* User-controlled medical privacy
* A reusable digital medical profile
* Better emergency information management

---

## 📌 Project Status

**Status:** 🚧 Active Development

The core MediQR functionality has been implemented, including:

* ✅ User authentication
* ✅ Emergency medical profile
* ✅ QR generation and management
* ✅ Public emergency route
* ✅ Privacy controls
* ✅ Emergency contacts
* ✅ Scan history
* ✅ Notifications
* ✅ Web application
* ✅ React Native/Expo application

Before production deployment, the documented **mobile API mismatches and JWT security issue** should be resolved.

---

## 🤝 Contribution

Contributions, suggestions, and improvements are welcome.

To contribute:

```bash
git clone https://github.com/YOUR-USERNAME/MediMate.git
cd MediQR
npm install
```

Create a new branch:

```bash
git checkout -b feature/your-feature
```

Make your changes, test them, and submit a pull request.

---

## 👩‍💻 Project

**MediQR — Digital Emergency Medical ID & QR Emergency Response System**

### Project Type

**Software / HealthTech**

### Primary Function

**Digital Emergency Medical ID & QR Emergency System**

### Current Technology

**Next.js 16 + React 19 + React Native + Expo + TypeScript + Prisma + SQLite**

---

## 📄 License

This project is currently intended for educational, hackathon, and development purposes.

A formal open-source license can be added before public distribution.
