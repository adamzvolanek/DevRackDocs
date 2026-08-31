While many tools exist for documenting softare, tooling, etc. I am test running WikiJS however [BookStack](https://www.bookstackapp.com/) is a strong contender, I am using WikiJS going forward due to GitHub integration.

## Admin Configuration

- Access WikiJS via server IP and port defined in docker compose.
- Enter desired administration email address
- Generate strong password for adminstrator
- Enter desired domain (this can be changed later)

### WikiJS Configuration

In the adminstration tab, navigate to the dashboard. Select the green Apply button at the top after each section.

#### General

1. Verify "Site URL" is accurate.
2. Update "Site Title" accordingly.
3. Update logo or define a URL.
4. Under SEO, check "No Index" and "No Follow"
5. Turn off comments.

#### Locale

Skipping for future implementation.

#### Navigation

Select 'Custom Navigation' and begin generating a navigation tree.

#### Theme

Enable Dark Mode.

#### Git Storage Configuration

1. Check the "Git" Targets
2. Ensure "Authentication Type" is ssh
3. Paste in the "Repository URI"
4. Define "Branch" as `main`.
5. For "SSH Private Key Mode" to be `path`.
6. Open terminal and navigate to the servers wikijs volume mount.
8. Create the .ssh directory in local: `mkdir -p /local/.ssh`
8. Run `ssh-keygen -t rsa -b 4096`
  9. Set the path to `/local/.ssh/id_rsa`
10. Update ssh key in Git as authentication key.
11. In the WikiJS container, update the git safe directories: `git config --global --add safe.directory /local/repo`
12. Select Apply in WikiJS configuration.

#### Navigation Setup

- Select 'Site Tree'

#### Email Configuration

- Under System -> Mail, enter the Sender name and Sender Email fields
- Configure your 'SMTP Settings' as needed. Use a app-seicific password.

#### Security

1. Enable "Enforce HSTS"
  2. Set HSTS Max Age to one day.
