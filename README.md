# Wayback Scanner

A mobile-first Wayback Machine file search tool. Enter a domain or URL, choose a scope and date range, filter archived file records by extension/MIME/status, review capture metadata, and export results.

## First version

- Searches the Internet Archive CDX index (metadata search, not a crawler).
- Filters results by extensions and MIME type; supports date range, scope, status, and record limits.
- Reports result count, known byte totals, inferred URL-path folders, and maximum path depth.
- Opens individual archived captures; selected rows can open up to 10 archive links.
- Exports the result list as CSV or JSON.
- Capacitor wrapper configuration for Android.

File size and directory statistics are best-effort: missing sizes are excluded, and folder/depth figures are inferred from URL paths. The selected-links action opens archived captures; it is not a guaranteed native multi-file download manager.

## Build and run locally

Requires Node.js 20+ and JDK 21 for Android builds. For a browser preview, run `npm install && npm run build`, then serve `www/` with any static HTTP server.

```sh
npm install
npm run build
npx cap add android
npx cap sync android
cd android && ./gradlew assembleDebug
```

The debug APK is written to `android/app/build/outputs/apk/debug/app-debug.apk`. The Android project is generated during the build and is not committed.

## Notes

The app calls the public Wayback CDX endpoint directly. If an environment blocks cross-origin requests or the archive service is temporarily unavailable, search will show an error; a small proxy service may be needed for that environment. Broad searches are capped by the chosen CDX result limit; extension and MIME filtering happen on the returned records.
