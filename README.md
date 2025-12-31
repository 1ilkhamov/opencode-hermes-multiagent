# 🔱 Hermes Multi-Agent System for OpenCode AI

<div align="center">

**[English](#english) | [Русский](#russian)**

[![OpenCode AI](https://img.shields.io/badge/OpenCode-AI-blue?style=for-the-badge)](https://opencode.ai)
[![Agents](https://img.shields.io/badge/Agents-17-green?style=for-the-badge)]()
[![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)]()

</div>

---

<a name="english"></a>
## 🇬🇧 English

### Overview

Hermes is a sophisticated multi-agent orchestration system designed for OpenCode AI. It coordinates 17 specialized AI agents to handle complex software development tasks — from research and planning to implementation, testing, and deployment.

The system follows a strict pipeline architecture where each agent has a specific role, ensuring quality, security, and consistency across all operations.

### Architecture

```
                              ┌─────────────────────────────────────┐
                              │           🔱 HERMES                 │
                              │      Master Orchestrator            │
                              │      (openai/gpt-5.2-high)          │
                              └─────────────────┬───────────────────┘
                                                │
        ┌───────────────────────────────────────┼───────────────────────────────────────┐
        │                                       │                                       │
        ▼                                       ▼                                       ▼
┌───────────────┐                     ┌───────────────┐                       ┌───────────────┐
│   RESEARCH    │                     │   PLANNING    │                       │IMPLEMENTATION │
├───────────────┤                     ├───────────────┤                       ├───────────────┤
│ @finder       │                     │ @architect    │                       │ @coder        │
│ @analyst      │                     │ @planner      │                       │ @editor       │
│ @researcher   │                     └───────────────┘                       │ @fixer        │
└───────────────┘                                                             │ @refactorer   │
                                                                              └───────────────┘
        ┌───────────────────────────────────────┼───────────────────────────────────────┐
        │                                       │                                       │
        ▼                                       ▼                                       ▼
┌───────────────┐                     ┌───────────────┐                       ┌───────────────┐
│    QUALITY    │                     │ DOCUMENTATION │                       │INFRASTRUCTURE │
├───────────────┤                     ├───────────────┤                       ├───────────────┤
│ @reviewer     │                     │ @documenter   │                       │ @devops       │
│ @tester       │                     │ @commenter    │                       │ @optimizer    │
│ @debugger     │                     └───────────────┘                       └───────────────┘
│ @security     │
└───────────────┘
```

### Agents

#### 🔱 Hermes — Master Orchestrator
- **Model:** `openai/gpt-5.2-high`
- **Role:** Routes requests, manages pipelines, coordinates agents, handles conflicts
- **Tools:** `task`, `todowrite`, `todoread`

#### 🔍 Research Agents

| Agent | Model | Role |
|-------|-------|------|
| **@finder** | `gemini-3-flash` | Fast codebase scout. Finds files, patterns, project structure |
| **@analyst** | `sonnet-4.5-thinking-high` | Deep code analysis. Dependencies, risks, data flow |
| **@researcher** | `sonnet-4.5-thinking-low` | External knowledge. Documentation, best practices, solutions |

#### 📐 Planning Agents

| Agent | Model | Role |
|-------|-------|------|
| **@architect** | `opus-4.5-thinking-medium` | Solution design. Components, interfaces, integration |
| **@planner** | `gemini-3-flash` | Task decomposition. Atomic tasks, dependencies, ordering |

#### 💻 Implementation Agents

| Agent | Model | Role |
|-------|-------|------|
| **@coder** | `opus-4.5-thinking-high` | Creates new code. Files, functions, classes |
| **@editor** | `opus-4.5-thinking-high` | Modifies existing code. Safe changes, backward compatibility |
| **@fixer** | `sonnet-4.5-thinking-high` | Fixes bugs. Minimal changes, root cause fixes |
| **@refactorer** | `sonnet-4.5-thinking-high` | Improves structure. Same behavior, better code |

#### ✅ Quality Agents

| Agent | Model | Role |
|-------|-------|------|
| **@reviewer** | `gpt-5.2-codex-xhigh` | Code review. Quality, best practices, issues |
| **@tester** | `gpt-5.2-codex-xhigh` | Testing. Unit tests, integration tests, coverage |
| **@debugger** | `sonnet-4.5-thinking-high` | Bug investigation. Root cause analysis, diagnosis |
| **@security** | `gpt-5.2-codex-xhigh` | Security audit. Vulnerabilities, compliance, OWASP |

#### 📚 Documentation Agents

| Agent | Model | Role |
|-------|-------|------|
| **@documenter** | `sonnet-4.5-thinking-medium` | Technical docs. README, API docs, guides |
| **@commenter** | `sonnet-4.5-thinking-low` | Code comments. JSDoc, inline comments |

#### 🔧 Infrastructure Agents

| Agent | Model | Role |
|-------|-------|------|
| **@devops** | `sonnet-4.5-thinking-medium` | CI/CD, Docker, deployment, infrastructure |
| **@optimizer** | `sonnet-4.5-thinking-high` | Performance. Bottlenecks, memory, efficiency |

### Pipelines

#### New Feature
```
@finder → @analyst → @architect → @planner → @coder → @reviewer → @tester → @documenter
```

#### New Feature (Security-Related)
```
@finder → @analyst → @researcher → @architect → @planner → @coder → @reviewer → @security → @tester → @documenter
```

#### Bug Fix (Unknown Cause)
```
@finder → @debugger → @fixer → @reviewer → @tester
```

#### Bug Fix (Known Cause)
```
@finder → @fixer → @reviewer → @tester
```

#### Refactoring
```
@finder → @analyst → @refactorer → @reviewer → @tester
```

#### Performance Optimization
```
@finder → @analyst → @optimizer → @reviewer → @tester
```

#### Infrastructure Changes
```
@finder → @devops → @reviewer → @tester
```

### Key Features

- **Mandatory Quality Gates:** `@reviewer` and `@tester` run after every code change
- **Security First:** `@security` is mandatory for auth, user data, secrets
- **Checkpoints:** User confirmation required between phases
- **Revision Loops:** Up to 3 iterations for fixes before escalation
- **Context Passing:** Full context flows between all agents
- **Session Learning:** System learns from repeated issues
- **Conflict Resolution:** Priority-based resolution (security > quality > implementation)

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd hermes-agents
```

2. Install dependencies:
```bash
bun install
# or
npm install
```

3. Configure OpenCode AI to use the agent system:
```bash
# Copy agent files to OpenCode config
cp -r agent ~/.config/opencode/
```

4. Set up MCP servers (for @researcher):
```bash
# Context7 for library documentation
npx -y @upstash/context7-mcp

# Fetch for web pages
uvx mcp-server-fetch
```

### Usage

The system activates automatically when you use OpenCode AI. Hermes analyzes your request and routes it to the appropriate pipeline.

**Examples:**

```
"Add user authentication with JWT"
→ Security-related feature pipeline

"Fix the login bug"
→ Bug fix pipeline (debugger if cause unknown)

"Refactor the UserService"
→ Refactoring pipeline

"Optimize database queries"
→ Performance pipeline
```

### Configuration

All configuration is in `opencode.json`:

- **Models:** Customize models for each agent
- **Tools:** Enable/disable tools per agent
- **MCP:** Configure external tool servers
- **LSP:** Language Server Protocol integration

### Project Structure

```
agent/
├── core/
│   └── hermes.md          # Master orchestrator
└── subagents/
    ├── research/
    │   ├── finder.md      # Codebase scout
    │   ├── analyst.md     # Code analyst
    │   └── researcher.md  # External knowledge
    ├── planning/
    │   ├── architect.md   # Solution design
    │   └── planner.md     # Task decomposition
    ├── implementation/
    │   ├── coder.md       # Code writer
    │   ├── editor.md      # Code editor
    │   ├── fixer.md       # Bug fixer
    │   └── refactorer.md  # Code refactorer
    ├── quality/
    │   ├── reviewer.md    # Code reviewer
    │   ├── tester.md      # Test engineer
    │   ├── debugger.md    # Bug investigator
    │   └── security.md    # Security auditor
    ├── documentation/
    │   ├── documenter.md  # Technical writer
    │   └── commenter.md   # Code commenter
    └── infrastructure/
        ├── devops.md      # DevOps engineer
        └── optimizer.md   # Performance optimizer
```

---

<a name="russian"></a>
## 🇷🇺 Русский

### Обзор

Hermes — это продвинутая мультиагентная система оркестрации для OpenCode AI. Она координирует 17 специализированных ИИ-агентов для выполнения сложных задач разработки — от исследования и планирования до реализации, тестирования и деплоя.

Система следует строгой пайплайн-архитектуре, где каждый агент имеет определённую роль, обеспечивая качество, безопасность и согласованность всех операций.

### Архитектура

```
                              ┌─────────────────────────────────────┐
                              │           🔱 HERMES                 │
                              │      Главный Оркестратор            │
                              │      (openai/gpt-5.2-high)          │
                              └─────────────────┬───────────────────┘
                                                │
        ┌───────────────────────────────────────┼───────────────────────────────────────┐
        │                                       │                                       │
        ▼                                       ▼                                       ▼
┌───────────────┐                     ┌───────────────┐                       ┌───────────────┐
│ ИССЛЕДОВАНИЕ  │                     │ ПЛАНИРОВАНИЕ  │                       │  РЕАЛИЗАЦИЯ   │
├───────────────┤                     ├───────────────┤                       ├───────────────┤
│ @finder       │                     │ @architect    │                       │ @coder        │
│ @analyst      │                     │ @planner      │                       │ @editor       │
│ @researcher   │                     └───────────────┘                       │ @fixer        │
└───────────────┘                                                             │ @refactorer   │
                                                                              └───────────────┘
        ┌───────────────────────────────────────┼───────────────────────────────────────┐
        │                                       │                                       │
        ▼                                       ▼                                       ▼
┌───────────────┐                     ┌───────────────┐                       ┌───────────────┐
│   КАЧЕСТВО    │                     │ ДОКУМЕНТАЦИЯ  │                       │ИНФРАСТРУКТУРА │
├───────────────┤                     ├───────────────┤                       ├───────────────┤
│ @reviewer     │                     │ @documenter   │                       │ @devops       │
│ @tester       │                     │ @commenter    │                       │ @optimizer    │
│ @debugger     │                     └───────────────┘                       └───────────────┘
│ @security     │
└───────────────┘
```

### Агенты

#### 🔱 Hermes — Главный Оркестратор
- **Модель:** `openai/gpt-5.2-high`
- **Роль:** Маршрутизация запросов, управление пайплайнами, координация агентов, разрешение конфликтов
- **Инструменты:** `task`, `todowrite`, `todoread`

#### 🔍 Агенты Исследования

| Агент | Модель | Роль |
|-------|--------|------|
| **@finder** | `gemini-3-flash` | Быстрый поиск по кодовой базе. Файлы, паттерны, структура |
| **@analyst** | `sonnet-4.5-thinking-high` | Глубокий анализ кода. Зависимости, риски, поток данных |
| **@researcher** | `sonnet-4.5-thinking-low` | Внешние знания. Документация, лучшие практики, решения |

#### 📐 Агенты Планирования

| Агент | Модель | Роль |
|-------|--------|------|
| **@architect** | `opus-4.5-thinking-medium` | Проектирование решений. Компоненты, интерфейсы, интеграция |
| **@planner** | `gemini-3-flash` | Декомпозиция задач. Атомарные задачи, зависимости, порядок |

#### 💻 Агенты Реализации

| Агент | Модель | Роль |
|-------|--------|------|
| **@coder** | `opus-4.5-thinking-high` | Создание нового кода. Файлы, функции, классы |
| **@editor** | `opus-4.5-thinking-high` | Модификация существующего кода. Безопасные изменения |
| **@fixer** | `sonnet-4.5-thinking-high` | Исправление багов. Минимальные изменения |
| **@refactorer** | `sonnet-4.5-thinking-high` | Улучшение структуры. То же поведение, лучший код |

#### ✅ Агенты Качества

| Агент | Модель | Роль |
|-------|--------|------|
| **@reviewer** | `gpt-5.2-codex-xhigh` | Код-ревью. Качество, лучшие практики, проблемы |
| **@tester** | `gpt-5.2-codex-xhigh` | Тестирование. Unit-тесты, интеграционные тесты, покрытие |
| **@debugger** | `sonnet-4.5-thinking-high` | Расследование багов. Анализ первопричин, диагностика |
| **@security** | `gpt-5.2-codex-xhigh` | Аудит безопасности. Уязвимости, соответствие, OWASP |

#### 📚 Агенты Документации

| Агент | Модель | Роль |
|-------|--------|------|
| **@documenter** | `sonnet-4.5-thinking-medium` | Техническая документация. README, API docs, гайды |
| **@commenter** | `sonnet-4.5-thinking-low` | Комментарии в коде. JSDoc, inline-комментарии |

#### 🔧 Агенты Инфраструктуры

| Агент | Модель | Роль |
|-------|--------|------|
| **@devops** | `sonnet-4.5-thinking-medium` | CI/CD, Docker, деплой, инфраструктура |
| **@optimizer** | `sonnet-4.5-thinking-high` | Производительность. Узкие места, память, эффективность |

### Пайплайны

#### Новая Фича
```
@finder → @analyst → @architect → @planner → @coder → @reviewer → @tester → @documenter
```

#### Новая Фича (Связанная с Безопасностью)
```
@finder → @analyst → @researcher → @architect → @planner → @coder → @reviewer → @security → @tester → @documenter
```

#### Исправление Бага (Причина Неизвестна)
```
@finder → @debugger → @fixer → @reviewer → @tester
```

#### Исправление Бага (Причина Известна)
```
@finder → @fixer → @reviewer → @tester
```

#### Рефакторинг
```
@finder → @analyst → @refactorer → @reviewer → @tester
```

#### Оптимизация Производительности
```
@finder → @analyst → @optimizer → @reviewer → @tester
```

#### Изменения Инфраструктуры
```
@finder → @devops → @reviewer → @tester
```

### Ключевые Особенности

- **Обязательные Проверки Качества:** `@reviewer` и `@tester` запускаются после каждого изменения кода
- **Безопасность Прежде Всего:** `@security` обязателен для auth, пользовательских данных, секретов
- **Чекпоинты:** Требуется подтверждение пользователя между фазами
- **Циклы Ревизии:** До 3 итераций для исправлений перед эскалацией
- **Передача Контекста:** Полный контекст передаётся между всеми агентами
- **Обучение в Сессии:** Система учится на повторяющихся проблемах
- **Разрешение Конфликтов:** Приоритетное разрешение (безопасность > качество > реализация)

### Установка

1. Клонируйте репозиторий:
```bash
git clone <repository-url>
cd hermes-agents
```

2. Установите зависимости:
```bash
bun install
# или
npm install
```

3. Настройте OpenCode AI для использования системы агентов:
```bash
# Скопируйте файлы агентов в конфиг OpenCode
cp -r agent ~/.config/opencode/
```

4. Настройте MCP серверы (для @researcher):
```bash
# Context7 для документации библиотек
npx -y @upstash/context7-mcp

# Fetch для веб-страниц
uvx mcp-server-fetch
```

### Использование

Система активируется автоматически при использовании OpenCode AI. Hermes анализирует ваш запрос и направляет его в соответствующий пайплайн.

**Примеры:**

```
"Добавь аутентификацию пользователей с JWT"
→ Пайплайн фичи, связанной с безопасностью

"Исправь баг в логине"
→ Пайплайн исправления бага (debugger если причина неизвестна)

"Отрефактори UserService"
→ Пайплайн рефакторинга

"Оптимизируй запросы к базе данных"
→ Пайплайн производительности
```

### Конфигурация

Вся конфигурация в `opencode.json`:

- **Models:** Настройка моделей для каждого агента
- **Tools:** Включение/отключение инструментов для агента
- **MCP:** Конфигурация внешних серверов инструментов
- **LSP:** Интеграция Language Server Protocol

### Структура Проекта

```
agent/
├── core/
│   └── hermes.md          # Главный оркестратор
└── subagents/
    ├── research/
    │   ├── finder.md      # Поиск по кодовой базе
    │   ├── analyst.md     # Анализ кода
    │   └── researcher.md  # Внешние знания
    ├── planning/
    │   ├── architect.md   # Проектирование решений
    │   └── planner.md     # Декомпозиция задач
    ├── implementation/
    │   ├── coder.md       # Написание кода
    │   ├── editor.md      # Редактирование кода
    │   ├── fixer.md       # Исправление багов
    │   └── refactorer.md  # Рефакторинг кода
    ├── quality/
    │   ├── reviewer.md    # Код-ревью
    │   ├── tester.md      # Тестирование
    │   ├── debugger.md    # Расследование багов
    │   └── security.md    # Аудит безопасности
    ├── documentation/
    │   ├── documenter.md  # Техническая документация
    │   └── commenter.md   # Комментарии в коде
    └── infrastructure/
        ├── devops.md      # DevOps инженер
        └── optimizer.md   # Оптимизация производительности
```

---

## License

MIT

## Contributing

Contributions are welcome! Please read the contribution guidelines before submitting a pull request.

---

<div align="center">
  <sub>Built with ❤️ for OpenCode AI</sub>
</div>
