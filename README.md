# kfd-engineering-loop-practice-demo

Демонстрационный проект занятия «Инженерный контур». Откройте эту папку в IDEA.

Начальное состояние: displayName с исходной ошибкой, один проходящий тест, CI только Assemble. Тег lesson-start отмечает исходную версию; исходный код пока не исправлен, чтобы показать цикл на занятии.

[Пошаговый сценарий преподавателя](TEACHER_RUNBOOK.md).

```powershell
.\gradlew.bat assemble
.\gradlew.bat test --rerun-tasks
```

В Bash: `bash ./gradlew assemble` и `bash ./gradlew test --rerun-tasks`.

Ожидается 1 успешный тест. Студенческая база находится в [kfd-engineering-loop-practice](https://github.com/nikitosion/kfd-engineering-loop-practice) и уже содержит два теста и два шага CI. Исходный проект демонстрации и готовая студенческая база различаются намеренно.

Проект остаётся локальным по решению преподавателя: remote не подключён. Для показа GitHub Actions используйте готовый запуск студенческого шаблона, а падение и исправление демонстрируйте в локальном терминале.
