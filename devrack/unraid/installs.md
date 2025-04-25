This section includes the installation documentation for many of my dockers and plugins running on Alexandria.

Be sure to review the [writing standards](./writing_standards) to understand the various markdown styling is used.

## Setup Docker Compose on Unraid

Pre-requisite includes installing the docker compose plugin under the Community "Apps" tab.

## Creating a Docker Compose Stack

Note, the dockers will not have their `appdata` directories created until initial startup. Create a docker-compose stack by selecting "Add New Stack" and provide a relevant `stack_name`. Populate the stack directory with corresponding directory to GitHub, e.g. cloud, external, etc.

Select the cog wheel ![Unraid Docker Compose Cog Wheel](unraid-docker-compose-cog-wheel.png) and click "Edit description" to edit the description of the stack with a relevant description. It is best to leave the location of the docker-compose stacks. e.g. `/boot/config/plugins/compose.manager/projects/<stack_name>`.

Select the cog wheel ![Unraid Docker Compose Cog Wheel](unraid-docker-compose-cog-wheel.png) and click "Edit Stack" and then "Compose File". Paste the contents of the respective compose file. Select "Save Changes".

Select the cog wheel ![Unraid Docker Compose Cog Wheel](unraid-docker-compose-cog-wheel.png) and click "Edit Stack" and then "Env File". Paste the contents of the environment file as referenced in the docker-compose file. Note, this may also require the use of [`server.env`](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/server.env) to be pasted in the same box. Update the values as needed for respective Unraid server.

## Auto Start

Prerequisite, have the docker-compose stack up and running. Turn on the Auto Start toggle ![Unraid Auto Start Toggle](unraid-docker-compose-autostart.png) both on the stack and the running container in the Docker Containers section.
