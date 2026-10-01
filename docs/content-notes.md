# Content notes – factual basis of the SKS privacy policy

This file records what the privacy policy is based on. Update it whenever the app's behavior or the policy changes. It is not legal advice.

## 1. Confirmed app behavior (supplied by the developer)

- App name: **SKS**. In-app title: **SKS Lernapp**.
- Platforms: iOS and Android.
- Bundle ID / Android application ID: `com.einsteinhain.sks`.
- Current version: 1.0.0.
- Offline learning / exam-preparation app with fixed educational and exam content bundled with the app.
- Users rate their own answers as **Wrong**, **Partly correct** or **Correct**. The resulting learning progress is stored locally on the device.
- A progress record contains the question ID, the self-assessment and the date/time of the assessment.
- The app has a function to delete all learning progress. The fixed content stays in the app after deletion.
- The app does not intentionally send learning progress to a server, and does not intentionally collect or transmit personal data.
- The app does **not** have: an account system, social features, advertising, analytics, tracking, subscriptions, in-app purchases, payments, AI-generated questions, automatic answer grading, cloud synchronization, server-side user profiles or network-based features.
- The Android release currently requests no Android permissions.
- The app does not intentionally access the camera, microphone, photos, contacts, location, health data, calendar, Bluetooth, advertising identifiers, or device identifiers for tracking.
- The app UI is German only (`locale: Locale('de')`). The rating labels are “Falsch”, “Teilweise richtig” and “Richtig” (renamed from “Perfekt” in app commit `4910da9`). The delete button is labelled “Alle Fortschrittsdaten löschen” and is on the “Übersicht” screen (`lib/ui/app_strings.dart`, `lib/ui/dashboard_screen.dart`).
- Provider: Hannes Diethelm, Pettenkoferstrasse 42, 10247 Berlin, Germany; info@einsteinhain.com (supplied by the developer). URLs: German policy (primary, given to the stores) `https://einsteinhain.com/sks/datenschutz/`, English translation `https://einsteinhain.com/sks/privacy-policy/`, Impressum `https://einsteinhain.com/sks/impressum/`.
- OS backups may include locally stored app data under normal platform backup behavior. **Decision:** the app's backup configuration stays unchanged, and the policy discloses this in plain language.

## 2. Observed in the app source code (at `/Users/hd/apps/sks`, re-checked at commit `55dee3e` on 1 October 2026)

These points were read from the source and match the facts above.

- The non-SDK runtime dependencies in `pubspec.yaml` are `shared_preferences` and `url_launcher` (plus `flutter_localizations`). `url_launcher` only opens the policy URL in the external browser (Übersicht → „Datenschutzerklärung“); the app itself makes no network requests.
- The light/dark appearance toggle is not persisted.
- Progress is stored under one `shared_preferences` key (`learning_progress_v1`). Each stored assessment holds the question ID, the assessment and its date/time (`recordAssessment(questionId, assessment, assessedAt)`).
- "Delete all progress" removes that key (`deleteAll()` → `remove(storageKey)`).
- The release `android/app/src/main/AndroidManifest.xml` declares no `<uses-permission>`. `INTERNET` appears only in the `debug` and `profile` manifests, which are used for development and aren't part of the release build.
- The main Android manifest doesn't set `android:allowBackup`, so Android's default backup behavior applies. On iOS, app data is normally included in device backups.
- No `PrivacyInfo.xcprivacy` was found in `ios/Runner`. See review item 4.

## 3. Policy sections and their factual basis

The German page (`datenschutz/`) is the primary text. The English page (`privacy-policy/`) has the same sections in the same order and states that the German version prevails. Restructured on 1 October 2026 into a full Art. 13 GDPR notice (summary box, table of contents, numbered sections).

