# CLAUDE.md — Личный сайт Валерии Кривко

**URL (RU):** https://valeriyakrivko.com/  
**URL (EN):** https://valeriyakrivko.com/en/  
**GitHub Pages репо:** krivkovaleriya-spec/krivkovaleriya-spec.github.io (или аналог)  
**Платформа:** GitHub Pages (не Tilda — нет ограничений платформы)  
**Кастомный домен:** valeriyakrivko.com (CNAME файл в репо) — с 2026-09-29 переехали с .kz на .com

## Двуязычность

Сайт двуязычный:
- `/` — русская версия (default)
- `/en/` — английская версия
- `/cases/` и `/en/cases/` — кейсы
- Переключатель `RU | EN` есть в хедере и мобильном меню всех 4 страниц
- hreflang теги во всех `<head>` (ru, en, x-default)
- `sitemap.xml` содержит все 4 URL с `<xhtml:link rel="alternate">`
- `/en/llms.txt` — отдельный английский llms.txt для AI-поисковиков

Правки текста делать в обоих версиях одновременно. Цены в EN: USD/EUR/GBP (курс 1 USD ≈ 475 KZT).

---

## Структура проекта

```
lera-website/
├── index.html              # RU главная
├── cases/index.html        # RU кейсы
├── cases-standalone.html   # Редирект на /cases/
├── llms.txt                # RU llms.txt для AI-поисковиков
├── en/
│   ├── index.html          # EN главная
│   ├── cases/index.html    # EN кейсы
│   ├── cases-standalone.html  # Редирект на /en/cases/
│   └── llms.txt            # EN llms.txt
├── sitemap.xml             # Карта сайта (4 URL + xhtml:link alternates)
├── robots.txt              # Allow: /, Sitemap ссылка
├── CNAME                   # valeriyakrivko.com (для GitHub Pages)
├── og-banner.html          # Исходник OG-баннера 1200×630
├── CLAUDE.md               # Этот файл
├── .gitignore              # node_modules, временные скрипты
├── images/
│   ├── Lera.png            # Фото Лерчика (hero section)
│   ├── Preview.png         # OG-баннер 1200×630
│   └── ...                 # Скрины кейсов
└── video/                  # Видео (не подключено)
```

---

## Стек и дизайн

- **Тёмная тема:** `#0a0a0a` фон, `#f0f0e8` текст (`var(--fg)`), `#a8a9a3` приглушённый (`var(--fg-dim)`)
- **Шрифты:** Space Grotesk (заголовки) + Inter (текст) + JetBrains Mono (метки/моно)
- **Акцент:** `oklch(var(--g-lit) var(--g-sat) var(--g-hue))` — зелёный (hue 130)
- **Кастомный курсор** с магнетизмом (`[data-magnetic]`), активируется через `document.body.classList.add("cursor-on")`
- **Бургер-меню** для мобилки (`#burger` + `.nav-mobile`)

**Что удалено:**
- Preview bar (Desktop / Tablet / Mobile переключатель) — убран полностью
- Tweaks-панель (⚙ шестерёнка, настройка цвета) — убрана полностью

---

## SEO — что сделано

### Технический SEO
- `sitemap.xml` — index.html + cases-standalone.html с lastmod
- `robots.txt` — Allow: /, Sitemap: https://valeriyakrivko.com/sitemap.xml
- `CNAME` — кастомный домен valeriyakrivko.com
- Canonical URL — `<link rel="canonical" href="https://valeriyakrivko.com/">`
- `<link rel="preload" as="image" href="images/Lera.png">` — LCP оптимизация
- og:image = `images/Preview.png` (брендированный баннер 1200×630)

### On-page SEO
- Title, meta description (148 символов — в лимите)
- og:title, og:description, og:url, og:image, twitter:card
- JSON-LD: Person + ProfessionalService + FAQPage (11 вопросов, синхронизированы)
- Alt-тексты на всех изображениях кейсов (ключевые слова в alt)
- H1 на cases-standalone.html: "Кейсы — Tilda, GetCourse, чат-боты"
- Hero-теги с ключевыми запросами (между sub-title и CTA)
- FAQ секция — 11 вопросов (6 про ИИ-продавца, 3 про GetCourse/Tilda/гео, 2 про процесс)
- areaServed в JSON-LD: Казахстан, Россия, Великобритания, Таиланд, Кипр

