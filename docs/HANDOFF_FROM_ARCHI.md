# Передача з сесії ARCHI 14.11.2026 (факти, live n8n)

## Що це за workflow
- ID `YcbuzP4ii03B6Mtk`, імʼя «My workflow 2», створено 02.06.2026, 19 вузлів, активний.
- Тригер: Telegram Trigger (message, callback_query). Розкладів немає.
- Switch: `/start` → HTTP-запит з inline-меню; callback_query → Code-вузол зі статичними меню (аварії, оплата, лічильники, контакти, звернення) → HTTP-запит у Telegram; решта тексту → AI Agent.
- AI Agent: Claude Haiku 4.5, Postgres Chat Memory (ключ: Telegram `from.id`, таблиця `n8n_chat_histories`, вікно 10).
- Інструменти агента: Google Docs (юрист, курс управителя, паспорт будинку, база законів), Google Sheets (реєстр документів, критичні знахідки, реєстр співвласників). Pinecone (`zhkg-agent`, `stritenska-17`) вимкнено.

## Що знайдено (не змінювалось)
1. Токен Telegram-бота записаний прямо в URL трьох HTTP-вузлів (`HTTP Request`, `HTTP Request1`, фрагмент меню). Потрібно: перенести в credential n8n і відкликати токен у BotFather.
2. Реєстр співвласників (персональні дані) доступний агентові як інструмент: переглянути, хто і що може запитати.
3. Спільні з ARCHI ресурси: credential Anthropic, credential OpenAI, база Postgres, ліміт виконань тарифу.
4. Робоча версія відрізняється від активної (`versionId` ≠ `activeVersionId`) станом на 14.11.2026 через зміну налаштування MCP.
5. У листопаді 0 виконань.

## Інші workflow ОСББ на тому ж n8n (за списком 14.11.2026; не перевірені детально)
- OSBB Copilot v3 — Routing (`fdkFyjbTXhpDamB3`), активний, Telegram Trigger.
- Drive Auto-Indexer v1 (`NA9QHCDM306kVL4u`), активний, розклад раз на добу, 7 виконань у листопаді.
- Dental Shift Report Bot, ABMK COO Agent, Task Dispatcher, KB Reindex, OSBB Passport Doc Reader, OSBB Error Handler: активні; за листопад виконань 0.
- Решта з ~80 workflow: вимкнені тимчасові й діагностичні.

## З чого почати наступну сесію
1. Вирішити з власником, який workflow з перелічених є продуктом «ЖКГ-Агент», а які застарілі.
2. Експортувати їх в `workflows/` (токени замінити заглушкою).
3. Перенести токен у credential. Це зміна живого n8n: лише після «так».
