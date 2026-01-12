# Hibas Status Page - Next Steps

## Current Status: LIVE

**URL:** https://salberg87.github.io/website-status/

**What's working:**
- Monitoring 3 sites every 5 minutes (Hibas Test, Hibas Preview, Hafjell Hytter)
- Status page with Hibas branding (blue gradient, matching preview.hibas.no)
- Norwegian localization
- GitHub Issue alerts when sites go down
- Weekly broken link checker (Mondays 7am UTC)

---

## TODO: Set Up Transactional Email Notifications

Currently notifications only work via GitHub (watching the repo). To send real emails to `fredrik@pifre.no` and `Hansi@hibas.no`:

### Option 1: SendGrid (Recommended - Free tier: 100 emails/day)

1. **Create SendGrid account:** https://sendgrid.com/
2. **Create API key:** Settings → API Keys → Create API Key (Full Access)
3. **Verify sender:** Settings → Sender Authentication → Verify `status@hibas.no` or similar
4. **Add GitHub Secret:**
   - Go to: https://github.com/Salberg87/website-status/settings/secrets/actions
   - New secret: `NOTIFICATION_EMAIL_SENDGRID` = your API key

5. **Update `.upptimerc.yml`:**
```yaml
notifications:
  - type: email
    from: status@hibas.no
    to: fredrik@pifre.no
  - type: email
    from: status@hibas.no
    to: Hansi@hibas.no
```

### Option 2: Mailgun

1. **Create Mailgun account:** https://www.mailgun.com/
2. **Get API key and domain**
3. **Add GitHub Secrets:**
   - `NOTIFICATION_EMAIL_MAILGUN` = API key
   - `NOTIFICATION_EMAIL_MAILGUN_DOMAIN` = your domain

### Option 3: AWS SES (if you already use AWS)

1. **Verify sender email in SES**
2. **Create IAM user with SES permissions**
3. **Add GitHub Secrets:**
   - `NOTIFICATION_EMAIL_SES_REGION` = eu-north-1 (or your region)
   - `NOTIFICATION_EMAIL_SES_ACCESS_KEY_ID` = IAM access key
   - `NOTIFICATION_EMAIL_SES_SECRET_ACCESS_KEY` = IAM secret

### Option 4: Any SMTP Server

```yaml
notifications:
  - type: email
    from: status@hibas.no
    to: fredrik@pifre.no
```

**GitHub Secrets:**
- `NOTIFICATION_EMAIL_SMTP_HOST` = smtp.example.com
- `NOTIFICATION_EMAIL_SMTP_PORT` = 587
- `NOTIFICATION_EMAIL_SMTP_USERNAME` = username
- `NOTIFICATION_EMAIL_SMTP_PASSWORD` = password

---

## TODO: Add hibas.no After Launch (Jan 15)

Uncomment in `.upptimerc.yml`:
```yaml
  - name: Hibas
    url: https://hibas.no
    maxResponseTime: 5000
    icon: https://hibas.no/favicon.ico
```

---

## Optional Enhancements

- **Slack notifications:** Add webhook URL as `NOTIFICATION_SLACK_WEBHOOK`
- **SMS alerts:** Use Twilio with `NOTIFICATION_SMS_TWILIO_*` secrets
- **Custom domain:** Point `status.hibas.no` to GitHub Pages

---

## Files Reference

| File | Purpose |
|------|---------|
| `.upptimerc.yml` | Main configuration |
| `assets/custom.css` | Hibas-branded styling |
| `.github/workflows/links.yml` | Weekly broken link checker |

## Repo

https://github.com/Salberg87/website-status
