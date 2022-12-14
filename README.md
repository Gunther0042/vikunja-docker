# Vikunja Docker-Compose Template

### Motivation
[Vikunja](https://vikunja.io/) is a really great, open-source, self-hostable to-do application. However, I found its setup documentation to be a bit confusing and based on some posts on Reddit and the project's forums, I don't think I'm the only one. I decided to create a Github repo with a Vikunja docker setup that can be implemented with a few commands. I've endeavored to make this guide as idiot-proof as possible :smiley:

### Disclaimers
This repo is meant to be a supplement to the [Vikunja docs](https://vikunja.io/docs/), not a replacement for them. The `docker-compose.yml` and `nginx.conf` files used here are identical to the ones found in the [Docker Walkthrough](https://vikunja.io/docs/docker-walkthrough/) in the docs, with the exception of some additional environment variables in the `docker-compose.yml` file I thought might be useful.

I'm a relative novice when it comes to Docker and web hosting, so feedback is welcome. Issues with Vikunja itself should be directed to the [Vikunja repos](https://kolaente.dev/vikunja). I have my Vikunja instance set up behind an nginx reverse proxy and the configuration here worked for me, but it is possible it will not be compatible with your setup.

### Setup Instructions
The following assumes you have a linux machine with a sudo user to host your Vikunja instance on, and docker, docker-compose, and git already installed.

Navigate to where you want the project directory to live (`cd ~` is a good default choice if you are unsure).
Then clone this Github repo to that location and enter the directory.
```bash
git clone https://github.com/Gunther0042/vikunja-docker.git
cd vikunja-docker
```

Next, copy the `.env-template` file to `.env`. This will allow you to change the environment variables without worrying about overwriting them if you ever reclone the repo.
```bash
cp .env-template .env
```
At this point, feel free to use a text editor like nano to edit the environment variables in `.env`. The container should run fine with the defaults, but I would recommend at least changing the MYSQL root and user passwords. You may also want to change the external port if you do not want to host your Vikunja instance on port 80.

You're now ready to spin up your docker container. To do so, use the following commands.
```bash
sudo docker-compose pull && sudo docker-compose up -d
```
At this point, your Vikunja docker container should be up and running!

If you ran into any trouble following the setup instructions, feel free to create an issue on this repo. However, there's a good chance the problem will be beyond my ability to solve and I'll instead redirect you to the Vikunja dev, who is pretty friendly and responsive to questions.

### Useful Tips
Here are some commands I found useful for debugging and/or after I had my Vikunja docker container working.

To update your Docker container to the latest Vikunja version after a new release, simply navigate to the project directory and rerun the commands to start the container.
```bash
sudo docker-compose pull && sudo docker-compose up -d
```
You can also use something like [Watchtower](https://containrrr.dev/watchtower/) to automate updates of your Docker containers.

To use the [Vikunja CLI](https://vikunja.io/docs/cli/), enter the following command.
```bash
sudo docker-compose exec api /app/vikunja/vikunja <vikunja subcommand>
```

You can make using the CLI easier to use by making an alias for the command. To do that, add the following line to your `.bashrc` file.
```bash
alias vikunja='sudo docker-compose exec api /app/vikunja/vikunja'
```

If you need to access Vikunja's logs, use the following command.
```bash
sudo docker-compose logs -f
```
