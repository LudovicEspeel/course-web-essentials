# Virtual Machine

A **Virtual Machine (VM)** is a computing resource that uses software instead of a physical computer to run programs and deploy applications. One or more virtual "guest" machines run on a physical "host" machine. Each virtual machine runs its own operating system and functions separately from the other VMs, even when they are all running on the same host. 

**Docker** is a software platform that allows you to build, test and deploy applications quickly. Docker packages software into standardized units (*containers*) that have everything the software needs to run including libraries, system tools, code and runtime. 

Each student has his/her own VM on the server. In this VM we will use Docker to deploy the website.

:::warning 🔥Warning
First make sure you are connected to the `devbit` network.
:::

Next we will be making some one-time adjustments and installations on your VM. 

## Enable remote connection

To be able to connect to your VM you need to setup the connection with your GitHub ssh-key.

Open a terminal (e.g. Powerhell) and connect to your VM with username and ip address. Refer to the list on Toledo.

```bash
ssh <username>@<ip address>
```
Logging in for the first time can sometimes take a while.

*If asked if you want to continue, just type `yes`.*

You will be asked to enter your password.

It is strongly recommended to change your initial password as soon as possible after the first login. To do this, use the following command:
```bash
passwd
```
You will be prompted to enter your current password, followed by your new password twice. Make sure to remember your new password!

Now that you are connected to your VM and have a command line, enter the following commands to make remote access possible with your SSH key from GitHub:

```bash
sudo apt update
sudo apt install ssh-import-id 
ssh-import-id-gh <GitHub-username>
```

When you enter a sudo command for the first time in the terminal, you will be asked to enter your password.

## Install Docker

We use a script to install both Docker and Docker compose. Enter now this command:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
```

(Note: if the `curl` command is not known, enter first command `sudo apt install curl` to install.)

:::warning 🔥Warning
Depending on how many students install Docker simultaneously, this can take a while.

Please limit this to **6 students at the same time**.
:::

Next we need to add your username to Docker.

```bash
sudo adduser <username> docker
exit
```

With that last `exit` command you will disconnect from your VM and get the windows command prompt again.

You can close the terminal now.