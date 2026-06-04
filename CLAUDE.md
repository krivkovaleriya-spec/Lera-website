# CLAUDE.md — Личный сайт Валерии Кривко

**URL:** https://valeriyavaly.github.io/  
**Платформа:** GitHub Pages (не Tilda — нет ограничений платформы)  
**Репо:** remote уже настроен (`origin/main`)

---

## Структура проекта

```
lera-website/
├── index.html            # Всё в одном файле — весь сайт
├── cases-standalone.html # Отдельная страница кейсов
├── llms.txt              # Для AI-поисковиков (ChatGPT, Perplexity, Claude)
├── TODO.md               # Список доработок с приоритетами
├── images/               # Все скрины кейсов, фото Лерчика
└── video/                # Видео (пока не подключено на сайте)
```

---

## Стек и дизайн

- **Тёмная тема:** `#0a0a0a` фон, `#f0f0e8` текст
- **Шрифты:** Space Grotesk (заголовки) + Inter (текст) + JetBrains Mono (метки/моно)
- **Акцент:** `oklch(var(--g-lit) var(--g-sat) var(--g-hue))` — настраиваемый зелёный (hue 130)
- **Кастомный курсор** с магнетизмом (`[data-magnetic]`)
- **Tweaks-панель** — ⚙ кнопка, настройка цвета прямо в браузере
- **Бургер-меню** для мобилки (`#burger` + `.nav-mobile`)
- **Preview bar** — Desktop / Tablet·1024 / Mobile·390 (iframe той же страницы, внутри iframe бар скрыт)

---

## Контакты на сайте

- WhatsApp: `https://wa.me/+77775481717`
- Telegram: `https://t.me/valeriyavaly`
- Instagram: `https://www.instagram.com/valeriyavaly`
- Email: `mailto:krivko.valeriya@gmail.com`

---

## Правила работы

- Контент только реальный — ничего не придумывать (цифры, отзывы, кейсы)
- GitHub Pages: нет серверного рендеринга, нет PHP, всё статика
- Cloudflare email protection не использовать — несовместимо с GitHub Pages (заменено на `mailto:`)
- `!important` на `color` для `<a>` не нужен (это не Tilda)
- Мобилку менять прямо в HTML/CSS, никакого `#course-emulator`

---

## Деплой

```bash
cd "d:\Claude Code\lera-website"
git add -A
git commit -m "..."
git push origin main
```

GitHub Pages автоматически публикует через ~1–2 минуты.

---

## Что сделано

- JSON-LD Schema (Person + ProfessionalService + FAQPage)
- llms.txt
- FAQ секция (8 вопросов)
- Мобильная адаптация кейсов
- Страница cases-standalone.html
- Плавающие кнопки WhatsApp + Telegram
- Кастомный курсор с magnetic-эффектом
- Секция визуала GetCourse (flip-карточки)
- Реальные скрины кейсов в images/

## Что ещё не сделано (см. TODO.md)

- Отзывы — добавить реальные имена и ниши
- Кейсы — добавить метрики (цифры реальные, не выдуманные)
- ИИ-продавец — добавить скриншот/gif диалога
- Hero — усилить оффер под клиента
- Lead magnet — сделать конкретным
- sitemap.xml + robots.txt
- og:image брендированный баннер 1200×630
- Расширить llms.txt (методология, этапы работы)
