# Hugging Face Space Keep Alive

GitHub Actions workflow to automatically keep your Hugging Face Space from going inactive.

## 🚀 Features

- ✅ Automatically pings your Hugging Face Space every 30 minutes
- ✅ Prevents Space from going inactive due to inactivity
- ✅ Free to use (GitHub Actions free tier)
- ✅ Manual trigger support
- ✅ Failure notifications

## ⚙️ Setup Instructions

### 1. Configure Secrets

Go to your repository Settings → Secrets and variables → Actions

Add the following secrets:

- `HF_USERNAME`: Your Hugging Face username
- `HF_SPACE_NAME`: Your Space name

### 2. Test the Workflow

1. Go to the Actions tab
2. Select "Hugging Face Space Keep Alive" workflow
3. Click "Run workflow" to test manually

### 3. Automatic Scheduling

The workflow will automatically run:
- Every 30 minutes (UTC time)
- On every push to main branch
- Manually when triggered

## 🔧 Configuration

### Custom Schedule

Edit the cron schedule in `.github/workflows/keep-alive.yml`:

```yaml
schedule:
  - cron: "*/30 * * * *"  # Every 30 minutes
  # - cron: "0 */6 * * *"   # Every 6 hours
  # - cron: "0 9 * * *"     # Daily at 9:00 AM UTC
```

### Notification Settings

By default, the workflow will create a GitHub Issue if it fails. You can customize this behavior in the workflow file.

## 📊 Monitoring

- Check the Actions tab for execution logs
- View success/failure status
- Monitor Space activity on Hugging Face

## ❓ Troubleshooting

### Common Issues

1. **Secrets not configured** - Make sure `HF_USERNAME` and `HF_SPACE_NAME` are set
2. **Space not public** - Ensure your Space is publicly accessible
3. **Rate limiting** - If using free tier, respect Hugging Face's rate limits

### Debug Mode

To enable debug output, add `-v` flag to the curl command in the workflow.

## 📝 License

MIT License - feel free to use and modify as needed.

## 🤝 Contributing

Feel free to submit issues and enhancement requests!

---

**Note**: This workflow helps prevent your Space from going inactive, but cannot prevent other Hugging Face resource limitations.