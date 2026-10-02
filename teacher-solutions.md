# Разбор для преподавателя

Опубликуйте этот разбор после самостоятельной работы. Сейчас он не включён в студенческий репозиторий и статью Academy.

## Маршрут A

Удаляем пробелы по краям и используем запасное имя для отсутствующей или пустой строки:

```kotlin
package kfd

fun displayName(name: String?): String {
    val normalized = name?.trim()
    if (normalized == null || normalized.isEmpty()) {
        return "Гость"
    }
    return normalized
}
```

Пять требований покрыты тестами в `03-teacher-solution/app/src/test/kotlin/kfd/DisplayNameTest.kt`.

## Маршрут B

В исходной функции два вида проблем: `!!` приводит к исключению для разрешённого аргумента null; строгое сравнение `<` запрещает длину, равную лимиту. Исходный тест проверяет обычную короткую строку, поэтому обе проблемы остаются незамеченными.

Один из корректных вариантов:

```kotlin
package kfd

fun canSendMessage(
    text: String?,
    maxLength: Int = 140
): Boolean {
    if (text == null || maxLength <= 0) {
        return false
    }
    return text.isNotEmpty() && text.length <= maxLength
}
```

После раннего выхода при `text == null` Kotlin знает, что в оставшейся части функции `text` — непустая ссылка на String (само содержимое строки ещё может быть пустым). Проверка `isNotEmpty()` отвечает уже за содержимое. Именованные аргументы явно показывают, какой лимит проверяется; вызовы без maxLength проверяют значение по умолчанию.

Пример набора тестов:

```kotlin
package kfd

import org.junit.jupiter.api.Assertions.assertFalse
import org.junit.jupiter.api.Assertions.assertTrue
import org.junit.jupiter.api.Test

class MessagePolicyTest {
    @Test
    fun acceptsShortMessage() {
        assertTrue(canSendMessage("Привет"))
    }

    @Test
    fun rejectsMissingMessage() {
        assertFalse(canSendMessage(null))
    }

    @Test
    fun rejectsEmptyMessage() {
        assertFalse(canSendMessage(""))
    }

    @Test
    fun acceptsBelowExplicitLimit() {
        assertTrue(canSendMessage(text = "Ко", maxLength = 3))
    }

    @Test
    fun acceptsAtExplicitLimit() {
        assertTrue(canSendMessage(text = "Кот", maxLength = 3))
    }

    @Test
    fun rejectsAboveExplicitLimit() {
        assertFalse(canSendMessage(text = "Коты", maxLength = 3))
    }

    @Test
    fun rejectsZeroLimit() {
        assertFalse(canSendMessage(text = "А", maxLength = 0))
    }

    @Test
    fun rejectsNegativeLimit() {
        assertFalse(canSendMessage(text = "А", maxLength = -1))
    }

    @Test
    fun acceptsAtDefaultLimit() {
        assertTrue(canSendMessage("А".repeat(140)))
    }

    @Test
    fun rejectsAboveDefaultLimit() {
        assertFalse(canSendMessage("А".repeat(141)))
    }

    @Test
    fun countsSpacesWithoutTrimming() {
        assertTrue(canSendMessage(text = "   ", maxLength = 4))
    }
}
```

На исходной реализации из этих 11 тестов падают три: отсутствующий текст, граница заданного лимита и граница лимита по умолчанию. Остальные восемь проходят. Это три примера, обнаруживающие два вида ошибок.

Строка из пробелов разрешена, если её длина укладывается в лимит: задание не требует trim или isBlank. Не переносите требования маршрута A в маршрут B.

Зелёный CI подтверждает только выполненные проверки. Число тестов в эталоне не является обязательным для студентов: сравнивайте покрытие требований и поведение, а не текст реализации.
