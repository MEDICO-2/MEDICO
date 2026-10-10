Medico AI 💊
Your Health, Your Language, Your Care.
Medico AI is a mobile-first, browser-based medicine reminder prototype designed to help people—especially senior citizens—follow the medicine schedule and instructions they enter from their own prescription. It supports spoken reminders in English and Hindi and, with the patient's consent, can prepare a message for a caregiver when reminders go unanswered.
Important safety notice: Medico AI is not a medical device and does not replace advice from a doctor or pharmacist. It repeats information entered by the user. It does not diagnose conditions, prescribe medicines, recommend or change doses, verify prescriptions, identify pills, or determine whether a medicine is appropriate. If a prescription is unclear or a dose is missed, contact a doctor or pharmacist for guidance.

 Features
Area	Status / details
Medicine schedule	Add medicines with start/end dates, times, doctor details, and instructions entered by the user
English and Hindi interface	Switch between English and हिन्दी
Spoken reminders	Uses the browser Web Speech API with en-IN and hi-IN; voice availability and quality depend on the device and browser
Dose status	Mark a reminder as taken, ask to be reminded later, or request help
Activity history	Review timestamped reminder-related events
Follow-up reminders	Configurable grace periods and one follow-up reminder
Caregiver support	Optional caregiver details and consent-based escalation; consent can be revoked
Caregiver message	Opens a pre-filled SMS for the user to review and send; the app does not automatically send it or confirm delivery
Quiet hours	Configurable quiet hours suppress reminder and escalation activity
Emergency shortcut	Configurable emergency number and a tel: call link; in India, the emergency number is 112
Find nearby care	Opens Google Maps or OpenStreetMap searches for nearby care; provider information is not verified or stored by the app
Data export and deletion	Export app data as JSON or delete this app's data from the current browser
Responsive interface	Mobile-first layout with light/dark appearance support


How reminder escalation works
1. At the scheduled time, the app displays and speaks a reminder.
2. If there is no response after the grace period (5 minutes by default), the app issues one follow-up.
3. If there is still no response after another grace period, and the patient has consented and saved a caregiver number, the app opens a pre-filled SMS for the patient to send.
4. The activity log records the message as prepared, not delivered. The reminder may be marked missed.
5. A missed reminder is not treated as an emergency.
Each stage runs at most once per medicine per day. Quiet hours suppress reminder and escalation activity.
Reminder limitation: Reminders run only while the page is open. Closing the page or browser may prevent them from firing on time. Reliable background reminders would require a native app, push notifications, or a server-side service.


Technology stack

- HTML5 — application structure
- CSS — responsive styling, design system, and theme support
- Vanilla JavaScript — scheduling, escalation, and user interface logic
- Browser localStorage — local persistence
- Web Speech API (speechSynthesis) — spoken reminders in supported languages
- sms: links — user-initiated caregiver messages
- Google Maps and OpenStreetMap links — nearby-care search shortcuts
- Node.js built-in test runner (node:test) — logic tests, requiring Node.js 18 or later
The current prototype has no build step, external package dependencies, server, database, account system, cloud synchronization, or AI/LLM integration. “AI” is part of the project name; the current prototype does not integrate an AI model.


Project structure

medico-ai/
├── index.html          # Application shell
├── css/
│   └── styles.css      # Design system, responsive layout, dark mode
├── js/
│   ├── logic.js        # Scheduling and escalation logic
│   └── app.js          # UI, storage, speech, reminder loop
├── tests/
│   └── logic.test.js   # Unit tests
└── README.md


Run locally

No package installation or build step is required. Because the app uses JavaScript ES modules, serve it over HTTP instead of opening index.html directly from disk.
Prerequisites
- A modern browser
- Python 3 to run the local static server
- Node.js 18 or later to run the tests
Start the website
1. Clone your repository and enter its folder:
   git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
   cd YOUR-REPOSITORY
2. Start a local server:
   python3 -m http.server 8080
3. Open http://localhost:8080 in your browser.
Stop the server with Ctrl+C in the terminal.
Run tests
From the project root, run:
node --test
The tests use Node.js's built-in node:test runner and do not require installing packages.


Deploy to GitHub Pages

This is a static website, so GitHub Pages can host it without a separate backend.
1. Push the project files to a GitHub repository.
2. Open the repository on GitHub.
3. Go to Settings → Pages.
4. Under Build and deployment, select Deploy from a branch.
5. Select the main branch and the / (root) folder, then save.
6. Wait for GitHub Pages to finish publishing and open the URL shown in the Pages settings.
The published URL will typically look like:
https://YOUR-USERNAME.github.io/YOUR-REPOSITORY/
The URL above is an example format; use the actual URL shown by GitHub Pages. If the repository is configured differently, adjust the branch or folder selection to match where index.html is stored.


 Privacy and consent
 
