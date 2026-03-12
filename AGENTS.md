# csvchop

csvchop is a browser-side CSV inspector and JSON converter — paste any CSV, see it as a formatted table, and download the result as JSON.

## What it does

- Auto-detects CSV delimiter (comma, tab, semicolon, pipe)
- Renders CSV as a scrollable table with sticky headers
- Converts CSV to JSON in two formats:
  - **Array of objects** (each row → `{ header: value, ... }`) — default, most useful for APIs
  - **Array of arrays** (raw rows including header row)
- Download result as `.json` file
- Nothing is uploaded — all processing happens in the browser

## Input / Output

**Input:** Raw CSV text (comma, tab, semicolon, or pipe separated)

**Output:** JSON array (array of objects or array of arrays)

## How an agent can use it

csvchop is currently a browser-only tool. There is no server-side API.

An agent that needs to convert CSV to JSON can replicate the same parsing logic using PapaParse (JavaScript) or any standard CSV library:

```javascript
// JavaScript equivalent
const Papa = require('papaparse');
const result = Papa.parse(csvString, { skipEmptyLines: true, dynamicTyping: false });
const headers = result.data[0];
const rows = result.data.slice(1);
const json = rows.map(row => Object.fromEntries(headers.map((h, i) => [h, row[i] ?? ''])));
```

```python
# Python equivalent
import csv, json, io
reader = csv.DictReader(io.StringIO(csv_string))
json_out = json.dumps(list(reader), indent=2)
```

## Planned API (future)

A future version will expose an HTTP endpoint at `https://csvchop.radicchio.page/api/parse`:

```
POST /api/parse
Content-Type: text/plain

name,age,city
Alice,30,New York

→ 200 OK
Content-Type: application/json

[{"name":"Alice","age":"30","city":"New York"}]
```

Query params: `?mode=objects` (default) or `?mode=arrays`, `?delimiter=,` (or `tab`, `semicolon`, `pipe`)

## Pricing

Free. No account required. No rate limits.

## Support

https://bitterdesk.com
