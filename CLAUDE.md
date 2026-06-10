# CLAUDE.md — Личный сайт Валерии Кривко

**URL:** https://valeriyakrivko.kz/  
**GitHub Pages репо:** krivkovaleriya-spec/krivkovaleriya-spec.github.io (или аналог)  
**Платформа:** GitHub Pages (не Tilda — нет ограничений платформы)  
**Кастомный домен:** valeriyakrivko.kz (CNAME файл в репо)

---

## Структура проекта

```
lera-website/
├── index.html              # Весь сайт — один файл
├── cases-standalone.html   # Отдельная страница кейсов
├── llms.txt                # Для AI-поисковиков (ChatGPT, Perplexity, Claude)
├── sitemap.xml             # Карта сайта для Googlebot
├── robots.txt              # Allow: /, Sitemap ссылка
├── CNAME                   # valeriyakrivko.kz (для GitHub Pages)
├── og-banner.html          # Исходник OG-баннера 1200×630 (HTML → скриншот)
├── CLAUDE.md               # Этот файл
├── images/
│   ├── Lera.png            # Фото Лерчика (hero section)
│   ├── Preview.png         # Брендированный OG-баннер (скриншот og-banner.html)
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
- `robots.txt` — Allow: /, Sitemap: https://valeriyakrivko.kz/sitemap.xml
- `CNAME` — кастомный домен valeriyakrivko.kz
- Canonical URL — `<link rel="canonical" href="https://valeriyakrivko.kz/">`
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

## DNS-записи (у регистратора домена)

DNS настроен на GitHub Pages:
```
A  @  185.199.108.153
A  @  185.199.109.153
A  @  185.199.110.153
A  @  185.199.111.153
CNAME  www  krivkovaleriya-spec.github.io
```

Остальные записи (mail, online→getcourse, TXT, MX, n8n) — не трогать, нужны для почты и других сервисов.

HTTPS: автоматически через GitHub Pages (Let's Encrypt), активируется после DNS propagation.

---

## Правила работы

- Контент только реальный — ничего не придумывать (цифры, отзывы, кейсы)
- GitHub Pages: нет серверного рендеринга, нет PHP, всё статика
- `!important` на `color` для `<a>` не нужен (это не Tilda)
- Мобилку менять прямо в HTML/CSS
- Все URL в файлах: `valeriyakrivko.kz` (не valeriyavaly.github.io)

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

**Задеплоено:** да, сайт открывается на valeriyakrivko.kz  
**HTTPS:** автоматически (ждать до 30 мин после DNS)  
**Все SEO улучшения:** применены

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

## Что ещё можно сделать (низкий приоритет)

- Внешние упоминания: FL.ru, Kwork, Profi.ru, VC.ru, Habr — для ссылочного профиля и AI-индексации
- Кейсы: добавить реальные метрики (цифры)
- Отзывы: добавить реальные имена и ниши
- Preloader: slot-machine анимация цифр (обсуждалось, не сделано)
