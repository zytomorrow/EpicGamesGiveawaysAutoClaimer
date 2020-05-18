# EpicGames Giveaways Auto Claimer

[中文版](./README.md), [English Version](./README_EN.md).

Using GitHub Actions to auto claim Epic Giveaways.

1.  `Get_Epic_Game.yml`: GitHub Actions to claim Epic Giveaways.

# Known Issues

- Perhaps GitHub Actions IP problem, sometimes script failed to claim/login.
  - **Because this sample repo pre-defined a scheduled time, many scripts run at the same time may cause Epic defense mechanism. Edit schedule time is recommended.**
- GTA5 claim failed reason：https://github.com/Revadike/epicgames-freebies-claimer/issues/22

# Config

**Note：If you fork this repo, enable Actions execution in Actions tab first.**

In 'Settings' - 'Secrets' page, add three variables: `EMAIL` (Epic account), `PASSWD` (Epic password), `SECRET` (2FA secret).

If you need telegram bot notification, add `TELEGRAM_TO` (which is Telegram account id, can get by @userinfobot), `TELEGRAM_TOKEN` (which is bot token, can get by @BotFather when the bot is created).

Note: you need to send a message to your bot, or a `Bad Request: chat not found` error will raise.

2FA secret can be found in the QR-code page when you are enabling 2FA. If you already enabled 2FA, disable and re-enable it, a new secret will display.

Then, edit `.github/workflows/Get_Epic_Game.yml`, remove `#` at line start:

```yaml
on:
  schedule: # Delete "#" at line start
    - cron: "25 2 * * *" # Delete "#" at line start, and edit the scheduled time is recommended, the first number is minute, the second num is hour (+8 timezone by default).
  push:
    branches:
      - master
```

Attention：`yml` file requires correctly **indented**, please keep spaces correctly.

# Using GitHub `Star` button to trigger Actions

```yaml
#  watch: # Delete "#" at line start
#    types: started # Delete "#" at line start
```

# Notes

- Sometimes Epic add more free games randomly, and the script may fail, GitHub doesn't support auto-rerun, so the scheduled time is every day.

- After several tests, if the yaml only config cron trigger, GitHub won't create Actions correctly, so the `on-push` trigger is added.

- GitHub Actions Schedule is not exactly, 5~10 mins delay is normal.
