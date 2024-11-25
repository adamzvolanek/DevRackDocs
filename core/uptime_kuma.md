This page covers the setup of [Uptime-Kuma](https://uptime.kuma.pet/) in my docker-compose cloud stack.

## Setup

### Account Setup

Upon start of Uptime-Kuma, setup an account with a password to get started. After setup, head over to your account "Settings" at the top-right and
select "Security". Setup 2FA given this is an external application.

### Monitor Setup

If you plan on organizing or grouping different individual monitors under one grouped monitor, you can begin by clicking on "Add New Monitor" and selecting a Group for "Monitor Type". Give the group a friendly name and fill out the remainder of the fields. Note, the Group will poll the status of the individual monitors within it, not the end-points of the monitors themselves. Remember to select "Save" at the bottom.

To add individual monitors, select "Add New Monitor" and select an appropriate monitor type. Most commonly used option is HTTP(s) and fill out the fields appropriately. Select "Save" at the bottom and continue to add new monitors as needed.

You are welcome to setup Notifications, I setup an email SMTP relay using the following settings having also created an application specific email password:

- Notification Type: Email (SMTP)
- Friendly Name: <Fillout appropriately>
- Hostname: smtp.email.com
- Port: 465
- Security: TLS (465)
- SMTP username: Your email address
- SMTP password: Application specific email password
- From email: <Fillout appropriately>
- To Email: <Email to be sent to>

At the bottom you can toggle the email SMTP to be the default notification method along with appliying to all existing monitors. Applying it to all existing monitors will also add it to groups **and** individual monitors.
