# kfd-engineering-loop-practice-demo

Демонстрационный проект для занятия «Инженерный контур».

## Начальное состояние

- `displayName` преобразует аргумент в строку; обработка отсутствующего имени ещё не реализована.
- Единственный тест проверяет обычное имя и проходит.
- GitHub Actions выполняет только `Assemble`.

Откройте эту папку в IntelliJ IDEA как Gradle-проект. Основной код находится в `app/src/main/kotlin/kfd/DisplayName.kt`, тест — в `app/src/test/kotlin/kfd/DisplayNameTest.kt`.

## Запуск

В терминале PowerShell из корня проекта:

```powershell
.\gradlew.bat assemble
.\gradlew.bat test --rerun-tasks
```

В Bash:

```bash
bash ./gradlew assemble
bash ./gradlew test --rerun-tasks
```

Ожидается 1 успешный тест. В IDEA можно запустить весь класс `DisplayNameTest` стрелкой рядом с его объявлением.

## Ход демонстрации

1. Запустите исходный тест и обсудите, что именно он подтверждает.
2. Добавьте тест: для `null` ожидается `"Гость"`. Покажите падение теста.
3. После подключения GitHub-репозитория отправьте изменение: CI с одним `Assemble` останется зелёным.
4. В `.github/workflows/ci.yml` добавьте после `Assemble` шаг `Test` с командой `bash ./gradlew test --no-daemon`. Отправьте изменение и покажите падение CI.
5. Исправьте функцию на `name ?: "Гость"`. Запустите тесты локально и отправьте изменение, чтобы получить зелёный CI.

Локальный репозиторий создан в ветке `main`. Начальное состояние отмечено тегом `lesson-start`. Удалённый репозиторий пока не подключён: автоматические запуски Actions появятся после публикации на GitHub.

Готовая база для студентов: [kfd-engineering-loop-practice](https://github.com/nikitosion/kfd-engineering-loop-practice). Она уже содержит обработку `null`, два теста и CI со сборкой и тестами.
