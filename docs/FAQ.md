# Frequently Asked Questions (FAQ)

## General Questions

### What is the MetaTrader Gateway?

The MetaTrader Gateway is a service that allows you to connect to MetaTrader 4 and MetaTrader 5 platforms from various programming languages. It provides a bridge between your code and the MetaTrader terminal, enabling you to build trading strategies, custom applications, and automated trading systems.

### Which languages are supported?

We currently support:
- **C#** (MT4 & MT5)
- **Go** (MT4 & MT5)
- **Python** (MT4 & MT5)
- **Java** (MT5 only, MT4 coming soon)

More languages are planned for the future.

### What's the difference between MT4 and MT5?

- **MT4 (MetaTrader 4)** - Older platform, primarily for Forex trading
- **MT5 (MetaTrader 5)** - Newer platform with more features, supports stocks, futures, and Forex

Our libraries support both platforms (except Java, which currently only supports MT5).

---

## Connection Issues

### I can't connect to the gateway

**Common solutions:**
1. Verify the gateway is running and accessible
2. Check your connection credentials
3. Ensure the MetaTrader terminal is running
4. Check firewall settings
5. Verify network connectivity

### Connection timeout errors

**Possible causes:**
- Gateway is not running
- Incorrect host/port configuration
- Network firewall blocking the connection
- MetaTrader terminal not running

**Solution:** Check all connection parameters and ensure the gateway service is running.

---

## Trading Issues

### Orders are not being placed

**Common causes:**
1. Insufficient account balance
2. Invalid symbol or lot size
3. Market is closed
4. Trading is disabled in MetaTrader settings
5. Broker restrictions

**Solution:** Check your account details, symbol validity, and broker requirements.

### How do I handle order errors?

Always check error codes returned by the gateway. Each error code corresponds to a specific issue:
- **Invalid price** - Check if the price is within acceptable range
- **Invalid volume** - Verify lot size meets broker requirements
- **Market is closed** - Wait for market hours
- **Not enough money** - Check account balance

---

## Platform-Specific Questions

### Can I use the same code for MT4 and MT5?

The APIs are very similar, but there are some differences between MT4 and MT5 platforms:
- MT5 has a different order system (positions vs. orders)
- Some functions have different names or parameters
- Symbol properties may differ

Check the specific library documentation for your language.

### Which platform should I use?

- **Use MT4** if your broker only supports MT4, or you need compatibility with older systems
- **Use MT5** if you want more features, better performance, and future compatibility

---

## Development Questions

### How do I debug my code?

1. Enable logging in your application
2. Check MetaTrader terminal logs (Experts tab)
3. Use try-catch blocks to handle errors
4. Test with a demo account first
5. Start with simple operations before complex strategies

### Can I use this on a VPS?

Yes! Our libraries work on VPS (Virtual Private Server) environments. Make sure:
- The VPS has the required runtime (.NET, Python, Java, etc.)
- MetaTrader terminal is installed and running
- Gateway is configured and running
- Network ports are accessible

### Is the gateway safe to use?

Yes, the gateway runs locally and communicates with your MetaTrader terminal. Your credentials and trading data never leave your machine unless you explicitly send them elsewhere.

**Security best practices:**
- Never share your gateway credentials
- Use environment variables for sensitive data
- Don't commit credentials to version control
- Use secure connections when deploying

---

## Getting Help

### Where can I ask questions?

- **GitHub Discussions** - Best for technical questions and community support
- Check existing discussions first - your question might already be answered
- Provide code samples and error messages when asking for help

### How do I report a bug?

Use the **Bug Report** template in GitHub Discussions. Include:
1. Clear description of the issue
2. Steps to reproduce
3. Code sample (minimal reproduction)
4. Error messages and stack traces
5. Environment details (language version, OS, MT version)
6. Attach ZIP file with your project if needed

### Can I share my trading strategies?

Yes! Use the **Show and Tell** category to share your projects. Just remember to:
- Remove sensitive data (API keys, account numbers)
- Remove proprietary trading logic if you want to keep it private
- Share interesting technical implementations

---

## Common Error Messages

### "Connection refused"
- Gateway is not running
- Incorrect host/port
- Firewall blocking connection

### "Authentication failed"
- Wrong credentials
- Gateway not properly configured

### "Symbol not found"
- Symbol doesn't exist on your broker
- Incorrect symbol name
- Market data not loaded in MetaTrader

### "Invalid volume"
- Lot size outside broker limits
- Lot size not a valid step (e.g., broker requires 0.01 increments)

### "Trade context busy"
- Another operation is in progress
- Wait and retry the operation

---

## Performance Tips

### How can I improve performance?

1. **Batch operations** when possible
2. **Use subscriptions** for real-time data instead of polling
3. **Minimize API calls** - cache data when appropriate
4. **Use async/await** patterns for non-blocking operations
5. **Close connections** properly when done

### What's the maximum number of requests?

This depends on:
- Your broker's limitations
- Gateway configuration
- Network bandwidth
- MetaTrader terminal capacity

For high-frequency trading, consider optimizing your code and testing with your broker's limits.

---

**Still have questions?** Check our [GitHub Discussions](../../../discussions) or create a new discussion to get help from the community!