### AI-поиск (llms.txt)
- Описание услуг с ценами
- Методология: 5 этапов ИИ-продавца, схема Tilda→n8n→GetCourse, этапы Tilda-сайта
- Ключевые кейсы с именами
- Триггеры когда упоминать Лерчика (для LLM-рекомендаций)
- Международная география клиентов

### cases-standalone.html
- Полный meta-блок (title, og:*, canonical, twitter:card)
- Текстовые разборы всех 5 кейсов: задача → решение → результат

---

## Контакты на сайте

- WhatsApp: `https://wa.me/+77775481717`
- Telegram: `https://t.me/valeriyavaly`
- Instagram: `https://www.instagram.com/valeriyavaly`
- Email: `mailto:krivko.valeriya@gmail.com`

---

## DNS-записи (Cloudflare)

Домен `valeriyakrivko.com` куплен на Cloudflare, DNS настроен на GitHub Pages:
```
A      @    185.199.108.153    DNS only (серое облачко)
A      @    185.199.109.153    DNS only
A      @    185.199.110.153    DNS only
A      @    185.199.111.153    DNS only
CNAME  www  krivkovaleriya-spec.github.io    DNS only
```

**⚠️ Важно про Proxy status:**
- DNS only (серое) — обязательно на этапе получения SSL от GitHub, иначе сертификат не выпустится
- После того как HTTPS заработает, можно включить оранжевое (Cloudflare прокси) → но тогда SSL/TLS в Cloudflare должен быть **Full** (не Flexible — будет редирект-петля)

**Старый домен `valeriyakrivko.kz`:** не оплачивается, отпущен (с 2026-09-29).

