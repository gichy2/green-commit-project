# green-commit

The `task.sh` script generates random commit messages and updates an `update.md` file in your repository with the last update timestamp. It's a fun way to automate your daily commits while keeping your GitHub contribution graph green.

## How it works

1. The script defines an array of commit messages, each with an emoji and a short description.

2. It generates a random number to select a message from the array.

3. It gets the current date and time.

4. If the `update.md` file doesn't exist, it creates it and stages it for commit.

5. It appends the last update timestamp to the `update.md` file.

6. It uses the Git identity configured by the workflow (or your local Git configuration when run locally).

7. Finally, it commits the changes to the repository with a random commit message and the current timestamp.

## Automated commits to your GitHub account

The workflow uses GitHub Actions' automatically provided `GITHUB_TOKEN` to push commits, so no password or personal access token needs to be stored in this repository. It requests `contents: write` permission and sets the commit author to the GitHub account that triggered the workflow.

If pushes are denied, check **Settings → Actions → General → Workflow permissions** and allow read and write permissions. Scheduled runs are attributed to the account that configured the schedule; manually started runs are attributed to the account that starts them. Contribution graph credit also depends on GitHub's contribution rules.

## Customize

- For local runs, configure Git with your account's name and verified email using `git config --global user.name "Your Name"` and `git config --global user.email "your-verified-email@example.com"`.
- Change the [cron schedule](.github/workflows/bot.yml) to adjust automation. (Refer to [crontab.guru](https://crontab.guru/).)
- Modify the [messages array](task.sh) to include your own commit messages.

## Notes

- GitHub Actions runs on Coordinated Universal Time (UTC) time, so commit timestamps will be in UTC, affecting your GitHub contribution graph based on UTC time instead of your local time zone.
