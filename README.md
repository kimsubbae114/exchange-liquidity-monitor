# exchange-liquidity-monitor

> **한국어 요약** — 10개 거래소(CEX 5 · Perp DEX 5)의 **호가창을 실제로 받아** 시장가 주문을 시뮬레이션하고,
> 주문 규모별 슬리피지로 순위를 매깁니다. GitHub Actions 로 매시간 돌고 결과는 정적 사이트로 나옵니다.
> 자세한 한국어 설명은 `README.ko.md`.

Measures **real order-book liquidity** across ten venues — five centralized exchanges and five perpetual DEXes —
by pulling live order books, simulating market orders of several sizes, and ranking venues by slippage.

- Venues: binance · bybit · okx · mexc · kucoin · grvt · hyperliquid · aster · lighter · extended
- Runs hourly on GitHub Actions, keeps a history, and publishes a static report (`public/`)
- Fees are excluded from the ranking by default (they change with tiers and promotions); depth and slippage are what is measured

## Usage

```bash
pip install -r requirements.txt
python collect.py        # pull order books once → data/
python agg.py            # aggregate
python build_report.py   # → public/index.html
```

See `.github/workflows/` for the hourly schedule and deploy step.

## Notes

- Some venues cap order-book depth per request; the collector asks for the deepest level each API allows.
- Symbols differ per venue (RWA tickers especially); the mapping lives in `collect.py`.

## License

MIT — see `LICENSE`.

## Deployment setup

Set repository variables CLOUDFLARE_PAGES_PROJECT and SITE_URL for your own deployment, plus CLOUDFLARE_API_TOKEN and CLOUDFLARE_ACCOUNT_ID secrets.

## Author

https://x.com/kimsubbae114
