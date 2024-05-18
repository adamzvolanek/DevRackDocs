# PingVin Share

This page covers the configuration of the [PingVin-Share](https://github.com/stonith404/pingvin-share) as an upload and download file-sharing application.

## Manual Setup

Steps here cover the manual configuration of the PingVin-Share application.

### Configuration

Select "Get started" and enter the following fields:

- Username: Admin
- Email: email+pingvin+admin@domain.tld
- Password: Admin Password

Select "Customize configuration" and update the fields:

- App name: Alexandria File Exchange
- App URL: `http:${SERVER_IP}:${PingvinPort}`
- [ ] Show home page
- Logo: Select logo
- Select "Save"

On the left side, select "SMTP".

- [X] Enabled
- Host: smtp.gmail.com
- Port: 465
- Email: fileExchange@alexandria.com
- Username: email@domain.tld
- Password: App Password

Select "Save" and "Send test email". Select "Email" on the left-side.

- [X] Enable share email recipients
- Share recipients subject: Alexandria File Exchange Files Shared With You
- Share recipients message:
  - 
        Hey!
        
        {creator} shared some files with you, view or download the files with this link: {shareUrl}
        
        The share will expire {expires}.
        
        Note: {desc}
        
        Shared securely with Pingvin Share 🐧 via Alexandria

- Reverse share subject: Alexandria Reverse share link used
- Reverse share message:
  - 
        Hey!
        
        A share was just created with your reverse share link: {shareUrl}
        
        Shared securely with Pingvin Share 🐧 via Alexandria

- Reset password subject: Alexandria File Exchange password reset
- Reset password message:
  - 
        Hey!
        
        You requested a password reset. Click this link to reset your password: {url}
        
        The link expires in a hour.

        Pingvin Share 🐧via Alexandria

- Invite subject: Alexandria File Exchange Share Invite
- Invite message:
  - 
        Hey!

        You were invited to Alexandria File Exchange. Click this link to accept the invite: {url}

        Your password is: {password}

        Pingvin Share 🐧via Alexandria

Select "Share" on the left-side.

- [ ] Allow registration
- [ ] Allow unauthenticated shares
- Max expiration: 0
- Max size: 10000000000
- Zip compression level: 8
- Chunk size: 10000000

Select "Social Login".

- [ ] Allow registration
- [ ] Ignore TOTP

Leave the remainder of login options empty.

### Accounts

#### TOTP

Select "My Account" at the top-right, scroll to Security section.

Enter *Admin account password* to enable TOTP. Follow steps to continue TOTP setup.

#### User Account

As admin, select "Administration" at the top-right and then "User Management". Click "Create" at top-right and provide Username and Email.

Email recipient will automatically receive a password. To update, select "My Account" at the top-right, scroll to Password section.

### Authentik Setup

https://www.reddit.com/r/Authentik/comments/1c8tz5g/pingvin_share_with_authentik/