| Policy section | Statements | Basis |
|---|---|---|
| Header, summary | Controller, dates; plain-language summary | §1 |
| 1 Controller and contact | Name, address, email; no DPO (Art. 37 GDPR, §38 BDSG thresholds not met) | §1; decision 14 |
| 2 Scope | App, website, email; definition of personal data | — |
| 3.1 No data transmission | Offline; no network connections, accounts, cloud, ads, third-party SDKs, tracking IDs, purchases | §1, §2 |
| 3.2 Progress on device | Question ID, rating, date/time; local only (UserDefaults/SharedPreferences); theme not stored; no processing by us, fallback legal basis Art. 6(1)(b)/(f); §25(2) no. 2 TDDDG | §2; decision 3 |
| 3.3 Permissions | None requested; no INTERNET permission in release | §2 |
| 3.4 Opening the policy | Browser makes the connection; section 6 applies | §2 (`url_launcher`) |
| 3.5 Deletion and backups | Delete button and location; uninstall; OS backups | §1, §2 |
| 4 App stores | Download by Apple/Google as independent controllers; crash/usage statistics (opt-in, Art. 6(1)(f), opt-out paths); store reviews | Decision 4; decision 15 |
| 5 Email | Data, legal basis, deletion criteria; Namecheap as processor | Decision 3; decision 16 |
| 6 Website | Static, no cookies/JS/third-party content; GitHub Pages IP logging; Art. 6(1)(f) | Decisions 7, 11 |
| 7 Recipients and transfers | GitHub (DPF, Art. 45); Namecheap (SCCs 2021/914, Art. 46(2)(c)); no selling | Decisions 11, 16 |
| 8 No automated decisions | Art. 22; no obligation to provide data (Art. 13(2)(e)) | §1 |
| 9 Security | OS app sandbox; HTTPS | §2 |
| 10 Children | Works the same for all ages; no data collected from minors | Decision 2 |
| 11 Rights | Art. 15–18, 20, 21; Art. 11 note for on-device data; separate right-to-object box; complaint to Berlin DPA | Decisions 3, 6, 17 |
| 12 Changes | Current version applies; consent would be asked in-app before any future processing requiring it | — |

## 4. Decisions (30 September 2026)

These decisions are based on the primary sources listed below. **They were made by Claude and have not been checked by a lawyer.**

1. **Store disclosures.**
   - *App Store Connect → App Privacy:* answer **“No, we do not collect data from this app”** (“Data Not Collected”). Apple defines “collect” as transmitting data off the device, and says data processed only on the device is not collected and that developers are not responsible for disclosing data collected by Apple.
   - *Google Play → Data safety:* answer **No** to “Does your app collect or share any of the required user data types?”. Google says data that is only processed on the device and not sent off it doesn't need to be disclosed. Android vitals crash data is collected by Google at the operating-system level from users who opted in, not by the app. Enter the privacy-policy URL.
   - *Apple privacy manifest:* separate from the questionnaire. Check that the build includes the manifest shipped by `shared_preferences` (`UserDefaults` is a “required reason” API) before App Store submission.
