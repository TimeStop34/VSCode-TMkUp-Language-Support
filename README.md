# TMkUp Language Support for VS Code

Официальная поддержка языка разметки **TMkUp v2.0** в Visual Studio Code.

TMkUp (Text Markup) — язык разметки для текстовой сети **TNet**, сочетающий простоту Markdown с ANSI-цветами, интерактивными формами и совместимостью с Gopher.

## Features

### Подсветка синтаксиса

Полная подсветка всех элементов TMkUp, совместимая с любыми темами VS Code (как в Markdown):

- **Заголовки** всех уровней (`# H1 #` … `###### H6 ######`)
- **Стили текста**: `*курсив*`, `**жирный**`, `***жирный курсив***`, `~~зачёркнутый~~`, `==выделенный==`, `^верхний^`, `~нижний~`
- **ANSI-цвета**: `{red}…{/red}`, `{bg-blue}…{/bg-blue}`, яркие (`{bred}`, `{bg-bgreen}`), сброс `{/}`
- **Списки**: маркированные, нумерованные, задачи (`[ ]`, `[x]`, `[~]`), определения
- **Ссылки и изображения**: `[текст](url)`, `![alt](img.png {height=90})`
- **Блоки кода**: встроенные `` `code` `` и многострочные ` ```lang `
- **Специальные блоки**: информационные (`!!!`), цветные (`%%`), спойлеры (`???`)
- **Формы**: `@@ … @@` с полями, чекбоксами, радиокнопками, select'ами
- **Таблицы** с выравниванием
- **Сноски**: `[^1]` и `[^1]: текст`
- **Комментарии**: `//` и `/* … */`
- **Переменные**: `{{ variable }}`
- **Gopher-директивы**: `@@gopher-type … @@endgopher`
- **Метаданные**: `---tmk-meta … ---tmk-meta`

### Автозакрытие пар

Автоматически закрываются:

- Скобки и кавычки: `{}`, `[]`, `()`, `` ` ``, `""`
- Стили: `*`, `**`, `_`, `~~`, `==`
- Блоки: `!!!`, `%%`, `???`, `@@`, ` ``` `, `---tmk-meta`
- Блочные теги: `[radio]…[/radio]`, `[select]…[/select]`, `@@gopher-type…@@endgopher`
- Цветовые теги: `{red}…{/red}`, `{bg-blue}…{/bg-blue}` и другие

### Сворачивание блоков

Сворачиваются все блочные конструкции:

- `!!! … !!!`
- `%% … %%`
- `??? … ???`
- `@@ … @@`
- `[radio] … [/radio]`
- `[select] … [/select]`
- `@@gopher-type … @@endgopher`
- ` ``` … ``` `
- `---tmk-meta … ---tmk-meta`

### Автоотступы

При входе в блок (после `!!!`, `%%`, `@@`, `[radio]`, `[select]`) автоматически ставится отступ. При закрытии — отступ убирается.

## Requirements

Никаких зависимостей. Расширение работает сразу после установки.

- VS Code `^1.60.0` или выше.

## Extension Settings

Расширение не добавляет собственных настроек. Цвета подсветки настраиваются через стандартный механизм тем VS Code.

Пример кастомизации цветов для элементов TMkUp в `settings.json`:

```json
"editor.tokenColorCustomizations": {
    "textMateRules": [
        {
            "scope": "markup.heading.tmkup",
            "settings": { "foreground": "#569CD6", "fontStyle": "bold" }
        },
        {
            "scope": "support.constant.color.tmkup",
            "settings": { "foreground": "#CE9178" }
        },
        {
            "scope": "keyword.control.radio.tmkup",
            "settings": { "foreground": "#C586C0" }
        },
        {
            "scope": "punctuation.definition.block.begin.tmkup",
            "settings": { "foreground": "#808080" }
        }
    ]
}
```

## Пример файла

```tmkup
---tmk-meta
title: "Добро пожаловать в TNet"
author: "admin"
---tmk-meta

# Главная страница

*Добро пожаловать* в **TNet** — новую текстовую сеть.

{green}Этот текст зелёный.{/green}

## Навигация

- [Главная](/index.tmkup)
- [О проекте](/about.tmkup)

## Спойлер

??? {title="Показать ответ"}
Секретный ответ: **42**
???

## Форма

@@ {action="/feedback" method="post"}

[Имя] {type="text" name="name" required}

[radio name="gender"]
  [Мужской] {value="male" checked}
  [Женский] {value="female"}
[/radio]

[Отправить] {type="submit"}
@@
```

## Known Issues

- VS Code не всегда корректно обрабатывает `surroundingPairs` с одинаковыми открывающими и закрывающими маркерами (`!!!…!!!`, `%%…%%`, `???…???`, `@@…@@`).
- Автозакрытие блоков (например, `!!!`) не поддерживается нативно — нужно вручную дописывать закрывающий маркер.

## Release Notes

### 2.0.0

Первый публичный релиз с поддержкой **TMkUp v2.0**:

- Полная подсветка синтаксиса
- Автозакрытие пар и стилей
- Сворачивание всех блочных конструкций
- Автоотступы для блоков, форм и радиокнопок
- Совместимость с темами VS Code для Markdown

## Ссылки

- [Официальный репозиторий TMkUp](https://github.com/TimeStop34/tmkup)
- [Официальный репозиторий TNet](https://github.com/TimeStop34/tnet-protocols)
- [Репозиторий расширения TMkUp v2.0 для VSCode](https://github.com/TimeStop34/vscode-tmkup-language-support)
- [VS Code Markdown Support](https://code.visualstudio.com/docs/languages/markdown)

## Лицензия

[GNU GPL v3.0](https://github.com/TimeStop34/vscode-tmkup-language-support/LICENSE)