- Medicine schedules, settings, caregiver details, and activity history are stored in localStorage in the browser being used.
- There is no account system, server-side storage, or automatic cross-device synchronization.
- Anyone with access to the same browser profile may be able to access locally stored information.
- Exported JSON files may contain sensitive health information; store and share them carefully.
- Revoking caregiver consent disables the app's caregiver escalation flow.
- The caregiver feature prepares an SMS link; it does not automatically send messages or confirm delivery.
- Clearing browser data may remove the information saved by this app.


 Safety and limitations
 
- Enter medicine names, times, and instructions exactly as shown on a clinician-provided prescription.
- Medico AI does not calculate doses, verify prescriptions, identify pills, diagnose conditions, or advise whether a medicine is suitable.
- Do not rely on the app to decide what to do about a missed dose. Contact a doctor or pharmacist for advice.
- Reminders are not guaranteed to run in the background and may not fire if the page is closed, suspended, or the device is unavailable.
- Nearby-care links are search shortcuts. The app does not verify providers, opening hours, services, or availability.
- A prepared caregiver SMS is not a sent or delivered alert.
- A missed reminder is not automatically an emergency.
- In a genuine emergency in India, call 112 directly. Do not wait for this app.

 
Roadmap

Potential future improvements—not features currently provided by this prototype—include:
- Progressive Web App (PWA) support and more reliable notifications
- Additional Indian languages by extending the language dictionary in js/app.js
- Accessibility improvements, including larger text and improved onboarding
- Expanded automated tests for scheduling, data export, and consent flows
- Optional secure authentication and cross-device synchronization using a backend such as Supabase, with strict access controls
- Server-side caregiver SMS or calling through a provider that reports delivery status
- Appointments and a healthcare-provider directory with a documented verification process
Any future caregiver notification service should clearly distinguish between a message being prepared, sent, and confirmed delivered.


#  Problem Statement

Many people, especially senior citizens and individuals managing multiple medicines, may find it difficult to remember their prescribed medicine schedules. Language barriers, missed reminders, and limited caregiver communication can make following a routine more challenging.

Existing reminder tools may not always provide accessible Hindi voice reminders, consent-based caregiver support, or a simple interface for users who are less comfortable with technology.

##  Our Solution: Medico AI

Medico AI is a mobile-first medicine reminder web application that helps users follow the schedule and instructions they enter from their prescriptions. It combines English and Hindi voice reminders with simple reminder-status controls and optional caregiver messaging.

The application focuses on accessibility, user consent, privacy, and clear communication without making medical decisions.

##  Problem-Solving Approach

### 1. Language barriers
**Problem:** Some users may find text-only reminders difficult to understand or notice.

**Solution:** Provide spoken reminders in English and Hindi using the browser's Web Speech API. Voice availability and quality depend on the user's device and browser.

### 2. Forgotten medicine schedules
**Problem:** Users may lose track of scheduled reminders during their daily routines.

**Solution:** Allow users to enter medicine schedules, times, start and end dates, and prescription instructions, then receive reminders while the app page remains open.

### 3. Unanswered reminders
**Problem:** A reminder may go unanswered, leaving the user without an easy next step.

**Solution:** Provide reminder controls such as **Taken**, **Remind me later**, and **I need help**, followed by a configurable follow-up reminder.

### 4. Caregiver communication
**Problem:** A caregiver may need to be informed when a user does not respond to reminders.

**Solution:** With the user's consent and a saved caregiver number, prepare an SMS after the configured reminder stages. The user reviews and sends the message manually. The app does not claim that the message was delivered.

### 5. Privacy and user control
**Problem:** Health-related information requires careful handling.

**Solution:** Store app data locally in the browser, provide data export and deletion controls, and allow users to revoke caregiver consent. The prototype does not use a cloud database or account system.

### 6. Access to nearby care
**Problem:** Users may need help locating nearby healthcare services.

**Solution:** Provide shortcuts to Google Maps and OpenStreetMap searches for hospitals, clinics, pharmacies, diagnostic laboratories, and ambulance services. Search results are not independently verified by Medico AI.

##  Expected Impact

- Make medicine reminders easier to understand through voice support.
- Improve accessibility for users who prefer Hindi or English.
- Help users keep track of reminder statuses and history.
- Make consent-based caregiver communication easier to initiate.
- Encourage privacy-conscious handling of locally stored information.

##  Scope and Limitations

Medico AI is a reminder prototype, not a medical device. It does not diagnose, prescribe, calculate or change doses, identify pills, or verify prescriptions. Reminders are not guaranteed to run when the page is closed. Caregiver messages require the user to send them manually, and a missed reminder is not automatically an emergency.

The application supports reminder management and communication; it does not guarantee medication adherence or improved health outcomes.


 Contributing
Issues and pull requests are welcome. When proposing changes, prioritize accessibility, privacy, and safe handling of health-related information. Do not add features that invent, verify, or alter medical dosage instructions, or claim that an alert was delivered without provider confirmation.
📄 License
This project has not specified a license yet. Add a LICENSE file before distributing it as open-source software under a particular license.
