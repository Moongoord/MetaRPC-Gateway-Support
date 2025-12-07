# Connection Problems

This guide covers common connection issues and their solutions.

## Table of Contents

- [Gateway Connection Issues](#gateway-connection-issues)
- [MetaTrader Connection Issues](#metatrader-connection-issues)
- [Network Issues](#network-issues)
- [Authentication Issues](#authentication-issues)

---

## Gateway Connection Issues

### Problem: "Connection refused" or "Cannot connect to gateway"

**Symptoms:**
- Your application fails to connect to the gateway
- Connection timeout errors
- "Connection refused" error messages

**Solutions:**

1. **Verify gateway is running**
   - Check if the gateway process is active
   - Look for gateway logs to confirm it's running
   - Try restarting the gateway service

2. **Check host and port configuration**
   ```
   Correct:   localhost:8080  or  127.0.0.1:8080
   Incorrect: localhost:80    or  192.168.1.1:8080 (if gateway is local)
   ```

3. **Verify firewall settings**
   - Windows Firewall might be blocking the connection
   - Add an exception for the gateway port
   - Temporarily disable firewall to test (re-enable after)

4. **Check if port is already in use**
   ```bash
   # Windows
   netstat -ano | findstr :8080

   # Linux/Mac
   lsof -i :8080
   ```

---

## MetaTrader Connection Issues

### Problem: Gateway connects but can't communicate with MetaTrader

**Symptoms:**
- Gateway is running but operations fail
- "MetaTrader not responding" errors
- Timeout on trading operations

**Solutions:**

1. **Ensure MetaTrader terminal is running**
   - Open MetaTrader 4 or MetaTrader 5
   - Login to your trading account
   - Make sure AutoTrading is enabled (button in toolbar)

2. **Check Expert Advisor is loaded**
   - The gateway requires an EA (Expert Advisor) running in MetaTrader
   - Check the "Experts" tab in MetaTrader for errors
   - Reload the EA if needed

3. **Verify account is connected**
   - Look for "Connected" status in MetaTrader status bar
   - Check your internet connection
   - Verify broker server is accessible

4. **Enable AutoTrading**
   - Click the "AutoTrading" button in MetaTrader toolbar (should be green)
   - If it's red, click it to enable automated trading
   - Some brokers require enabling AutoTrading in settings

---

## Network Issues

### Problem: Connection works locally but fails on VPS/remote server

**Symptoms:**
- Works on your local machine but not on VPS
- Intermittent connection failures
- High latency or timeouts

**Solutions:**

1. **Check VPS network configuration**
   - Ensure VPS can reach the gateway
   - Test with ping or telnet to verify connectivity
   - Check VPS firewall rules

2. **Verify gateway is listening on correct interface**
   - Gateway might be bound to localhost only
   - Configure gateway to listen on 0.0.0.0 or specific IP
   - Update your connection string accordingly

3. **Use correct IP address**
   ```
   Local:     localhost or 127.0.0.1
   VPS:       VPS public IP or private network IP
   ```

4. **Check network latency**
   - High latency can cause timeouts
   - Increase timeout values in your code
   - Consider using a VPS closer to your broker's servers

---

## Authentication Issues

### Problem: "Authentication failed" or "Unauthorized"

**Symptoms:**
- Connection is established but authentication fails
- "Invalid credentials" errors
- Permission denied errors

**Solutions:**

1. **Verify credentials are correct**
   - Double-check API key, username, and password
   - Ensure no extra spaces or hidden characters
   - Use environment variables to avoid typos

2. **Check credential configuration**
   - Credentials should match gateway configuration
   - Some implementations use API keys, others use username/password
   - Refer to your language-specific documentation

3. **Regenerate credentials**
   - If using API keys, regenerate them in gateway settings
   - Update your application with new credentials
   - Restart both gateway and application

4. **Permission issues**
   - Ensure your account has trading permissions
   - Check if broker allows API trading
   - Verify account type supports automated trading

---

## Language-Specific Connection Examples

### C# Connection Example
```csharp
// Ensure proper connection parameters
var client = new MT5Client("localhost", 8080);
try {
    await client.ConnectAsync();
    // Connection successful
} catch (Exception ex) {
    Console.WriteLine($"Connection failed: {ex.Message}");
    // Check gateway is running
    // Verify host and port
}
```

### Python Connection Example
```python
# Proper error handling for connection
try:
    client = MT5Client(host="localhost", port=8080)
    client.connect()
    # Connection successful
except ConnectionError as e:
    print(f"Connection failed: {e}")
    # Check gateway is running
    # Verify host and port
```

### Go Connection Example
```go
// Connection with timeout
client := mt5.NewClient("localhost:8080")
ctx, cancel := context.WithTimeout(context.Background(), 10*time.Second)
defer cancel()

if err := client.Connect(ctx); err != nil {
    log.Printf("Connection failed: %v", err)
    // Check gateway is running
    // Verify host and port
}
```

### Java Connection Example
```java
// Connection with retry logic
MT5Client client = new MT5Client("localhost", 8080);
try {
    client.connect();
    // Connection successful
} catch (ConnectionException e) {
    System.out.println("Connection failed: " + e.getMessage());
    // Check gateway is running
    // Verify host and port
}
```

---

## Debugging Connection Issues

### Step-by-step debugging process:

1. **Test gateway is running**
   ```bash
   curl http://localhost:8080/health
   # or
   telnet localhost 8080
   ```

2. **Check MetaTrader terminal**
   - Is it running?
   - Is it logged in?
   - Is AutoTrading enabled?

3. **Review logs**
   - Gateway logs
   - MetaTrader Experts tab
   - Your application logs

4. **Test with minimal code**
   - Create a simple connection test
   - Remove all complex logic
   - Verify basic connection works

5. **Network diagnostics**
   ```bash
   # Test port is open
   telnet localhost 8080

   # Check what's listening on the port
   netstat -an | findstr :8080
   ```

---

## Still Having Issues?

If you've tried all the solutions above and still have connection problems:

1. **Create a GitHub Discussion**
   - Use the "Bug Report" or "Question" template
   - Include error messages and logs
   - Specify your language, platform (MT4/MT5), and environment

2. **Provide the following information:**
   - Operating system (Windows/Linux/Mac)
   - Language and version (e.g., Python 3.11, .NET 6.0)
   - MetaTrader version and build number
   - Gateway version/configuration
   - Complete error messages and stack traces
   - Network setup (local/VPS/remote)

3. **Attach diagnostics:**
   - Gateway logs
   - MetaTrader Experts tab screenshot
   - Your connection code (remove sensitive data!)
   - Network diagnostic output

[Create a Discussion](../../../discussions) to get help from the community!
