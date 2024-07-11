# Commands related to Flutter

## reinstall

> flutter clean and pub get

```sh
flutter clean
flutter pub get
```

## pod-reinstall

> flutter ios Pods delete and install --repo-update

```sh
cd ios
rm -rf Pods
rm -rf Podfile.lock
pod install --repo-update
pod cache clean --all
cd ..
```
