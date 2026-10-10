# Medico AI 💊

**Your Health, Your Language, Your Care.**

Medico AI is a mobile-first medicine reminder web application designed to help people, especially senior citizens, follow their prescribed medicine schedules. It provides English and Hindi voice reminders and optional, consent-based caregiver messaging when reminders go unanswered.

> **Medical Disclaimer:** Medico AI is a reminder tool, not a medical device. It does not diagnose conditions, prescribe medicines, recommend or change doses, verify prescriptions, or identify pills. Always consult a doctor or pharmacist for medical advice.

##  Problem Statement

People managing regular medication schedules may forget reminders or find text-based applications difficult to use. Language barriers can make reminders less accessible, while unanswered reminders may leave caregivers unaware that a user has not responded.

##  Our Solution

Medico AI provides a simple, mobile-friendly interface with spoken reminders in English and Hindi, medicine schedule management, reminder status tracking, and optional caregiver messaging. It focuses on accessibility, privacy, consent, and user control.

##  Features

- **Medicine scheduling:** Enter medicine names, prescribed instructions, times, start dates, and end dates.
- **English and Hindi voice reminders:** Uses the browser's Web Speech API with `en-IN` and `hi-IN` language settings.
- **Reminder actions:** Mark a reminder as taken, request a later reminder, or select “I need help.”
- **Reminder history:** View timestamped reminder-related activities.
- **Follow-up reminders:** Provides one follow-up after the configured grace period.
- **Caregiver support:** Optionally save a caregiver number and provide or revoke consent.
- **Manual caregiver SMS:** Prepares a message that the user can review and send.
- **Quiet hours:** Suppresses reminder and escalation activity during configured quiet hours.
- **Emergency shortcut:** Provides a configurable phone link. India's emergency number is **112**.
- **Find nearby care:** Opens Google Maps and OpenStreetMap searches for healthcare services.
- **Data export and deletion:** Export app data as JSON or delete the app's locally stored data.
- **Responsive design:** Mobile-first layout with light and dark appearance support.

##  How Reminder Escalation Works

1. At the scheduled time, the app displays and speaks the reminder.
2. If there is no response after the grace period (5 minutes by default), one follow-up reminder is issued.
3. If there is still no response after another grace period, the app can prepare an SMS for a saved caregiver, provided the user has consented.
4. The user must review and send the SMS manually.
5. The activity log records the message as **prepared**, not delivered.

Each escalation stage runs at most once per medicine per day. Quiet hours suppress reminder and escalation activity.

**Important:** Reminders only run while the app page is open. A missed reminder is not automatically an emergency.

##  Technology Stack

- HTML5
- CSS3
- Vanilla JavaScript
- Browser `localStorage`
- Web Speech API (`speechSynthesis`)
- `sms:` links for user-initiated caregiver messages
- Google Maps and OpenStreetMap search links
- Node.js built-in test runner (`node:test`)

The current prototype has no backend, database, user accounts, cloud synchronization, external package dependencies, or AI/LLM integration. “AI” is part of the project name; the current prototype does not use an AI model.

##  Project Structure

```text
medico-ai/
├── index.html
├── css/
│   └── styles.css
├── js/
│   ├── logic.js
│   └── app.js
├── tests/
│   └── logic.test.js
└── README.md
```

- `index.html` — Application structure.
- `css/styles.css` — Responsive styling, design system, and theme support.
- `js/logic.js` — Scheduling and escalation logic.
- `js/app.js` — User interface, local storage, speech, and reminder loop.
- `tests/logic.test.js` — Automated logic tests.

##  Getting Started

### Prerequisites

- A modern web browser.
- Python 3 to run the local web server.
- Node.js 18 or later to run tests.

### Run Locally

**1. Clone the repository**

```bash
git clone https://github.com/MEDICO-2/MEDICO.git
cd MEDICO
```

**2. Start a local server**

```bash
python3 -m http.server 8080
```

**3. Open the application**

