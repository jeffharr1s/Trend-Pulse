# 📊 TrendPulse

**Social Sentiment Trading Signals Platform**

TrendPulse monitors social media, messaging platforms, and on-chain data to detect emerging trends before they go mainstream, helping you make informed trading decisions.

![TrendPulse Dashboard](docs/dashboard-preview.png)

## ✨ Features

### 📡 Multi-Source Data Collection
- **Social Platforms**: Reddit, X/Twitter, StockTwits, TikTok, YouTube
- **Private Messaging**: Telegram, Discord, WhatsApp
- **On-Chain Analytics**: LunarCrush, Santiment, Glassnode, DEXTools
- **Prediction Markets**: Polymarket, Kalshi
- **News Aggregation**: CryptoPanic, NewsAPI, Google Trends

### 🎯 Signal Generation
- Momentum scoring (0-100) based on multi-factor analysis
- Sentiment analysis with NLP
- Cross-platform trend detection
- Buy/Sell/Watch signal generation with confidence scores

### 🔔 Real-Time Alerts
- Volume surge detection
- Sentiment flip notifications
- Momentum breakout alerts
- Cross-platform spread detection

### 💹 Trading Integration
- **Stocks**: Alpaca, Interactive Brokers
- **Crypto**: Coinbase, Binance, Kraken

## 🚀 Quick Start

### Prerequisites
- Python 3.11+
- Node.js 18+ (for frontend)
- Redis (optional, for caching)

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/trend-pulse.git
cd trend-pulse
```

2. **Set up Python environment**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```

3. **Configure environment**
```bash
cp .env.example .env
# Edit .env with your API credentials
```

4. **Run the backend**
```bash
cd backend
python app.py
```

5. **Access the dashboard**
- API: http://localhost:8000
- API Docs: http://localhost:8000/docs
- Frontend: Open `frontend/trend-pulse-v2.jsx` in your React app

## 📁 Project Structure

```
trend-pulse/
├── backend/
│   ├── app.py                 # FastAPI application
│   ├── config.py              # Configuration settings
│   ├── models.py              # Pydantic models
│   ├── data_sources/
│   │   └── __init__.py        # Data source integrations
│   └── services/
│       ├── __init__.py
│       ├── aggregator.py      # Sentiment aggregation
│       ├── signal_generator.py # Signal generation
│       └── alert_manager.py   # Alert management
├── frontend/
│   └── trend-pulse-v2.jsx     # React dashboard
├── config/
│   └── tickers.json           # Ticker metadata
├── scripts/
│   └── setup_telegram.py      # Telegram auth helper
├── docs/
│   └── API.md                 # API documentation
├── requirements.txt
├── .env.example
├── docker-compose.yml
└── README.md
```

## 🔧 Configuration

### Data Sources

Each data source requires specific API credentials. Here's how to get them:

| Source | Documentation | Tier |
|--------|--------------|------|
| Reddit | [reddit.com/prefs/apps](https://www.reddit.com/prefs/apps) | Essential |
| Telegram | [my.telegram.org/apps](https://my.telegram.org/apps) | Essential |
| Discord | [discord.com/developers](https://discord.com/developers/applications) | Essential |
| LunarCrush | [lunarcrush.com/developers](https://lunarcrush.com/developers) | Essential |
| Twitter/X | [developer.twitter.com](https://developer.twitter.com) | Recommended |
| Santiment | [api.santiment.net](https://api.santiment.net) | Recommended |
| Alpaca | [alpaca.markets](https://alpaca.markets) | For Trading |

### Alert Thresholds

Customize alert sensitivity in `.env`:

```env
ALERT_MOMENTUM_THRESHOLD=70.0    # Trigger alerts above this momentum
ALERT_SENTIMENT_THRESHOLD=0.3   # Sentiment flip threshold
ALERT_VOLUME_SPIKE_THRESHOLD=200.0  # % increase to trigger surge alert
```

## 📡 API Reference

### REST Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/trends` | Get all current trends |
| GET | `/api/trends/{ticker}` | Get trend detail with history |
| GET | `/api/alerts` | Get recent alerts |
| POST | `/api/alerts/{id}/dismiss` | Dismiss an alert |
| GET | `/api/sources` | Get data source status |
| POST | `/api/sources/{id}/configure` | Configure a data source |
| POST | `/api/sources/{id}/test` | Test data source connection |

### WebSocket

Connect to `ws://localhost:8000/ws` for real-time updates:

```javascript
const ws = new WebSocket('ws://localhost:8000/ws');

ws.onmessage = (event) => {
  const data = JSON.parse(event.data);
  
  if (data.type === 'update') {
    // Handle trend updates
    console.log('Trends:', data.data.trends);
  } else if (data.type === 'alert') {
    // Handle new alert
    console.log('New Alert:', data.data);
  }
};
```

## 🐳 Docker Deployment

```bash
docker-compose up -d
```

This starts:
- TrendPulse API (port 8000)
- Redis cache (port 6379)
- PostgreSQL database (port 5432)

## 📊 Signal Logic

### Momentum Score (0-100)

Calculated from:
- **Volume Score** (40%): Log-scaled mention count
- **Sentiment Score** (25%): Absolute sentiment strength
- **Platform Score** (20%): Number of platforms discussing
- **Acceleration Score** (15%): Rate of change vs history

### Signal Generation

| Signal | Conditions |
|--------|------------|
| **BUY** | Momentum > 70, Sentiment > 0.3, Velocity > 60 |
| **SELL** | Momentum < 30 OR Sentiment < -0.3 |
| **WATCH** | Momentum > 50, Sentiment > 0.1 |
| **HOLD** | Default state |

## ⚠️ Disclaimer

TrendPulse is for informational purposes only. It is not financial advice. Trading stocks and cryptocurrencies involves substantial risk of loss. Always do your own research and consult with a qualified financial advisor before making investment decisions.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

MIT License - see [LICENSE](LICENSE) for details.

## 🙏 Acknowledgments

- [LunarCrush](https://lunarcrush.com) for social sentiment data
- [Santiment](https://santiment.net) for on-chain analytics
- [Alpaca](https://alpaca.markets) for commission-free trading API

---

**Built with ❤️ for traders who want to stay ahead of the curve**
