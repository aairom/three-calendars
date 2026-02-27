# 🗓 Three Calendar System

A self-contained, single-file HTML application that displays three calendar systems side by side — **Gregorian**, **Persian (Jalali)**, and **Hijri (Islamic)** — all synchronized to the same selected date via Julian Day Number (JDN) as a universal pivot.

---

## ✨ Features

| Feature | Description |
|---|---|
| **Three calendars** | Gregorian, Persian/Jalali, and Hijri/Islamic displayed simultaneously |
| **Synchronized selection** | Clicking any date in any calendar highlights the equivalent date in all three |
| **Month navigation** | `‹` / `›` buttons to move backward/forward one month per calendar independently |
| **Go to date** | Input fields (year, month dropdown, day) on each card to jump to a specific date |
| **Today button** | Instantly resets all three calendars to today's date |
| **Leap year badge** | A colored badge appears next to the month name when the displayed year is a leap year |
| **Weekend highlighting** | Weekends are visually distinguished per calendar's convention |
| **RTL layout** | Persian and Hijri grids render right-to-left as per their cultural convention |
| **Responsive design** | Cards stack vertically on screens narrower than 820 px |
| **Zero dependencies** | Pure HTML + CSS + JavaScript — no libraries, no build step |

---

## 📅 Calendar Systems

### Gregorian
- Standard international calendar (ISO 8601 basis).
- Week starts **Sunday**.
- Weekends: **Saturday** and **Sunday** (highlighted in red).
- Leap year: divisible by 4, except centuries unless also divisible by 400.
- Color accent: **blue** (`#4fc3f7`).

### Persian / Jalali (Solar Hijri)
- Official calendar of Iran and Afghanistan.
- Week starts **Saturday** (`Sha, Yek, Do, Se, Cha, Pan, Jom`).
- Weekend: **Friday** only (highlighted in red).
- Grid direction: **right-to-left**.
- Months 1–6 have 31 days, months 7–11 have 30 days, month 12 has 29 (or 30 in a leap year).
- Leap year algorithm: jalaali-js cycle-based calculation.
- Color accent: **green** (`#81c784`).

### Hijri / Islamic (Tabular)
- Lunar calendar used across the Islamic world.
- Week starts **Sunday** (same as Gregorian).
- Weekends: **Friday** and **Saturday** (highlighted in red).
- Grid direction: **right-to-left**.
- Month lengths alternate 30/29 days; the 12th month gains a day in leap years.
- Leap year rule: positions 3, 6, 8, 11, 14, 17, 19, 22, 25, 27, 30 in a 30-year cycle (`floor((11y+3)/30)`).
- Year displayed with the **AH** (Anno Hegirae) suffix.
- Color accent: **amber** (`#ffb74d`).

---

## 🔧 How It Works

### Core Conversion Engine

All three calendars are bridged through the **Julian Day Number (JDN)** — a continuous integer count of days since noon on 1 January 4713 BC (Julian calendar). Every date in any system is first converted to a JDN, and from that JDN any other calendar date can be derived.

| Function | Direction |
|---|---|
| [`g2d(gy, gm, gd)`](three-calendars.html:338) | Gregorian → JDN |
| [`d2g(jdn)`](three-calendars.html:344) | JDN → Gregorian |
| [`j2d(jy, jm, jd)`](three-calendars.html:388) | Persian → JDN |
| [`d2j(jdn)`](three-calendars.html:392) | JDN → Persian |
| [`i2d(iy, im, id)`](three-calendars.html:417) | Hijri → JDN |
| [`d2i(jdn)`](three-calendars.html:420) | JDN → Hijri |

### State Management

| Variable | Purpose |
|---|---|
| [`currentJDN`](three-calendars.html:460) | The currently selected day (JDN integer) |
| [`todayJDN`](three-calendars.html:464) | Today's JDN, computed once at startup |
| [`viewGreg`](three-calendars.html:461) | `{y, m}` — the month currently displayed in the Gregorian card |
| [`viewPers`](three-calendars.html:462) | `{jy, jm}` — the month currently displayed in the Persian card |
| [`viewHijri`](three-calendars.html:463) | `{iy, im}` — the month currently displayed in the Hijri card |

### Key Functions

| Function | Description |
|---|---|
| [`init()`](three-calendars.html:469) | Bootstraps the app: computes today's JDN, syncs views, populates dropdowns, renders |
| [`syncViewFromJDN(jdn)`](three-calendars.html:479) | Updates all three view states to the month containing the given JDN |
| [`navigate(cal, delta)`](three-calendars.html:491) | Moves a single calendar's view ±1 month |
| [`selectDay(jdn)`](three-calendars.html:716) | Sets `currentJDN`, syncs all views, re-renders |
| [`goToDate(cal)`](three-calendars.html:511) | Reads the input fields for a calendar, validates the date, and navigates to it |
| [`goToToday()`](three-calendars.html:543) | Resets `currentJDN` to `todayJDN` and re-renders |
| [`renderAll()`](three-calendars.html:570) | Calls all three render functions and updates input fields |
| [`updateInputFields()`](three-calendars.html:725) | Reflects `currentJDN` back into all six input fields |

---

## 🚀 Usage

No installation or build step required.

1. Open [`three-calendars.html`](three-calendars.html) directly in any modern browser.
2. The page loads showing today's date highlighted across all three calendars.

### Navigating

- Click **`‹`** or **`›`** on any calendar header to move that calendar's view one month backward or forward.
- Click any **day cell** to select that date — all three calendars will synchronize to the equivalent date.
- Click **Today** to jump back to the current date.

### Jumping to a Specific Date

1. Fill in the **Year**, **Month** (dropdown), and **Day** fields at the bottom of any calendar card.
2. Click **Go**.
3. All three calendars will navigate to the equivalent date.

---

## 🎨 Design

- **Dark glassmorphism** theme: semi-transparent cards with `backdrop-filter: blur` over a deep navy gradient background.
- Each calendar has a unique **color accent** (blue / green / amber) applied to the title, today highlight, leap badge, and Go button hover state.
- **Responsive**: at ≤ 820 px viewport width the three cards stack into a single column.

---

## 🌐 Browser Compatibility

Works in all modern browsers that support:
- CSS `backdrop-filter`
- ES5+ JavaScript (no ES6 modules or async/await used)

| Browser | Support |
|---|---|
| Chrome / Edge 76+ | ✅ Full |
| Firefox 103+ | ✅ Full |
| Safari 9+ | ✅ Full |
| Mobile browsers | ✅ Responsive layout |

---

## 📁 File Structure

```
three-calendars.html   ← entire application (HTML + CSS + JS, ~748 lines)
README.md              ← this file
```

---

## 📜 License

This project is provided as-is for personal and educational use. No external libraries or assets are used.