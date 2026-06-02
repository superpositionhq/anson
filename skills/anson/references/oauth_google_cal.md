# Google Calendar setup

If you already authorized `gog` for Gmail (`oauth_gmail.md`), you likely have Calendar access for free — `gog`'s default scope set includes Calendar read.

## If Calendar isn't authorized

Re-add the account with explicit Calendar scope:

```bash
gog auth add <email-address> --scopes calendar
```

(or `--scopes calendar.readonly` for read-only)

## Find your calendar IDs

Most people use just their primary calendar. List all calendars:

```bash
gog -a <email> calendar list-calendars
```

Note the IDs of the ones you actually want surfaced (usually `primary` is enough).

## Verify

```bash
python3 scripts/verify_gcal.py <email1> <email2>
```

Lists today's events.

## Multiple calendars per account

If you've got separate Work / Personal / Travel calendars within one account, list them in the `AGENTS.md` calendar table when the calendar integration is wired in Stage D — skills consult that table.
