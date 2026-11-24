name: Build APK
on:
  push:
  workflow_dispatch:
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
      - name: Unzip project
        run: |
          ZIP=$(ls *.zip | tail -1)
          unzip -q "$ZIP" -d project
          APPDIR=$(dirname "$(find project -name settings.gradle.kts | head -1)")
          echo "APPDIR=$APPDIR" >> $GITHUB_ENV
      - name: Build debug APK
        run: gradle -p "$APPDIR" assembleDebug --stacktrace
      - uses: actions/upload-artifact@v4
        with:
          name: aura-x-apk
          path: ${{ env.APPDIR }}/app/build/outputs/apk/debug/*.apk
