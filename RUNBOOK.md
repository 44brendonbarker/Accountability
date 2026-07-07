# Execute Your Life — Production Runbook

## Service

- **Production:** https://execute-your-life.vercel.app
- **Vercel project:** `upgrade` (team: BBANX)
- **GitHub:** https://github.com/44brendonbarker/Accountability
- **Stack:** Static HTML/CSS/JS PWA (no serverless functions)

## Incident response

### Severity levels

| Level | Example | Response |
|-------|---------|----------|
| P1 | Production down or data loss | Immediate rollback + notify owner |
| P2 | Broken UI, PWA install fails | Fix forward or rollback within 1h |
| P3 | Minor visual bug | Schedule fix in next deploy |

### Escalation

1. **Owner:** Brendon Barker (`brendonbarker1998@gmail.com`)
2. **Status page:** https://www.vercel-status.com
3. **Vercel dashboard:** https://vercel.com/bbanx/upgrade

### Communication

- Confirm impact (production vs preview only)
- Note deployment ID from Vercel dashboard
- Post resolution summary after fix

## Rollback

1. Open https://vercel.com/bbanx/upgrade/deployments
2. Find last known-good **production** deployment (`target: production`, state: READY)
3. Click **⋯ → Promote to Production** (or Instant Rollback)
4. Verify https://execute-your-life.vercel.app loads and shows the app shell

Known-good production candidate: check `isRollbackCandidate` deployments in dashboard.

## Deploy

### Via Git (preferred)

Push to `main` on `44brendonbarker/Accountability` — Vercel auto-deploys.

### Manual (API/CLI)

From `/Users/beej/execute-your-life`:

```bash
npx vercel deploy --prod
```

## Monitoring

- **Speed Insights:** enabled in Vercel project settings
- **Web Analytics:** enabled in Vercel project settings
- **Log drains:** configure in Vercel dashboard (Pro recommended)

## Dashboard actions (Hobby → Pro)

These require Vercel dashboard / plan upgrade:

- [ ] Spend Management alerts: Settings → Billing
- [ ] Log Drains: Project → Settings → Drains
- [ ] WAF + bot blocking: Project → Firewall (Pro)
- [ ] Custom domain DNS: Domains → Add domain
- [ ] Preview Deployment Suffix (Pro)

## Security notes

- Deployment Protection (SSO) is enabled for previews; production `*.vercel.app` remains public.
- All user data is stored in browser `localStorage` only — no server-side database.
- Security headers are configured in `vercel.json`.