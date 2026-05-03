# BDS Pipeline — Birdeye Data Sprint 3

**Multi-source crypto data pipeline with automated cleaning, validation, enrichment & export.**

Built for the Birdeye Data BIP Sprint 3 competition. 500 USDC bounty.

---

## 🏗️ Architecture

```
┌──────────────┐    ┌──────────────┐
│  CoinGecko   │    │  Birdeye BDS │
│  (Public)    │    │  (API Key)   │
└──────┬───────┘    └──────┬───────┘
       │                   │
       └────────┬──────────┘
                ▼
    ┌───────────────────────┐
    │   FETCH & NORMALIZE   │
    │   → Unified Schema    │
    └───────────┬───────────┘
                ▼
    ┌───────────────────────┐
    │   DATA TOOLKIT CLEAN  │
    │   • Deduplicate       │
    │   • Null handling     │
    │   • Number normalize  │
    │   • String normalize  │
    └───────────┬───────────┘
                ▼
    ┌───────────────────────┐
    │   ENRICH               │
    │   • Volatility flags   │
    │   • MCap tiers         │
    │   • Volume/MCap ratio  │
    └───────────┬───────────┘
                ▼
    ┌───────────────────────┐
    │   VALIDATE             │
    │   • Custom rules       │
    │   • Quality checks     │
    └───────────┬───────────┘
                ▼
    ┌───────────────────────┐
    │   EXPORT               │
    │   • JSON (full)        │
    │   • CSV (spreadsheet)  │
    │   • Summary (report)   │
    └───────────────────────┘
```

---

## 🚀 Quick Start

```bash
# Install
pip install -r requirements.txt

# Run with CoinGecko (free, no API key)
python bds_pipeline.py

# Run with Birdeye BDS (needs API key)
export BIRDEYE_API_KEY=your-key
python bds_pipeline.py --birdeye
```

---

## 📊 What It Produces

### 1. Clean Token Dataset
- 100 tokens, deduplicated, nulls handled
- Unified schema across all sources
- Ready for dashboards, analysis, trading

### 2. Enriched Metrics
- `volatility_flag`: HIGH/MEDIUM/LOW based on 24h change
- `mcap_tier`: LARGE/MID/SMALL/MICRO cap classification
- `volume_mcap_ratio`: Liquidity proxy

### 3. Export Formats
- `tokens_YYYYMMDD-HHMMSS.json` — Full data
- `tokens_YYYYMMDD-HHMMSS.csv` — Spreadsheet ready
- `summary_YYYYMMDD-HHMMSS.json` — Executive report

---

## 🔌 Birdeye BDS Integration

Drop-in replacement when `BIRDEYE_API_KEY` is set:

```python
# Automatic: pipeline detects API key and switches source
python bds_pipeline.py --birdeye

# Or programmatically:
pipeline = CryptoDataPipeline()
pipeline.run(use_birdeye=True)
```

Adapter for any BDS endpoint by extending `fetch_birdeye_*()` functions.

---

## 📈 Sprint 3 Deliverables

| Requirement | Status |
|------------|--------|
| Multi-source data pipeline | ✅ CoinGecko + Birdeye (configurable) |
| Data cleaning & normalization | ✅ Data Toolkit integrated |
| Validation & quality checks | ✅ Custom rules engine |
| Export to multiple formats | ✅ JSON + CSV + Summary |
| Production ready | ✅ Error handling, logging, CLI |

---

**Built for Birdeye Data BIP Sprint 3 by Atlas Nexus**
