# 📈 Forex EMA Strategy with Dashed Stops & Live Table

![PineScript](https://img.shields.io/badge/PineScript-v6-yellowgreen) ![TradingView](https://img.shields.io/badge/Platform-TradingView-blue) ![License](https://img.shields.io/badge/License-MIT-red)

A dynamic Forex trading strategy combining EMA crossovers with adaptive ATR-based stops and real-time visual feedback.

## 🌟 Features
- **📊 Dual EMA System**: 
  - `Fast EMA (10)` and `Slow EMA (50)` crossovers for signals
  - `200 EMA` trend filter
- **🛡 Adaptive Risk Management**:
  - ATR-based stops with day/night multipliers (⚡2.0x / 🌙1.5x)
  - Dashed stop-loss lines (green for longs, red for shorts)
- **⏰ Session Control**:
  - Morning (07:00-11:00 CT) 
  - Evening (19:00-02:00 CT) sessions
- **📊 Live Dashboard**:
  - Real-time session status
  - Position tracking (LONG/SHORT/FLAT)
  - Dynamic stop price display

## ⚙️ Input Parameters
| Parameter | Description | Default |
|-----------|-------------|---------|
| `Fast EMA` | Short-term EMA length | 10 |
| `Slow EMA` | Long-term EMA length | 50 |
| `Trend Filter EMA` | Trend direction filter | 200 |
| `ATR Length` | Volatility measurement period | 14 |
| `Morning Session` | Primary trading window | 0700-1100 CT |
| `Evening Session` | Secondary trading window | 1900-0200 CT |

## 📜 Strategy Logic

### Entry Conditions
- **▲ LONG**:
  ```.javascript
  bullish = ta.crossover(emaShort, emaLong) and close > emaTrendFilter
  inSession = not na(time(timeframe.period, morningSession)) or 
             (not na(time(timeframe.period, eveningSession)) and tradeEvening)

- **▲ SHORT**:
 ```.javascript
bearish = ta.crossunder(emaShort, emaLong) and close < emaTrendFilter
inSession = not na(time(timeframe.period, morningSession)) or 
           (not na(time(timeframe.period, eveningSession)) and tradeEvening)
```
### Exit Management
- **ATR Stop Calculation**:
```.javascript
  currentMultiplier = not na(time(timeframe.period, morningSession)) ? dayMultiplier : nightMultiplier
  longStop = low - (atrValue * currentMultiplier)
  shortStop = high + (atrValue * currentMultiplier)
```
## 🎨 Visual Features
| Element | Description | Color |
|---------|-------------|-------|
| Fast EMA | Short-term trend | `#2962FF` (Blue) |
| Slow EMA | Long-term trend | `#FF6D00` (Orange) |
| Trend Filter | Market bias | `#8E24AA` (Purple) |
| Long Stop | Dynamic protection | `#00BFA5` (Teal) |
| Short Stop | Risk management | `#D50000` (Red) |

**Live Table Features**:
- Session status (Morning/Evening/Closed)
- Current position with colored indicators
- Active stop price display

## 🚀 Installation
1. Open TradingView
2. Create new Pine Script strategy
3. Paste entire code
4. Adjust parameters in "Inputs" tab

## 💡 Customization Ideas
- Adjust EMA lengths for different timeframes
- Modify session times for specific markets
- Experiment with ATR multipliers (1.0-3.0 range)

**⚠️ Important**: Always backtest strategies with historical data before live trading. This is educational material - not financial advice.

    
