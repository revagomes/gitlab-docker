# Boilerplate for Gitlab with Docker

Setup a Gitlab instance using Docker with easy by running only a few command line instructions.

## Depedencies

- Git
- Docker
- Docker Compose
- Make

## Usage

1- Run `git clone git@github.com:nyxtechnology/gitlab-docker.git`

2- Run `cd gitlab-docker`

3- Run `cp .env.example .env`

(update the environment variables if necessary).

4- Run `cp docker-compose.override.yml.example docker-compose.override.yml`.

5- Run `make up`

(make sure port 22,80,443 are available)

Note: The first launch of the service may take several minutes.

6- (Optional) Run `make logs` to follow the state of Gitlab installation process

(go grap a cup of tea, this process may take a while... press Ctrl+C to exit the log screen)

7- Run `sudo echo '127.0.0.1       gitlab.local' >> /etc/hosts`

(update local domain to reflect you setup in case you have changed `GITLAB_HOST` variable in `.env` file)

8- Run `make getpass` and copy the password for root account

(command output is similar to: `/etc/gitlab/initial_root_password:Password: BFDCwgfG3MUJ1Ilvy6170iW+1ffoQr7RK4msOzKxgMw=`)

9- Access http://gitlab.local on your browser

10- Log in using 'root' as username and the password from step 8


## Configure Gitlab Runner

1- Once logged in, go to 'http://gitlab.local/admin/runners'

2- Click the 'Register an instance runner' button and copy the registration key/token

2- Back to the terminal, run `make runner-setup` to initiate gitlab-runner register module

A configuration process will take place. The module provides the following information:

- **Enter the GitLab instance URL:** confirm the entered value (click enter)
- **Enter the registration token:** enter the token copied before.
- **Enter a description for the runner:** enter the name of the runner, e.g. docker-runner
- **Enter tags for the runner:** you can leave the field blank here
- **Enter an executor:** enter docker here
- **Enter the default Docker image:** here we provide the default docker image, e.g. php:8.2.3-apache

After proper configuration, we should see a confirmation message "Runner registred successfully".

3- Run `make runner-network` to define 'gitlab-network' for gitlab-runners

