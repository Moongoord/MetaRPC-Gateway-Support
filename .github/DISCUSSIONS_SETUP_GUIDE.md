# GitHub Discussions Setup Guide

This guide is for repository maintainers to set up GitHub Discussions for the Support repository.

## Step 1: Enable Discussions

1. Go to your repository Settings page
2. Scroll to the "Features" section
3. Check the box next to "Discussions"
4. Click "Set up discussions"

## Step 2: Configure Categories

GitHub will create default categories. Replace them with these:

### Categories to Create:

| Category | Type | Description |
|----------|------|-------------|
| 💬 General Q&A | Q&A | General questions about the gateway and libraries |
| 🔧 C# Support | Q&A | Questions about C# (MT4/MT5) implementation |
| 🐹 Go Support | Q&A | Questions about Go (MT4/MT5) implementation |
| 🐍 Python Support | Q&A | Questions about Python (MT4/MT5) implementation |
| ☕ Java Support | Q&A | Questions about Java (MT5) implementation |
| 🐛 Bug Reports | Discussion | Report bugs and troubleshoot issues |
| 💡 Ideas | Discussion | Feature requests and improvements |
| 🎉 Show and Tell | Discussion | Share your projects and trading strategies |
| 📢 Announcements | Announcement | Official updates (maintainers only) |

### Steps to configure:
1. Go to your repository `/discussions/categories`
2. Delete default categories
3. Click "New category" for each one above
4. For "Announcements", check "Only maintainers can post"

## Step 3: Create Labels

Create these labels for better organization:

### Language Labels:
- `lang:csharp` - #178600
- `lang:go` - #00ADD8
- `lang:python` - #3776AB
- `lang:java` - #007396

### Platform Labels:
- `platform:mt4` - #FF6B35
- `platform:mt5` - #004E89

### Status Labels:
- `needs-info` - #FFA500
- `solved` - #00FF00
- `duplicate` - #CCCCCC

### Priority Labels:
- `priority:high` - #FF0000
- `priority:low` - #0000FF

## Step 4: Create Welcome Post (Optional)

1. Go to your repository Discussions
2. Click "New discussion"
3. Select "📢 Announcements" category
4. Create a welcome post introducing the support repository
5. Pin the discussion (click "..." → "Pin discussion")

Example welcome post:
```markdown
# Welcome to MetaTrader Gateway Support! 👋

This is the official support repository for all our MetaTrader Gateway libraries.

## How to Get Help

1. **Search first** - Check if your question has been answered
2. **Choose the right category** - Use language-specific categories
3. **Provide details** - Include code, errors, and environment info
4. **Be patient** - We'll respond as soon as possible

## Supported Languages

- C# (MT4/MT5)
- Go (MT4/MT5)
- Python (MT4/MT5)
- Java (MT5)

Happy trading! 🚀
```

## Step 5: Discussion Templates

The templates are already created in `.github/DISCUSSION_TEMPLATE/`:
- `question.yml` - For Q&A categories
- `bug-report.yml` - For Bug Reports
- `idea.yml` - For Ideas
- `show-and-tell.yml` - For Show and Tell

These will automatically appear when users create new discussions.

## Step 6: Update Repository Settings

Consider enabling these options in Settings → Discussions:
- ✅ Allow users to create discussions
- ✅ Allow users to comment on discussions
- ✅ Show discussions on the repository homepage

## Managing Discussions

### As a Maintainer:

**Daily Tasks:**
- Answer questions in language-specific categories
- Mark best answers in Q&A discussions
- Add appropriate labels (language, platform, priority)
- Convert confirmed bugs to issues in relevant repositories

**Weekly Tasks:**
- Review unanswered discussions
- Pin important/frequently asked questions
- Update FAQ based on common questions
- Clean up spam or duplicate discussions

**Best Practices:**
- Respond within 24-48 hours when possible
- Ask for more details if needed (code, errors, environment)
- Reference relevant repository documentation
- Be friendly and helpful to encourage community participation
- When users attach ZIP files, download and investigate locally

### Handling ZIP File Submissions:

When users upload project files:
1. Download the ZIP file from the discussion
2. Scan for sensitive data before investigating
3. Test their code in your local environment
4. Provide specific fixes or suggestions
5. Ask them to update their code and report back

## Useful Commands

### Convert discussion to issue:
```
Go to discussion → Click "..." → "Convert to issue"
```
Then transfer to the appropriate language repository.

### Transfer discussion to another category:
```
Go to discussion → Right sidebar → "Category" → Select new category
```

### Add labels:
```
Go to discussion → Right sidebar → "Labels" → Select labels
```

## Monitoring and Notifications

Set up notifications for:
- New discussions (Watch → Custom → Discussions)
- Mentions and replies
- Specific categories

Configure in your repository subscription settings.

## Auto-labeling (Optional - Future)

You can set up GitHub Actions to automatically label discussions based on:
- Selected language in the template
- Selected platform in the template
- Keywords in the discussion title/body

This would require creating a workflow in `.github/workflows/`.

---

Once discussions are enabled, users will see:
- "Discussions" tab in repository
- Templates when creating new discussions
- Easy way to search for solutions
- Community-driven support system
