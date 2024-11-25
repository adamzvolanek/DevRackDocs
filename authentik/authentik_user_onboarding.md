# New User Onboarding

This page covers the process of onboarding a new user to Alexandria via Authentik.

**Authentik is no longer deployed.**

## User Invitation

Login to an admin account to Authentik create an invitation using the following fields:

- Name: <User_Name>
- Expires: Use logic
- Flow: `enrollment-invitation`
- [X] Single use

Copy link to user for enrollment and send to user. **Ask user for email**

**BUG: User's cannot change their emails in Authentik!**

### User-View

User will fill out a username, password, and password-repeat. **Remember** password requirements! (Are posted on login). Upon user account creation, invitation will be deleted.

By default, user should have JellyFin, Jellyseerr, Cloud, Status, and docs.

## User Prompt

Ensure user click the cog-wheel at the top-right and setup 2FA!

## JellyFin Specific

Add user to "jellyfin_user" group in Authentik.

**BUG: This does not occur by default.**

To enable login directly to JellyFin, Alexandria Admin must input user password to respective user account in JellyFin manually.

## Jellyseer Specific

Currently, Jellyseerr references Jellyfin's user list, however on import, JellySeerr does not accept a SSO's JellyFin's users' passwords.

```bash
Failed login attempt from user with incorrect Jellyfin credentials {"account":{"ip":"<IP_HERE>","email":"<USER_NAME>","password":"__REDACTED__"}}
```

To enable Jellyseer support, Alexandria Admin must input user password to respective user account in JellyFin manually.

## Possible solution to local JellyFin login

https://www.reddit.com/r/selfhosted/comments/15wfmaz/jellyfin_authentik_duo_2fa_solution_tutorial/
