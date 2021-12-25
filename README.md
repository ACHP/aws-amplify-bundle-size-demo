## What is this repository

This is a simple react-native v0.67 app created with `npx react-native init targetNameDemo --version 0.67.0-rc.6`
Its purpose is to demonstrate a bug in `node_modules/react-native/react.gradle`.
The bug cause the final apk to contains necessary binaries(.so files) when using *build flavor*.

When using `internal` and `public` Build flavor for instance, the script tries to delete binaries in this folder (using `variant.dirName`):
```
android/app/build/intermediates/merged_native_libs/internal/release/...
```
But the correct path is this one:
```
android/app/build/intermediates/merged_native_libs/internalRelease/..
```

This can be solved easily using `variant.name` instead of `variant.dirName`

## Why the bug hasn't been seen before

The "bug" only appears when using buildVariant.
It works perfectly fine otherwise because `targetPath` will be `debug` or `internal` anyway.
