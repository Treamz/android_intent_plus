# Android Intent Plugin for Flutter

[![Flutter Community: android_intent_plus](https://fluttercommunity.dev/_github/header/android_intent_plus)](https://github.com/fluttercommunity/community)

[![pub package](https://img.shields.io/pub/v/android_intent_plus.svg)](https://pub.dev/packages/android_intent_plus)
[![android_intent_plus](https://github.com/fluttercommunity/plus_plugins/actions/workflows/android_intent_plus.yaml/badge.svg)](https://github.com/fluttercommunity/plus_plugins/actions/workflows/android_intent_plus.yaml)

<center><a href="https://flutter.dev/docs/development/packages-and-plugins/favorites" target="_blank" rel="noreferrer noopener"><img src="../../website/static/img/flutter-favorite-badge.png" width="100" alt="build"></a></center>

This plugin allows Flutter apps to launch arbitrary intents when the platform
is Android. If the plugin is invoked on iOS, it will crash your app. In checked
mode, we assert that the platform should be Android.

Use it by specifying action, category, data and extra arguments for the intent.
It does not support returning the result of the launched activity. Sample usage:

```dart
if (platform.isAndroid) {
  AndroidIntent intent = AndroidIntent(
      action: 'action_view',
      data: 'https://play.google.com/store/apps/details?'
          'id=com.google.android.apps.myapp',
      arguments: {'authAccount': currentUserEmail},
  );
  await intent.launch();
}
```

See documentation on the AndroidIntent class for details on each parameter.

Action parameter can be any action including a custom class name to be invoked.
If a standard android action is required, the recommendation is to add support
for it in the plugin and use an action constant to refer to it. For instance:

`'action_view'` translates to `android.os.Intent.ACTION_VIEW`

`'action_location_source_settings'` translates to `android.settings.LOCATION_SOURCE_SETTINGS`

`'action_application_details_settings'` translates to `android.settings.ACTION_APPLICATION_DETAILS_SETTINGS`

```dart
if (platform.isAndroid) {
  final AndroidIntent intent = AndroidIntent(
    action: 'action_application_details_settings',
    data: 'package:com.example.app', // replace com.example.app with your applicationId
  );
  await intent.launch();
}

```

Feel free to add support for additional Android intents.

The Dart values supported for the arguments parameter, and their corresponding
Android values, are listed [here](https://flutter.dev/platform-channels/#codec).
On the Android side, the arguments are used to populate an Android `Bundle`
instance. This process currently restricts the use of lists to homogeneous lists
of integers or strings.

> Note that a similar method does not currently exist for iOS. Instead, the
> [url_launcher](https://pub.dartlang.org/packages/url_launcher) plugin
> can be used for deep linking. Url launcher can also be used for creating
> ACTION_VIEW intents for Android, however this intent plugin also allows
> clients to set extra parameters for the intent.

## Platform Support

| Android |
| :-----: |
|   ✔️    |

Check out our documentation website to learn more. [Plus plugins documentation](https://plus.fluttercommunity.dev/docs/overview)

**Important:** As of January 2021, the Flutter team is no longer accepting non-critical PRs for the original set of plugins in `flutter/plugins`, and instead they should be submitted in this project. [You can read more about this announcement here.](https://github.com/flutter/plugins/blob/master/CONTRIBUTING.md#important-note) as well as [in the Flutter 2 announcement blog post.](https://medium.com/flutter/whats-new-in-flutter-2-0-fe8e95ecc65)