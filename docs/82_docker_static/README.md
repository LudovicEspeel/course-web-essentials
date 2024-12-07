# Deploy a HTML, CSS & JS project

:::warning 🔥Warning
Make sure you have prepared your VM before continuing here.
:::

## Prepare your project for deployment

To be able to deploy our website on the VM, we need to prepare it.

:::tip 💡Tip
Please check if all your URL's are relative (HTML, CSS and JS) on your website.
:::

### Create a GitHub repository for deployment

Steps to take if you **do not have a repository yet**:

1. Create a new repository on GitHub.
2. Create a local folder `<project-name>` with a subfolder `website`
3. Make a copy of your project to the folder `website`
4. Open the folder `<project-name>` in Visual Code and open a terminal.
5. Make it a git repository by typing `git init`
6. Add the remote GitHub repository by typing `git remote add origin git@github.com:yourGitHubUsername/repositoryname.git` (the last part is your SSH link from your GitHub repository).
7. Make a first push.

Steps to take if you **already have a repository** (e.g. created via an invitation link on Toledo):

1. Do a `git clone <ssh-url>`
2. In your cloned local folder, create a subfolder `website`
3. Make a copy of your project to the folder `website`
4. Open the folder `<project-name>` in Visual Code and open a terminal.
5. Make a first push.

### Create a docker-compose file

We will be deploying our website in a docker container, so the first thing we need to do is make a docker-compose file containing the information of how to deploy this project.

Create a file `docker-compose.yml` in the folder  `<project-name>` with the following content:

``` yaml
version: '3'
services:
  httpd:
    image: httpd:latest
    ports:
      - "80:80"
    volumes:
      - ./website:/usr/local/apache2/htdocs
    restart: always
```
* `version: '3'` specifies that Docker Compose version 3 is being used. This setting seems to be optional with newer Docker versions ...
* `httpd:` refers to the Apache HTTP Server, which is defined here as a service.
* `services:` indicates that the following configuration describes the services to be deployed by Docker Compose.
* `volumes:` maps a folder on the host machine to a folder inside the container. Here, `./website` (relative to the location of the `docker-compose.yml` file) is mapped to `/usr/local/apache2/htdocs` inside the container, which is Apache's default webroot.
* `restart: always` instructs Docker to always try to restart this service unless it was explicitly stopped by an administrator.
* `ports:`: defines the mapping between the host machine's port (external) and the container's port (internal). In this case, port 80 on the host is mapped to port 80 inside the container.

Now the preperation is ready, **push now everything to GitHub**.

## Clone and deploy your project in the VM

1. Open a `powershell` and connect to your VM by the ssh command.
2. Now you need to clone your docker repo, by using the https link of your GitHub repository: `git clone <https-link-repo>` (If you've already cloned the repository before, just use `git pull`).
3. Go to your folder `<project-name>`
   * If you want to see the subfolders and files below a folder, use the command `ls`
   * Go to a subfolder using the command `cd <folder name>`
4. The only thing left to do is deploying your website by starting the docker container.
   * To start: `docker compose up -d`
   * To stop: `docker compose down`
   * To view logs: `docker compose ps`
   * To view a list of the containers: `docker compose ls`

Now everyone connected to the `devbit` network can access your website through its ip address.