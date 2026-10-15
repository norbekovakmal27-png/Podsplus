name: Build APK
on: [push, workflow_dispatch]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: 17
      - uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: 8.9
      - run: unzip -q PodPulse.zip
      - run: gradle assembleDebug --no-daemon
        working-directory: PodPulse
      - uses: actions/upload-artifact@v4
        with:
          name: PodPulse-apk
          path: PodPulse/app/build/outputs/apk/debug/app-debug.apk
