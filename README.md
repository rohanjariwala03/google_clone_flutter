# Google Clone (Flutter)

A Google search page clone in Flutter, targeting Android, iOS and web. Search results come from the Google Custom Search JSON API. This was a learning project from mid-2022, built by following Rivaan Ranawat's Flutter Google clone tutorial.

## What's in it

- A home page with separate mobile and web layouts. `ResponsiveLayout` switches between them at 767px wide.
- A search results screen showing the result count and search time, the result list (links open in the browser through `url_launcher`), and Prev / Next paging in steps of 10.
- A dark theme with Google-style header, tabs, footer and language links.
- `ApiService` calls `https://www.googleapis.com/customsearch/v1`. If the request fails, returns a non-200, or `isDummyData` is set to `true`, it falls back to the sample response in `lib/config/api_json.dart`, so the results screen can be worked on without a key.

## Stack

Flutter on the beta channel at the time (Dart `>=2.17.0-69.2.beta`), with `http`, `flutter_svg` and `url_launcher`. Not checked against current Flutter.

## Structure

```
lib/
  config/       api_keys.dart (placeholders) and the sample API response
  responsive/   ResponsiveLayout plus the mobile and web home layouts
  screens/      search_screen.dart
  services/     api_service.dart
  widgets/      header, search box, tabs, result item, footers (shared, mobile/ and web/)
```

## Setup

1. Create a Programmable Search Engine and an API key with the Custom Search API enabled in Google Cloud Console.
2. Put the key and the search engine ID (`cx`) in `lib/config/api_keys.dart`. Don't commit real values.
3. Run:

```bash
flutter pub get
flutter run                 # mobile
flutter run -d chrome       # web
```

## Known gaps

The repo isn't runnable as committed:

- `pubspec.yaml` declares `assets/images/`, and the widgets load `google-logo.png`, `more-apps.svg`, `search-icon.svg` and `mic-icon.svg` from there, but that folder was never committed.
- `lib/main.dart` still has `home: null`. It needs to be set to `ResponsiveLayout(mobileScreenLayout: MobileScreenLayout(), webScreenLayout: WebScreenLayout())` before anything shows up.
