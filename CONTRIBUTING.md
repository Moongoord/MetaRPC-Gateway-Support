# Contributing to MetaTrader Gateway Support

Thank you for your interest in helping the community! This guide explains how you can contribute to making this support repository better.

## How You Can Help

### 1. Answer Questions

Help other developers by answering questions in [GitHub Discussions](../../discussions).

**Good answers include:**
- Clear explanations
- Code examples
- References to documentation
- Personal experience and tips

**Example:**
```
I had the same issue! The problem is that you need to normalize
the lot size to your broker's step.

Try this:

```python
lot_step = symbol_info.volume_step
lots = round(lots / lot_step) * lot_step
```

This worked for me on [Broker Name].
```

### 2. Share Your Solutions

Found a solution to a tricky problem? Share it!

- Reply to existing discussions with your solution
- Create a "Show and Tell" discussion about your project
- Suggest improvements to documentation

### 3. Report Issues

Help us improve by reporting:
- Bugs in the libraries
- Unclear documentation
- Missing examples
- Broken links

Use the **Bug Report** template and include:
- Clear description
- Steps to reproduce
- Expected vs actual behavior
- Your environment (language, OS, MT version)

### 4. Suggest Improvements

Have ideas for new features or better workflows?

Use the **Ideas** template to suggest:
- New library features
- Documentation improvements
- Better error messages
- Tool enhancements

### 5. Improve Documentation

Documentation can always be better!

**You can help by:**
- Fixing typos or unclear explanations
- Adding code examples
- Translating to other languages
- Creating tutorials or guides

**How to contribute documentation:**
1. Fork this repository
2. Make your changes in the `docs/` folder
3. Submit a Pull Request
4. Describe what you improved

---

## Discussion Guidelines

### Before Posting

1. **Search first** - Check if your question has been answered
2. **Read the docs** - Check FAQ and language-specific documentation
3. **Use the right template** - Choose the appropriate discussion template

### When Asking Questions

**Good questions include:**
- Clear, descriptive title
- What you're trying to achieve
- What you've already tried
- Code samples (minimal reproduction)
- Error messages (complete stack trace)
- Environment details

**Example of a good question:**

```
Title: How to handle "Invalid stops" error when placing orders?

I'm trying to place a buy order with stop loss but getting error 130
(Invalid stops).

My code (Python):
```python
order = client.order_send(
    symbol="EURUSD",
    volume=0.1,
    type=ORDER_TYPE_BUY,
    price=1.0850,
    sl=1.0840,  # 10 pips stop loss
    tp=1.0870
)
```

Error: ERR_INVALID_STOPS (130)

Environment:
- Python 3.11
- MT5 build 3850
- Broker: XYZ Demo
- OS: Windows 11

I've tried increasing the stop loss distance but still get the error.
```

### When Answering Questions

**Be helpful and respectful:**
- Assume good intent
- Be patient with beginners
- Provide context and explanations
- Test your suggestions when possible

**Good answer structure:**
1. Acknowledge the issue
2. Explain the cause
3. Provide a solution
4. Add context or alternatives

---

## Code Contribution Guidelines

### For Library Improvements

If you want to contribute code to the actual libraries (CSharpMT4, GoMT5, etc.):

1. **Discuss first** - Create an "Idea" discussion
2. **Wait for approval** - Maintainers will review the proposal
3. **Follow coding standards** - Use consistent style
4. **Add tests** - Include unit tests for new features
5. **Update documentation** - Document your changes

### For Examples and Tutorials

Contributing examples is highly encouraged!

**Good examples:**
- Solve a specific problem
- Include comments
- Are complete and runnable
- Follow best practices
- Remove sensitive data

**How to submit:**
1. Create a "Show and Tell" discussion
2. Share your code and explanation
3. Maintainers may add it to official examples

---

## Community Standards

### Be Respectful

- Treat everyone with respect
- Be welcoming to newcomers
- No harassment or discrimination
- Constructive criticism only

### Be Professional

- Keep discussions on-topic
- No spam or self-promotion
- No sharing of pirated software or illegal content
- Respect confidentiality and trading data

### Security Best Practices

**Never share:**
- API keys or credentials
- Account numbers
- Live trading strategies (if confidential)
- Broker login details

**Always:**
- Remove sensitive data from code samples
- Use demo accounts for examples
- Warn others about security risks

---

## Recognition

Contributors who consistently help the community may be:
- Highlighted in announcements
- Given special badges/recognition
- Invited to beta test new features
- Listed in contributors section

---

## Questions About Contributing?

- Create a discussion in [General Q&A](../../discussions)
- Ask in existing contribution discussions
- Reach out to maintainers

Thank you for making this community better! 🚀
