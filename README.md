# Gap & Go Trading Algorithm

**Note: This project is private. Please refrain from sharing the code or any sensitive information about the project.**

This project implements a **Gap & Go trading algorithm** leveraging the Interactive Brokers API to detect, validate, and trade stock opportunities based on gap, volume, and volatility conditions. Once a stock meets all criteria, the bot places a buy order with dynamically managed trailing stop losses for controlled exit points. This strategy is designed to capture significant gains by identifying high-momentum stocks and managing risk with progressive stop-loss adjustments.

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Key Conditions and Strategy](#key-conditions-and-strategy)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Limitations](#limitations)
- [License](#license)
- [Disclaimer](#disclaimer)

## Overview

The Gap & Go Trading Algorithm is designed to identify high-potential stocks through gap analysis, volume, and volatility conditions. The bot aims to maximize profits and minimize downside risk by leveraging a dynamic trailing stop-loss strategy. The algorithm operates within a defined time frame and automatically qualifies each stock to ensure it meets predefined conditions before trading.

## Features

Gap Detection: This method identifies stocks with an opening price gap within a specified range, indicating potential for high intraday momentum.
**Volume and Volatility Analysis**confirms that the stock has both high relative trading volume and implied volatility, increasing the likelihood of a sustained price movement.
- **Trailing Stop-Loss Management**: Sets progressively tightening server-managed trailing stops to protect gains.
- **Automated Buy Orders**: Places buy orders on qualifying stocks without requiring user intervention.
- **Time-Controlled Execution**: Runs within specific trading hours, configurable for optimal market conditions.

## Key Conditions and Strategy

The Gap & Go strategy is highly effective for capturing intraday or short-term price movements on high-momentum stocks. This section details the conditions used by the algorithm and explains how they contribute to identifying strong trade opportunities.

### 1. Gap Detection

Gap analysis identifies stocks whose **opening price is 7%-10% higher or lower than the previous day’s close**. This gap can signal a significant overnight shift in sentiment, often driven by news, earnings, or market events. By targeting stocks with a substantial opening gap, the algorithm aims to capitalize on the potential for a strong follow-through during regular market hours.

### 2. Relative Volume

Relative volume is a measure of current trading volume relative to an average (usually 90 days). A **high relative volume** (typically >1.5 times the average) suggests heightened interest and liquidity, which is crucial for the following reasons:
   - **Liquidity**: Increased volume supports smoother order execution and reduced slippage.
   - **Momentum Indicator**: High volume often confirms strong buying or selling pressure, indicating a higher likelihood that the price movement will continue.
   
By filtering for high relative volume, the algorithm ensures it focuses on stocks with increased activity, reducing the chances of false breakouts.

### 3. Implied Volatility

Implied volatility (IV) reflects the market’s forecast of a stock’s potential movement. A **high implied volatility rank** (typically above 0.5 in this algorithm) suggests that the stock is likely to experience significant price movement, either up or down. The benefits of this condition are:
   - **Movement Probability**: High IV implies the market expects volatility, increasing the chance of capturing substantial price changes.
   - **Risk Assessment**: By focusing on high IV stocks, the algorithm aims to capture higher reward-to-risk opportunities, as the market consensus is that movement is imminent.

Together, these conditions help the algorithm zero in on stocks with a higher probability of volatile, liquid, and momentum-driven moves that can be capitalized on with a gap-and-go strategy.

### 4. Trailing Stop Loss with Breakout Levels

Once a stock is bought, the algorithm applies an **initial trailing stop-loss** (typically set to 0.5% below the entry price) to manage downside risk. As the stock price moves up, the trailing stop is adjusted based on preset **breakout levels**:
- **Breakout Levels**: ********
- **Tightened Trailing Stops**: ********

At each breakout level, the trailing stop tightens, effectively locking in more gains while allowing for upward price movement. This progressive stop management allows the algorithm to capture extended trends while protecting profits at predefined intervals.

## Prerequisites

- **Python 3.8+**
- **Interactive Brokers Account** with API access enabled.
- **Interactive Brokers TWS or Gateway**: Must be running to allow data access and order execution.
- **Required Python Packages**: `ib_insync`, `logging`

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/gap-and-go-trading-algorithm.git
   cd gap-and-go-trading-algorithm
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Configuration

### IB Gateway/TWS Connection
Update the `self.ib.connect` settings in the `TradingAlgorithm` class to reflect your **host** (default: `127.0.0.1`) and **port** (default: `7497` for TWS or `4001` for IB Gateway).

### Trailing Stop Settings
Configure `breakout_levels`, `tightened_stops`, and `initial_stop_percent` in `place_buy_stock_order_gap_and_go` to customize trailing stop behavior.

## Usage

To start the trading algorithm, execute:

```bash
```python
if __name__ == "__main__":
    algorithm = TradingAlgorithm()
    algorithm.run_algorithm(symbol_list=["AAPL", "AMZN", "GOOGL", ...])
```

The bot will run within the defined time frame, checking each stock in the `symbol_list` and placing trades if all conditions are met.

## Contact Information
For any inquiries or concerns regarding this private project, please contact the project owner directly talgolde1@gmail.com.

## Limitations

- **Data Dependence**: Relies on accurate real-time data from Interactive Brokers.
- **Market-Specific**: Designed primarily for U.S. stock markets; modifications may be required for other exchanges.
- **Execution Speed**: Server-side trailing stops offer quick adjustments, but market volatility can still affect execution during rapid price changes.

## License

- This code is provided for educational and informational purposes only. Use it at your own risk. Trading options involves financial risk, and past performance is not indicative of future results.
- This project is private, and all rights are reserved by the project owner. Unauthorized distribution or use of the code is strictly prohibited. This project is licensed under the  [MIT License](LICENSE).

  
## Disclaimer

- This algorithm is provided for educational and informational purposes only. Use it at your own risk.
- Trading options involves financial risk, and past performance is not indicative of future results. Make sure to thoroughly understand the risks before engaging in real trading.
- The developer is not responsible for any losses or damages incurred as a result of using this algorithm.
