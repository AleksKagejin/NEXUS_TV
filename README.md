
name: Сборка NEXUS-TV

on:
  workflow_dispatch:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Получить файлы
        uses: actions/checkout@v4

      - name: Установить Java
        uses: actions/setup-java@v5
        with:
          distribution: temurin
          java-version: '17'

      - name: Установить Gradle
        uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: '8.7'

      - name: Проверить проект
        run: |
          ls -la
          test -d app
          test -f settings.gradle.kts

      - name: Собрать APK
        run: gradle assembleDebug

      - name: Сохранить APK
        uses: actions/upload-artifact@v4
        with:
          name: NEXUS-TV-APK
          path: app/build/outputs/apk/debug/*.apk
          if-no-files-found: error
          
