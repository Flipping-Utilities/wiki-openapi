# wiki-openapi

OpenAPI 3.0 specification for the **RuneScape Wiki Real-time Grand Exchange Prices API** (OSRS),
published by the OSRS Wiki in partnership with RuneLite.

- **Spec:** [`openapi.yaml`](./openapi.yaml)
- **Live docs / playground:** https://flipping-utilities.github.io/wiki-openapi/
- **Upstream wiki docs:** https://oldschool.runescape.wiki/w/RuneScape:Real-time_Prices

The docs site is rendered with [**Scalar**](https://github.com/scalar/scalar), an open-source API
reference viewer with a built-in interactive client (the "playground"). Requests sent from the
playground are routed through Scalar's public CORS proxy (`https://proxy.scalar.com`) so that
`prices.runescape.wiki` can be called directly from the browser.

## Endpoints covered

| Method | Path           | Description                                             |
| ------ | -------------- | ------------------------------------------------------- |
| GET    | `/latest`      | Latest high/low prices for all items (or a single one). |
| GET    | `/mapping`     | Static item metadata (name, id, examine, alch, limits). |
| GET    | `/5m`          | 5-minute average prices and traded volumes.             |
| GET    | `/1h`          | 1-hour average prices and traded volumes.               |
| GET    | `/6h`          | 6-hour average prices and traded volumes.               |
| GET    | `/24h`         | 24-hour average prices and traded volumes.              |
| GET    | `/timeseries`  | Historical high/low series for a single item.           |

Base URL: `https://prices.runescape.wiki/api/v2/osrs`

## Using the spec

Point any OpenAPI-compatible tool at the published spec URL:

```
https://flipping-utilities.github.io/wiki-openapi/openapi.yaml
```

```bash
# Example: fetch the latest price for the Abyssal whip (id=4151)
curl -H "User-Agent: my-tool - me@example.com" \
  "https://prices.runescape.wiki/api/v2/osrs/latest?id=4151"
```

> ⚠️ **Set a descriptive `User-Agent` header.** Default user-agents
> (`python-requests`, `curl/8.x`, `Java/17`, `RestSharp`, …) are blocked. See the
> [Acceptable use policy](https://oldschool.runescape.wiki/w/RuneScape:Real-time_Prices#Acceptable_use_policy)
> on the wiki.

## Local preview

Because Scalar fetches the spec via HTTP, open the site through any static file server rather than
`file://`:

```bash
# Python
python -m http.server 8000

# Node
npx serve
```

Then visit http://localhost:8000/.

## Regenerating / validating

```bash
npx @redocly/cli lint openapi.yaml
npx @redocly/cli bundle openapi.yaml --output openapi.bundle.yaml
```

## Repository layout

```
.
├── openapi.yaml    # The OpenAPI 3.0.3 document
├── index.html      # Scalar API Reference shell (loads openapi.yaml)
├── .nojekyll       # Disables Jekyll so GitHub Pages serves the raw yaml
└── README.md
```

## License

MIT. The underlying price data is provided by the
[OSRS Wiki](https://oldschool.runescape.wiki/w/RuneScape:Real-time_Prices) — please respect their
acceptable use policy.
