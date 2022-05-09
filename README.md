# Test hashFiles Filter Pattern Patching

On GitHub Actions, hashFiles uses pattern matching. However, the pattern matching doesn't always
behave as expected. The pattern `[0-9]+` does not seem to match "one or more digits" as one might
expect.

Per the documentation for [hashFiles](https://docs.github.com/en/actions/learn-github-actions/expressions#hashfiles)
and [filter patterns](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#filter-pattern-cheat-sheet):
* `+`: Matches one or more of the preceding character.
* `[]` Matches one character listed in the brackets or included in ranges. Ranges can only include
`a-z`, `A-Z`, and `0-9`. For example, the range `[0-9a-z]` matches any digit or lowercase letter.
For example, `[CB]at` matches `Cat` or `Bat` and `[1-2]00` matches `100` and `200`.

One might expect the pattern `ABCDE-[0-9]+.txt` to match a file named `ABCDE-12345.txt`. However,
this repo demonstrates that it will not.

More verbose debugging can be done by [enabling step debug logging](https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/enabling-debug-logging#enabling-step-debug-logging).
