# Multi-Service Keep Alive

GitHub Actions workflows to automatically keep your services from going inactive.

## 🚀 Features

### Hugging Face Space
- ✅ Automatically pings your Hugging Face Space every 30 minutes
- ✅ Prevents Space from going inactive due to inactivity

### Supabase Database  
- ✅ Weekly ping to prevent Supabase project pausing (7-day inactivity limit)
- ✅ Uses dedicated database table for activity tracking
- ✅ Free to use (GitHub Actions free tier)

### General
- ✅ Manual trigger support
- ✅ Failure notifications
- ✅ Free to use (GitHub Actions free tier)

## ⚙️ Setup Instructions

### 1. Configure Secrets

Go to your repository Settings → Secrets and variables → Actions

**For Hugging Face:**
- `HF_USERNAME`: Your Hugging Face username
- `HF_SPACE_NAME`: Your Space name

**For Supabase:**
- `SUPABASE_URL`: Your Supabase project URL (e.g., `https://xxxxxx.supabase.co`)
- `SUPABASE_ANON_KEY`: Your Supabase anon public key (from Settings → API)

### 2. Supabase Database Setup

Before using the Supabase keep-alive, create the required table:

```sql
-- Run this in your Supabase SQL Editor
CREATE TABLE IF NOT EXISTS keep_alive_pings (
  id SERIAL PRIMARY KEY,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Insert initial data
INSERT INTO keep_alive_pings (created_at) VALUES (NOW());
```

### 3. Test the Workflows

1. Go to the Actions tab
2. Select either "Hugging Face Space Keep Alive" or "Supabase Keep-Alive" workflow
3. Click "Run workflow" to test manually

## 🔧 Configuration

### Hugging Face Schedule
Edit `.github/workflows/keep-alive.yml`:
```yaml
schedule:
  - cron: "*/30 * * * *"  # Every 30 minutes
```

### Supabase Schedule  
Edit `.github/workflows/supabase-keep-alive.yml`:
```yaml
schedule:
  - cron: '30 5 * * 1'    # Every Monday at 5:30 AM UTC
```

## 📊 Monitoring

- Check the Actions tab for execution logs
- View success/failure status
- Monitor service activity on respective platforms

## ❓ Troubleshooting

### Common Issues

**Hugging Face:**
- Secrets not configured
- Space not public  
- Rate limiting

**Supabase:**
- `keep_alive_pings` table not created
- Invalid URL or anon key
- Database permissions issues

### Debug Mode

Workflows include detailed logging. Check the Actions output for specific error messages.

## 📝 License

MIT License - feel free to use and modify as needed.

## 🤝 Contributing

Feel free to submit issues and enhancement requests!

---

**Note**: These workflows help prevent services from going inactive, but cannot prevent other platform-specific resource limitations.