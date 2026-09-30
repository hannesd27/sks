# Store submission sheet

The exact values to enter in App Store Connect and Google Play Console. The reasoning and sources are in [`content-notes.md`](content-notes.md), section 4. These values have not been checked by a lawyer.

**Privacy policy URL everywhere: `https://einsteinhain.com/sks/datenschutz/`**

The site must be live at that URL before you submit (see README → Deployment).

## Apple – App Store Connect

| Field | Value |
|---|---|
| App Information → Privacy Policy URL (German localization) | `https://einsteinhain.com/sks/datenschutz/` |
| Privacy Policy URL (any other localization, e.g. English, if you add one) | `https://einsteinhain.com/sks/privacy-policy/` |
| User Privacy Choices URL (optional) | leave empty |
| App Privacy → “Do you or your third-party partners collect data from this app?” | **No, we do not collect data from this app** |
| Tracking | none (the “Data Not Collected” answer covers this) |
| Age rating questionnaire | answer truthfully for the content; expected result 4+ |
| Privacy manifest | nothing to do: the release build contains the `shared_preferences` manifest (UserDefaults, no data collected, no tracking), checked on 30 September 2026 |
| Business → Digital Services Act compliance: trader status | **I am not a trader** |

## Google – Play Console

| Field | Value |
|---|---|
| App content → Privacy policy | `https://einsteinhain.com/sks/datenschutz/` |
| Data safety → “Does your app collect or share any of the required user data types?” | **No** |
| Data safety → privacy policy link | `https://einsteinhain.com/sks/datenschutz/` |
| Ads | **No, my app does not contain ads** |
| Target audience and content → target age groups | **16–17** and **18 and over** |
| “Could your app unintentionally appeal to children?” (if asked) | No |
| App access | All functionality is available without special access |
| Developer account → Trader status (EU) | **I'm not a trader** |

## What “not a trader” means

As a non-trader, your address and phone number are not shown as trader details in the EU storefronts. The stores may show EU users a note that you haven't identified yourself as a trader, so EU consumer-protection rights for contracts with traders don't apply. If you later earn money with the app (price, in-app purchases, ads) or act as a business, update the trader status in both stores and review the Impressum.

## Inside the app

See [`in-app-link.md`](in-app-link.md). Link `https://einsteinhain.com/sks/datenschutz/`.
