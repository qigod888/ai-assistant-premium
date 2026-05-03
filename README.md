# AI Assistant Premium — Production Ready

Премиум AI-ассистент с визуальным аватаром, готовый к деплою на Vercel/Netlify.

## Быстрый деплой на Vercel

### 1. Установи Vercel CLI (если ещё нет)
```bash
npm install -g vercel
```

### 2. Деплой проекта
```bash
cd ai-assistant-vercel
vercel
```

При первом запуске:
- Vercel спросит, создать ли новый проект → **Yes**
- Спросит название → придумай любое
- Выбери настройки по умолчанию (Enter, Enter, Enter)

### 3. Настрой переменную окружения (API ключ)

После деплоя зайди в **Vercel Dashboard** → твой проект → Settings → Environment Variables:

- **Key**: `GROQ_API_KEY`
- **Value**: `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`
- **Environments**: Production, Preview, Development (выбрать все)

Нажми **Save**.

### 4. Передеплой
```bash
vercel --prod
```

Готово! Vercel даст тебе URL типа `https://твой-проект.vercel.app` — открывай с любого устройства.

---

## Альтернатива: Netlify

### 1. Создай файл `netlify.toml` в корне:
```toml
[build]
  functions = "api"

[[redirects]]
  from = "/api/*"
  to = "/.netlify/functions/:splat"
  status = 200
```

### 2. Переименуй папку `api` → `netlify/functions`

### 3. Деплой через Netlify CLI или GitHub

---

## Переход на платный API

Когда купишь Gemini/OpenAI ключ:

1. Открой `api/chat.js`
2. Измени URL и формат запроса:

```js
// Для Gemini
const response = await fetch(
  `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${GEMINI_KEY}`,
  {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      contents: [
        { parts: [{ text: messages[messages.length - 1].content }] }
      ]
    })
  }
);
```

3. Обнови переменную окружения `GROQ_API_KEY` → `GEMINI_API_KEY` в Vercel

---

## Структура проекта

```
ai-assistant-vercel/
├── index.html          # Фронтенд (весь UI)
├── api/
│   └── chat.js         # Serverless function (прокси к AI API)
├── package.json
├── vercel.json
└── README.md
```

---

## Фичи

✅ Работает на **всех устройствах** (ПК, планшеты, смартфоны)  
✅ **Нет CORS-проблем** (запросы идут через твой backend)  
✅ **Премиум UI**: строгий минимализм, анимации, голос  
✅ **Готов к продакшну**: просто заменишь API ключ  
✅ **Бесплатный хостинг** на Vercel/Netlify  

---

Вопросы? Открой issue или пиши мне.
