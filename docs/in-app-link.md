# Linking the privacy policy inside the app

Apple (App Review Guideline 5.1.1) and Google Play expect the privacy policy to be easy to find inside the app, as well as in the store listing.

| | |
|---|---|
| URL | `https://einsteinhain.com/sks/datenschutz/` |
| Label | `Datenschutzerklärung` |
| Suggested place | “Übersicht” screen, below “Alle Fortschrittsdaten löschen” (`lib/ui/dashboard_screen.dart`) |

Test that the URL is live before you release the app build with the link.

## Option A: open the page in the browser (recommended)

1. Add the dependency:

   ```bash
   flutter pub add url_launcher
   ```

2. Android 11+ only lets apps see browsers they declare. Add this to `android/app/src/main/AndroidManifest.xml`, inside `<manifest>` (next to `<application>`):

   ```xml
   <queries>
     <intent>
       <action android:name="android.intent.action.VIEW" />
       <data android:scheme="https" />
     </intent>
   </queries>
   ```

   This is not a permission. The app still requests no Android permissions, and it still doesn't need `INTERNET`, because the browser loads the page, not the app.

3. Add the strings to `lib/ui/app_strings.dart`:

   ```dart
   static const privacyPolicy = 'Datenschutzerklärung';
   static const privacyPolicyUrl = 'https://einsteinhain.com/sks/datenschutz/';
   ```

4. Add the button below the delete button in `lib/ui/dashboard_screen.dart`:

   ```dart
   import 'package:url_launcher/url_launcher.dart';

   // …below the delete button's Align(...):
   Align(
     alignment: Alignment.center,
     child: TextButton.icon(
       onPressed: () => launchUrl(
         Uri.parse(AppStrings.privacyPolicyUrl),
         mode: LaunchMode.externalApplication,
       ),
       icon: const Icon(Icons.privacy_tip_outlined),
       label: const Text(AppStrings.privacyPolicy),
     ),
   ),
   ```

## Option B: show the address only (no new dependency)

If you don't want to add `url_launcher`, show the address as selectable text. This is less convenient for users, but the policy is still easy to find:

```dart
const SelectableText(
  '${AppStrings.privacyPolicy}: ${AppStrings.privacyPolicyUrl}',
  textAlign: TextAlign.center,
),
```

## Effect on the privacy policy and store forms

Neither option changes any statement in the policy or any store-form answer. The app still collects and transmits nothing, and opening a web page happens in the user's browser. If you use option A, `url_launcher` is a new dependency; its iOS part ships its own privacy manifest.