2. **Children / target audience.** The policy now says only that the app “works the same way for all users, regardless of age”. The earlier wording “including children” could read as if children were a target group. **Store setting:** in Google Play, choose target age groups **16–17 and 18 and over** (the SKS licence can only be obtained from age 16). This keeps the app outside Google's Families Policy, which applies once any under-13 group is selected. Apple's age rating is set by the content questionnaire; with no objectionable content it will be 4+, which is a content rating, not a target audience.
3. **User rights and email contact.** The developer is based in Germany, so the GDPR applies to any personal data the developer does process. The app itself sends nothing, but **emails to info@einsteinhain.com are processed by the developer**, which triggers the information duties in Art. 13 GDPR (controller, purpose, legal basis, retention, rights, right to complain). The policy now names the controller, briefly states how email enquiries are handled (Art. 6(1)(b)/(f) GDPR), lists the GDPR rights and mentions the right to complain to a supervisory authority. Storing progress on the device doesn't need consent under §25(2) no. 2 TDDDG, because it is strictly necessary for a feature the user explicitly requests. No text is needed for this.
4. **Store statistics.** Apple (App Analytics, crash reports) and Google (Android vitals) give developers crash reports and usage statistics from users who have opted in, by default in their developer consoles. The policy mentions this in one sentence, with the purpose stated as finding and fixing problems. **Confirmed by the developer on 30 September 2026.**
5. **Delete button.** The policy now names the actual label and location: “Übersicht” → “Alle Fortschrittsdaten löschen”.
6. **Separate right to object.** Email handling and the website's server logs rely on Art. 6(1)(f) GDPR (legitimate interest). Art. 21(4) GDPR requires the right to object to such processing to be pointed out clearly and separately from other information, so both pages have a separate, bold “Widerspruchsrecht / Right to object” paragraph.
7. **Website section.** Every visit to einsteinhain.com/sks/ causes the hosting provider to process IP addresses, which is personal data under the GDPR, so the policy has a short “Diese Website / This website” section. It names the host only as “our hosting provider”, because none has been chosen yet (open item 1).
8. **German primary, English translation, one URL for the stores.** The app is German only, so the German page is the primary text, and its URL `…/sks/datenschutz/` is the one given to Apple and Google. The English page says it is a translation. `…/sks/` is a simple landing page linking to all three pages. Every page links to the others.
9. **Impressum.** Whether §5 DDG applies to a free app without ads is unclear (“geschäftsmäßig, in der Regel gegen Entgelt”). Your name and address are already public in the policy, so publishing an Impressum costs nothing and removes the question. It is at `…/sks/impressum/` and linked from every page. It gives email as the only contact method. See open item 2.
10. **Apple privacy manifest.** Checked in the existing release build (`build/ios/Release-iphoneos/Runner.app`, built 29 September 2026). It contains the `shared_preferences_foundation` manifest (UserDefaults, reason `1C8F.1`, no collected data, no tracking) and Flutter's own manifest. The app code uses no other required-reason APIs, so no app-level manifest is needed. Closed.
11. **Hosting: GitHub Pages** (chosen by the developer). GitHub documents that it logs and stores the IP address of every visitor to a GitHub Pages site for security purposes. GitHub, Inc. is certified under the EU–US Data Privacy Framework (certification active, next due 08/2027), which is covered by the Commission's adequacy decision (Art. 45 GDPR). The policy names GitHub, the purpose, the possible US transfer and its basis, and refers to GitHub's privacy statement for retention, because GitHub doesn't publish a specific retention period for Pages logs. GitHub's DPA covers paid business customers, not Pages visitors, so the policy describes GitHub neutrally rather than as “our processor”.
12. **Publishing only the pages.** GitHub Pages is deployed through a GitHub Actions workflow that publishes only `index.html`, `css/`, `icons/`, `datenschutz/`, `privacy-policy/` and `impressum/`. That keeps these notes off the website. They are still visible in the public repository.
13. **Trader status: not a trader** (the developer's decision). This goes in both store forms (`store-submission.md`). If the app later earns money or is run as a business, the trader status and the Impressum must be reviewed.

14. **No data protection officer.** A single-person controller without core activities under Art. 37(1) GDPR and below the §38 BDSG threshold (20 persons) need not appoint one; the policy says so.
15. **Store reviews and opt-out paths** (1 October 2026). Public store reviews (with the reviewer's display name) are visible to the developer and can be answered, so the policy mentions them. It also tells users where to switch off sharing diagnostics with developers on iOS and Android.
16. **Email provider: Namecheap Private Email** (MX `mx1/mx2.privateemail.com`, checked 1 October 2026). Namecheap, Inc. (USA) acts as processor; its Data Processing Addendum is accepted with its terms of service and includes the EU Standard Contractual Clauses (Module 2, Decision 2021/914). No DPF certification for Namecheap was found, so the policy relies on the SCCs and offers a copy on request (Art. 13(1)(f) GDPR). If the mailbox forwards to another provider (e.g. Gmail), name that provider too.
17. **Supervisory authority.** The policy names the Berliner Beauftragte für Datenschutz und Informationsfreiheit (Alt-Moabit 59–61, 10555 Berlin), the authority for a Berlin-based controller, and reminds users they may complain in their own member state.

Sources used:
- Apple, App privacy details: https://developer.apple.com/app-store/app-privacy-details/
- Google Play, Data safety section: https://support.google.com/googleplay/android-developer/answer/10787469
- Google Play, Target audience and content: https://support.google.com/googleplay/android-developer/answer/9867159
- Android vitals (opt-in diagnostics): https://developer.android.com/google/play/vitals/crash
- §25 TDDDG: https://www.gesetze-im-internet.de/ttdsg/__25.html
- §5 DDG (Impressum): https://www.gesetze-im-internet.de/ddg/__5.html
- GitHub Pages (IP logging): https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages
- GitHub Pages custom domains: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages
- GitHub privacy statement: https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement
- Data Privacy Framework participant list: https://www.dataprivacyframework.gov/
- Namecheap Data Processing Addendum: https://www.namecheap.com/legal/universal/data-processing-addendum/
- Berlin DPA, complaints: https://www.datenschutz-berlin.de/buergerinnen-und-buerger/beschwerde/einreichen-einer-beschwerde/

## 5. Remaining open items

All texts and documents in this repository are complete. What is left happens outside it:

1. **Deploy**: set up the two GitHub repositories and the Namecheap DNS (README → Deployment), then test the URLs.
2. **Store forms**: enter the values from [`store-submission.md`](store-submission.md), including “not a trader”.
3. **In-app link**: add it as described in [`in-app-link.md`](in-app-link.md). This is an app code change.
4. **Optional legal review.** Questions for a German data-protection lawyer:
   - Are the website/GitHub section, the email paragraph and the separate right to object sufficient?
   - Is email alone enough as the Impressum contact? The ECJ (C-298/07) requires a second fast way to reach you, which doesn't have to be a phone number.
   - Is it fine that the English page is only a translation of the German one?

## 6. Deliberately not claimed in the policy

- That the app or the developer is exempt from the GDPR or any other law.
- That the policy guarantees compliance with Apple, Google, the GDPR or any other rules.
- That absolutely no data is ever processed by anyone. The policy describes the app's *intended and implemented* behavior, and mentions platform and backup processing separately.
- Any retention period other than "until deleted or removed from the device", or "no longer needed" for email enquiries.
- Any specific third-party recipients.
- That the app is (or is not) designed for children.
