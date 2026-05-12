# Network Guardian Launch Brief

Status: release APK built and ready for content push.
Product: Network Guardian.
Audience: travelers, remote workers, founders, operators, and teams that depend on public or shared WiFi.
Last audited: 2026-05-10.

## Current Release Facts

- Android release APK generated at `NetworkGuardian/flutter_app/build/app/outputs/flutter-apk/app-release.apk` on 2026-05-09 12:39:08 +0530.
- Sign-in now supports Google, Apple, and Skip for now on both Sign in and Sign up screens.
- Sign in and Sign up now both show live community counters: WiFi Scans done and Unique WiFi scanned.
- Background Mode was hardened with defensive startup, foreground service requirements, boot auto-start, heartbeat tracking, abrupt-ending detection, and a restart path.
- Background Mode setup was streamlined into a single in-app surface with inline guidance instead of stacked app-owned pop-ups.
- Android build warning from `android_intent_plus` was removed by vendoring and patching the plugin source.

## Proof Points

- `flutter build apk` completed successfully and produced an 89.7MB release APK.
- Auth regression tests cover Google sign-in, Apple sign-in, Skip for now, and live counter rendering.
- Background Mode tests cover interval validation, paid-window replacement behavior, abrupt-ending detection, health recovery UI, and history notices.
- Visual golden tests cover Network Guardian home display, score overlay, and scan history across Android and iOS viewports.
- 2026-05-10 audit reran auth, background health, background history, and visual tests successfully.

## Source Map

- APK: `flutter_app/build/app/outputs/flutter-apk/app-release.apk`, timestamp 2026-05-09 12:39:08 +0530. No app source, test, pubspec, Android manifest, or vendored plugin source files were newer than the APK at audit time; only Gradle cache lock files were newer.
- Auth UI: `flutter_app/lib/screens/auth/sign_in_screen.dart`, `flutter_app/lib/screens/auth/sign_up_screen.dart`, `flutter_app/lib/widgets/auth_stats_row.dart`.
- Auth test coverage: `flutter_app/test/tc24_auth_signin_test.dart`.
- Background Mode service: `flutter_app/lib/services/background_scan_service.dart`.
- Android foreground/background permissions: `flutter_app/android/app/src/main/AndroidManifest.xml`.
- Background health UI: `flutter_app/lib/screens/home/home_screen.dart`.
- Background test coverage: `flutter_app/test/tc29_background_mode_interval_test.dart`, `flutter_app/test/tc31_background_mode_history_notice_test.dart`.
- Visual coverage: `flutter_app/test/visual_network_guardian_display_test.dart`.
- `android_intent_plus` warning fix: `flutter_app/pubspec.yaml` dependency override to `third_party/android_intent_plus`, with warning suppressions in `third_party/android_intent_plus/android/src/main/java/dev/fluttercommunity/plus/androidintent/MethodCallHandlerImpl.java`.

## Verification Commands

- `flutter test test/tc24_auth_signin_test.dart test/tc29_background_mode_interval_test.dart test/tc31_background_mode_history_notice_test.dart test/visual_network_guardian_display_test.dart`
- `find flutter_app/lib flutter_app/test flutter_app/android flutter_app/pubspec.yaml flutter_app/pubspec.lock flutter_app/third_party -type f -newer flutter_app/build/app/outputs/flutter-apk/app-release.apk`

## Content Angles

- Public WiFi should have a visible trust layer, not a blind leap of faith.
- Background protection only matters if the product detects when Android or OEM battery policy cuts it off.
- Trust products need honest failure states: if background scanning was interrupted, users should see it and get a recovery path.
- Consumer security UX should consolidate permission and setup friction instead of stacking modal prompts.
- Community network intelligence gets stronger when every scan contributes to WiFi Scans done and Unique WiFi scanned.

## Preferred CTA

Try the Android release build, scan the WiFi you are on, and help build the public WiFi trust map.

## Do Not Claim Yet

- Do not claim full protection after a true Android Force stop or aggressive OEM battery kill. Say the app can detect likely interruption and guide recovery.
- Do not claim continuous background scanning if the user exits, force-stops, denies permissions, or battery policy stops the service.
- Do not claim iOS background scanning parity.