HTTPS: автоматически через GitHub Pages (Let's Encrypt), активируется после DNS propagation (~15-30 мин).

---

## Правила работы

- Контент только реальный — ничего не придумывать (цифры, отзывы, кейсы)
- GitHub Pages: нет серверного рендеринга, нет PHP, всё статика
- `!important` на `color` для `<a>` не нужен (это не Tilda)
- Мобилку менять прямо в HTML/CSS
- Все URL в файлах: `valeriyakrivko.com` (не valeriyavaly.github.io)
- **Правки текста — сразу в RU и EN версиях** (index.html + en/index.html, cases/index.html + en/cases/index.html)
- **hreflang теги** во всех `<head>` — не удалять
- **Цены в EN:** USD / EUR / GBP (курс ~475 KZT/USD)

---

## Деплой

```bash
cd "d:\Claude Code\lera-website"
git add -A
git commit -m "..."
git push origin main
```

GitHub Pages публикует через ~1–2 минуты.

---

## Статус

**Домен:** valeriyakrivko.com (переехали с .kz 2026-09-29)  
**Двуязычность:** RU + EN, переключатель в меню, hreflang готов  
**HTTPS:** автоматически (ждать до 30 мин после DNS)  
**SEO:** sitemap с 4 URL, llms.txt на двух языках, JSON-LD на обеих версиях

---

## Что сделано (сессия 2026-09-29)

### Переезд домена .kz → .com
- Куплен `valeriyakrivko.com` на Cloudflare
- Настроены 4 A-записи + CNAME www на GitHub Pages (все DNS only)
- Заменён CNAME файл в репо
- Домен `.kz` отпущен (не оплачивается)
- Все URL в файлах (index.html, cases/, llms.txt, sitemap.xml, robots.txt, JSON-LD) обновлены на `.com`

### Английская версия сайта
- Создана папка `/en/` с полной англ версией: главная, кейсы, cases-standalone (редирект), llms.txt
- Профессиональный деловой перевод всех текстов (не машинный)
- Переключатель `RU | EN` в шапке и мобильном меню на всех 4 страницах — активный язык подсвечен зелёным
- `hreflang` теги (ru, en, x-default) во всех `<head>` — Google поймёт языковые версии
- `sitemap.xml` расширен: 4 URL + `xhtml:link rel="alternate"` для каждой пары
- Цены EN: три колонки USD / EUR / GBP (курс ~475 KZT/USD)
- JSON-LD (Person, ProfessionalService, FAQPage) переведён на английский на EN-страницах
- Название "ВАЛЕРИЯ КРИВКО" в preloader на EN → "VALERIA KRIVKO"
- Google Analytics (G-V7M0K19Y06) на обеих версиях — один property

### Прочее
- Добавлен `.gitignore` (node_modules, временные fix-*.js скрипты)

---

## Что сделано (сессия 2026-06-10)

### em / заголовки
- `em` глобально `display:inline-block` — зелёный хайлайт не наезжает на соседние строки
- На мобилке `em { margin-top:2px }` в медиа-запросе `max-width:600px`
- **НЕ менять** `em` на `inline` + `box-decoration-break` — Safari не поддерживает корректно

### Кейсы — главная страница
- Анимированная SVG-рука на всех 9 кейсах (`.case-tap-hint-wrap`) — исчезает при hover
- Цвета руки: **салатовая** (`var(--green)`) — кейсы 1, 2, 8; **тёмно-зелёная** (`var(--green-deep)`) — кейсы 3,4,5,6,7,9
- Скорость скролла ноутбука: `transition: transform 48s` (было 12s)
- В GetCourse секции поменяны местами скриншоты "до" между карточками 1 и 2

### Кейсы — cases-standalone.html
- Аналогичная SVG-рука добавлена на все 5 кейсов

### Мобилка — общее
- FAQ: убран дефолтный треугольник `▶` через `-webkit-details-marker` и `list-style:none`
- `.svc-card-wide` на мобилке: `align-items:flex-start` — текст не центрируется
- Блок статистики (50+ проектов): `text-align:center` на мобилке
- Кнопки hero: `width:85%`, `padding:18px 20px`, по центру
- Hero title на мобилке: `font-size:30px`
- Таблица цен на мобилке: 3 колонки (`grid-template-columns:1fr 1fr 1fr`), все три цены в одну строку

### Секция "Личный кабинет, который продаёт"
- Класс `section-title--compact` — на мобилке `font-size:clamp(18px,5.5vw,96px)`
- `<em>` разбит на два слова: `<em>который</em> <em>продаёт</em>` — чтобы переносилось корректно

### Scroll reveal анимация
- Fade-up при скролле через `IntersectionObserver` — класс `.reveal` → `.reveal.visible`
- Анимируются: заголовки, карточки услуг/аудитории/почему, кейсы, отзывы, FAQ, цены, контакт
- `prefers-reduced-motion` — анимации отключены
- Задержки: `.reveal-delay-1/2/3` для карточек в ряду

### Preloader
- Счётчик 0→100% с ease-curve, ~1.8s
- Крупная цифра: `clamp(80px,18vw,200px)` десктоп, `120px` мобилка
- Надпись "ВАЛЕРИЯ КРИВКО" внизу, тонкая зелёная полоска на всю ширину
- Выход: fade out 0.8s
- `topbar` z-index поднят до `999999` — меню видно во время preloader
- `prefers-reduced-motion` — preloader скрыт

---

## Правила — важные уроки

- **Десктоп не трогать** когда просят мобилку — все правки только в `@media (max-width:600px)`
- **`<br>` в hero-title** ломает десктоп — использовать только для мобилки через медиа-запрос или не использовать совсем
- **`em` внутри заголовков** — не менять на `inline`, только `inline-block`
- **price-row грид** на десктопе `1.6fr 2fr 1fr 1fr 1fr` — не ломать враппером

---

## TODO

- [ ] Проверить статистику посещений: https://analytics.google.com/analytics/web/provision/#/provision/create
  - Google Analytics подключён: G-V7M0K19Y06

---

## Что ещё можно сделать (низкий приоритет)

- Внешние упоминания: FL.ru, Kwork, Profi.ru, VC.ru, Habr — для ссылочного профиля и AI-индексации
- Кейсы: добавить реальные метрики (цифры)
- Отзывы: добавить реальные имена и ниши
- Preloader: slot-machine анимация цифр (обсуждалось, не сделано)