Visit [http://localhost:8080](http://localhost:8080) in your browser.

Because the application uses JavaScript ES modules, run it through an HTTP server rather than opening `index.html` directly from your file system.

### Run Tests

From the project root:

```bash
node --test
```

Tests require Node.js 18 or later and use the built-in Node.js test runner.

##  Deployment

Medico AI is a static website and can be hosted using GitHub Pages.

1. Push your project files to your GitHub repository.
2. Open the repository's **Settings**.
3. Select **Pages**.
4. Under **Build and deployment**, choose **Deploy from a branch**.
5. Select the `main` branch and the `/ (root)` directory.
6. Click **Save** and wait for deployment.
7. Open the published URL displayed in the Pages settings.

The URL will typically follow this format:

`https://YOUR-USERNAME.github.io/YOUR-REPOSITORY/`

Replace the placeholders with the actual GitHub username and repository name.

##  Privacy and Consent

- Medicine schedules, caregiver details, settings, and activity history are stored in the current browser's `localStorage`.
- The application does not provide accounts, server-side storage, or automatic cross-device synchronization.
- Anyone with access to the same browser profile may be able to access locally stored information.
- Exported JSON files may contain sensitive health information. Store and share them carefully.
- Revoking caregiver consent disables the caregiver escalation flow.
- Caregiver SMS messages are prepared for manual sending; the application does not automatically send or confirm delivery.
- Clearing browser data may remove saved application information.

##  Safety and Limitations

- Enter medicine details exactly as written on the prescription.
- Medico AI does not calculate doses, identify pills, diagnose conditions, or verify prescriptions.
- Contact a doctor or pharmacist if a prescription or missed dose is unclear.
- Reminders are not guaranteed to run when the page is closed or the browser is suspended.
- Voice availability and quality depend on the browser, operating system, and installed language voices.
- Nearby-care links are search shortcuts; the app does not verify providers, opening hours, or availability.
- A prepared caregiver message is not a sent or delivered alert.
- In a genuine emergency in India, call **112** directly. Do not wait for the application.

##  Future Improvements

Potential future improvements include:

- Progressive Web App (PWA) support and more reliable notifications.
- Additional Indian languages.
- Improved accessibility, larger text, and simpler onboarding.
- Expanded automated testing.
- Optional secure authentication and cross-device synchronization.
- Server-side caregiver notifications with delivery-status reporting.
- Appointments and a healthcare directory with a documented verification process.

These are future possibilities, not features currently implemented in this prototype.


## Team Contributions

**1. Divyansh Raturi – Project Lead & Planning**
- Identified the problem and defined the project objectives.
- Planned the project workflow and coordinated team activities.
- Ensured the solution addresses medicine adherence for senior citizens.

**2. Anuj Somani – Frontend Development**
- Developed the user interface using HTML, CSS, and JavaScript.
- Designed a simple, accessible, mobile-friendly interface.
- Improved usability for elderly users.

**3. Shlok Agrahari – Voice Reminder System**
- Implemented voice-based medicine reminders.
- Worked on English and Hindi text-to-speech functionality.
- Tested browser voice support and reminder playback.

**4. Sumit – Caregiver Alert & Logic**
- Developed the logic for tracking unanswered reminders.
- Worked on preparing caregiver notifications with the patient's consent.
- Helped design the medicine reminder workflow.

**5. Abhinav Bochare – Testing, Documentation & Deployment**
- Tested the application's main features and fixed reported issues.
- Prepared project documentation and the GitHub README.
- Worked on publishing the website and preparing the hackathon demonstration.

### Team Collaboration
All five members contributed to planning, reviewing the solution, discussing improvements, and preparing the final hackathon presentation.

##  Contributing

Issues and pull requests are welcome. Please prioritize accessibility, privacy, and safe handling of health-related information. Do not add features that invent or alter medical instructions or claim message delivery without confirmation.

##  License

No license has been specified yet. Add a `LICENSE` file before distributing this project under a specific open-source license..
