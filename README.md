# Finance Wise

Turn a Wise CSV export into one readable page of your spending. The whole app is a
single `index.html`: no backend, no build step, no dependencies — and your data never
leaves the browser.

**[Open it →](https://hsiaoliang.github.io/Finance_Wise/)**

## Features

- **Overview** — account balance, key figures, spending trend, category share, recent transactions
- **Analysis** — merchant ranking, weekday rhythm, cumulative spend, recurring charges, outlier detection
- **Money flow** — top-ups, internal transfers, refunds and real income kept apart, with a balance trend
- **Budgets** — a monthly budget per category and currency, with a month-end projection at your current pace
- **Transactions** — search, date filtering, per-charge detail, and your own category and tag rules
- **English / 中文** — switch any time from the toolbar; dates and numbers follow the language
- Light and dark themes, and a CSV export of whatever you have filtered

## Usage

### Online

Open the [GitHub Pages site](https://hsiaoliang.github.io/Finance_Wise/) and either choose
a file or drag your Wise CSV onto the page. It is parsed locally in the browser and
uploaded nowhere.

### Locally (reads the CSV from the folder for you)

```bash
git clone https://github.com/HsiaoLiang/Finance_Wise.git
cd Finance_Wise
python3 -m http.server 8777
```

Then open http://localhost:8777.

Save your export as `Sources/Wise Transaction History.csv` and the page reads it on load;
"Re-read" picks up the latest content without touching the filters.

## Getting your Wise CSV

Wise → Balances → Statement → pick a currency and a date range → download **CSV**.

Both Wise export shapes work: the transaction history and the account statement. Several
files can be imported at once, and duplicates are dropped.

## Language

The `EN` / `中` button in the toolbar switches the interface. The first visit follows your
browser (`zh-*` gets Chinese, everything else English); after that the choice is remembered
in the settings file.

Transaction categories keep the English names Wise gives them (Groceries, Eating out, …):
the Chinese interface translates them, the English one shows them as they come. Categories
and tags you create yourself are left untouched in both.

## Settings file

Rules, budgets and preferences live in `finance-wise-settings.json`, next to `index.html`.
Start from the template:

```bash
cp finance-wise-settings.example.json finance-wise-settings.json
```

In Chrome and Edge, "Link settings file" in the settings panel writes back to that file
directly. Other browsers use "Download a copy" and overwrite it yourself.

## Privacy

`Sources/*.csv` and `finance-wise-settings.json` are in `.gitignore`, so they are never
committed. This repository contains no real transaction data.

## How it works

`index.html` holds everything: styles, a CSV parser, the charts (hand-written SVG, no
chart library) and the rendering. The pipeline is parse → normalise → filter → aggregate →
draw, and nothing in it talks to the network.

Source strings are English and double as the keys of the `ZH` dictionary, so a missing
translation falls back to English rather than breaking. Static markup is collected once at
boot and swapped on a language switch; everything built in JS goes through `t()`.

## License

[MIT](LICENSE).

## Not affiliated with Wise

A personal tool for reading Wise CSV exports. Not an official Wise product.
