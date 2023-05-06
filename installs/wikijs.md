# WikiJS

While many tools exist for documenting softare, tooling, etc. I am test running WikiJS however [BookStack](https://www.bookstackapp.com/) is a strong contender and I may switch to in time.

## Prerequisite

This WikiJS instance is deployed using [Docker Desktop](https://www.docker.com/products/docker-desktop/) on my Windows PC. Remember to enable virtulization in your computers BIOS.

## Docker-Compose

You can view the docker-compose file on Git [here](https://adamzvolanek.github.io/alexandria_splash_page/)

### Admin Configuration

- Access WikiJS via localhost or port as needed.
- Enter desired administration email address
- Generate strong password for adminstrator
- Enter desired domain (this can be changed later)

### Git Storage Configuration

- Setup/Verify GitHub profile includes SSH Key (Deploy Key)
  - Generated using these [instructions](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key)
    - Be sure to name the deploy key to something recognizable to the application.
- Follow WikiJS instructions [here](https://docs.requarks.io/en/storage/git) and scroll to the "Configure Wiki.js".

## Tips

Open the dockers terminal and navigate to `/wiki/data/repo` to locate default location for Git installation.

1. To open terminal in Docker Desktop, select the respective container and click on its name.
2. Click on the 'Terminal' tab, it should look like this: ![image.png](/image.png){.align-center}
