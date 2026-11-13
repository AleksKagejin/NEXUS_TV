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

      - name: Установить Java 17
        uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: 17

      - name: Распаковать проект
        run: |
          mkdir project
          unzip -q NEXUS-TV-project-fixed.zip -d project
          find project -name gradlew -type f

      - name: Собрать APK
        run: |
          GRADLEW=$(find project -name gradlew -type f | head -n 1)
          chmod +x "$GRADLEW"
          cd "$(dirname "$GRADLEW")"
          ./gradlew assembleDebug

      - name: Сохранить APK
        uses: actions/upload-artifact@v4
        with:
          name: NEXUS-TV-APK
          path: project/**/build/outputs/apk/debug/*.apk
