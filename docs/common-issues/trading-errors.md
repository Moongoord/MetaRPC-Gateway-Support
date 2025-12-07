# Trading Errors and Solutions

Common trading errors and how to resolve them.

## Table of Contents

- [Order Placement Errors](#order-placement-errors)
- [Invalid Parameters](#invalid-parameters)
- [Account and Balance Issues](#account-and-balance-issues)
- [Market and Symbol Errors](#market-and-symbol-errors)
- [Platform-Specific Issues](#platform-specific-issues)

---

## Order Placement Errors

### Error: "Trade context is busy"

**What it means:**
MetaTrader is currently processing another trading operation and cannot accept new requests.

**Solutions:**
1. Wait a moment and retry the operation
2. Implement retry logic with delays
3. Avoid sending multiple simultaneous orders
4. Check if Expert Advisor is performing other operations

**Example (C#):**
```csharp
int maxRetries = 3;
for (int i = 0; i < maxRetries; i++) {
    try {
        var result = await client.PlaceOrderAsync(order);
        break; // Success
    } catch (TradeContextBusyException) {
        if (i == maxRetries - 1) throw;
        await Task.Delay(500); // Wait 500ms before retry
    }
}
```

### Error: "Requote"

**What it means:**
The price changed between when you requested the order and when it was processed.

**Solutions:**
1. This is normal in fast-moving markets
2. Retry with current market price
3. Use market execution instead of instant execution (if broker supports)
4. Widen your slippage tolerance

---

## Invalid Parameters

### Error: "Invalid price" or "Invalid stops"

**Common causes:**
- Stop Loss/Take Profit too close to current price
- Price not normalized to broker's decimal places
- Using bid price for buy or ask price for sell

**Solutions:**

1. **Check minimum distance from price:**
```python
# Get minimum stop level from broker
min_stop_level = client.get_symbol_info(symbol).stops_level
point = client.get_symbol_info(symbol).point

# Ensure stop loss is far enough
stop_loss = current_price - (min_stop_level + 10) * point
```

2. **Normalize prices:**
```csharp
// Normalize to broker's decimal places
double normalizedPrice = Math.Round(price, broker.Digits);
```

3. **Use correct prices:**
```go
// For BUY: use Ask price
// For SELL: use Bid price
buyPrice := quote.Ask
sellPrice := quote.Bid
```

### Error: "Invalid volume" or "Invalid lots"

**Common causes:**
- Lot size below minimum
- Lot size above maximum
- Lot size not in correct step increments
- Insufficient margin

**Solutions:**

1. **Check broker limits:**
```python
symbol_info = client.get_symbol_info("EURUSD")
min_lot = symbol_info.volume_min  # e.g., 0.01
max_lot = symbol_info.volume_max  # e.g., 100.0
lot_step = symbol_info.volume_step  # e.g., 0.01

# Normalize lot size
lots = round(lots / lot_step) * lot_step
lots = max(min_lot, min(lots, max_lot))
```

---

## Account and Balance Issues

### Error: "Not enough money"

**What it means:**
Insufficient account balance or free margin to place the order.

**Solutions:**

1. **Check account balance:**
```csharp
var accountInfo = await client.GetAccountInfoAsync();
Console.WriteLine($"Balance: {accountInfo.Balance}");
Console.WriteLine($"Free Margin: {accountInfo.FreeMargin}");
```

2. **Calculate required margin:**
```python
# Calculate margin required for order
symbol_info = client.get_symbol_info(symbol)
margin_required = (lots * symbol_info.contract_size * price) / leverage

if margin_required > account.free_margin:
    print("Insufficient margin")
```

3. **Reduce lot size or close other positions**

### Error: "Trade is disabled"

**Common causes:**
- AutoTrading disabled in MetaTrader
- Trading disabled for specific symbol
- Account is in read-only mode
- Market is closed

**Solutions:**
1. Enable AutoTrading button in MetaTrader (green button in toolbar)
2. Check if symbol allows trading: `symbol_info.trade_mode`
3. Verify account permissions with broker
4. Check market hours for the symbol

---

## Market and Symbol Errors

### Error: "Symbol not found" or "Unknown symbol"

**Solutions:**

1. **Check symbol name:**
```go
// Symbol names may have broker-specific suffixes
// Correct: "EURUSD", "EURUSDm", "EURUSD.a"
symbols := client.GetSymbols()
for _, s := range symbols {
    fmt.Println(s.Name)
}
```

2. **Show symbol in Market Watch:**
```python
# Some brokers require symbol to be visible
client.show_symbol(symbol)
```

### Error: "Market is closed"

**What it means:**
Trading session is closed for this symbol.

**Solutions:**
1. Check trading hours for the symbol
2. Use `symbol_info.session` to get trading schedule
3. Implement time-based checks before trading

```csharp
var symbolInfo = await client.GetSymbolInfoAsync(symbol);
if (symbolInfo.TradeMode == TradeMode.Disabled) {
    Console.WriteLine("Trading disabled for this symbol");
}
```

### Error: "Off quotes"

**What it means:**
No current price quotes available for the symbol.

**Solutions:**
1. Market may be closed
2. No liquidity for the symbol
3. Connection issue with broker's price feed
4. Wait for market to open or switch to different symbol

---

## Platform-Specific Issues

### MT4 vs MT5 Differences

#### Order System

**MT4:**
- Uses ticket-based order system
- Each order has a unique ticket number
- Orders and positions are the same

**MT5:**
- Separate orders and positions
- Position can have multiple orders
- Orders have execution tickets

```python
# MT4
order_ticket = client.order_send(...)
position = client.order_select(order_ticket)

# MT5
order_result = client.order_send(...)
position = client.position_get_ticket(order_result.position)
```

#### Hedging vs Netting

**MT5 supports two account types:**

1. **Hedging:** Can have multiple positions for same symbol (like MT4)
2. **Netting:** Only one position per symbol (positions are merged)

```csharp
// Check account type
var accountInfo = await client.GetAccountInfoAsync();
if (accountInfo.MarginMode == MarginMode.Netting) {
    // Only one position per symbol
    // New order in opposite direction will close/reduce position
}
```

---

## Error Code Reference

Common error codes and their meanings:

| Code | MT4 Error | Meaning | Solution |
|------|-----------|---------|----------|
| 2 | ERR_COMMON_ERROR | Common error | Check logs for details |
| 3 | ERR_INVALID_TRADE_PARAMETERS | Invalid parameters | Verify all order parameters |
| 4 | ERR_SERVER_BUSY | Trade server is busy | Wait and retry |
| 6 | ERR_NO_CONNECTION | No connection | Check internet/broker connection |
| 8 | ERR_TOO_FREQUENT_REQUESTS | Too many requests | Slow down request rate |
| 128 | ERR_TRADE_TIMEOUT | Trade timeout | Retry the operation |
| 129 | ERR_INVALID_PRICE | Invalid price | Refresh price and retry |
| 130 | ERR_INVALID_STOPS | Invalid stop loss/take profit | Adjust stops according to minimum distance |
| 131 | ERR_INVALID_TRADE_VOLUME | Invalid volume | Check min/max/step lot size |
| 134 | ERR_NOT_ENOUGH_MONEY | Not enough money | Reduce lot size or deposit funds |
| 136 | ERR_OFF_QUOTES | No quotes | Wait for market to open |
| 138 | ERR_REQUOTE | Price changed | Retry with new price |
| 141 | ERR_TOO_MANY_REQUESTS | Too many requests | Reduce request frequency |
| 145 | ERR_TRADE_MODIFY_DENIED | Modification denied | Check if order can be modified |
| 146 | ERR_TRADE_CONTEXT_BUSY | Trade context busy | Wait and retry |

---

## Debugging Trading Issues

### Step-by-step debugging:

1. **Enable verbose logging:**
```python
import logging
logging.basicConfig(level=logging.DEBUG)
```

2. **Check order parameters:**
```csharp
Console.WriteLine($"Symbol: {symbol}");
Console.WriteLine($"Volume: {volume}");
Console.WriteLine($"Price: {price}");
Console.WriteLine($"SL: {stopLoss}, TP: {takeProfit}");
```

3. **Verify symbol specifications:**
```go
info, _ := client.GetSymbolInfo(symbol)
fmt.Printf("Min Lot: %f, Max Lot: %f, Step: %f\n",
    info.VolumeMin, info.VolumeMax, info.VolumeStep)
fmt.Printf("Stops Level: %d, Spread: %d\n",
    info.StopsLevel, info.Spread)
```

4. **Test on demo account first**
5. **Start with minimum lot size**
6. **Check MetaTrader Experts/Journal tabs**

---

## Getting More Help

If you're still experiencing trading errors:

1. **Check the FAQ:** [FAQ.md](../FAQ.md)
2. **Search existing discussions:** Someone may have had the same issue
3. **Create a discussion** with:
   - Complete error message
   - Your code (remove sensitive data)
   - Symbol and broker information
   - Account type (demo/live, hedging/netting)
   - Screenshot of MetaTrader Experts tab

[Create a Discussion](../../../discussions) to get help from the community!
