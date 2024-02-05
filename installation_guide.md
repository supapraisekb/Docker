# Steps to Install docker on Ubuntu

# 1. Uninstall old versions

Before you can install Docker Engine, you need to uninstall any conflicting packages.

run this code:

```
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

# 2. Install using the apt repository

Before you install Docker Engine for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

run this code: 

```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
# 3. Install the Docker packages.

- To install the latest version, run this code:

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

- To install a specific version of Docker Engine, first list the available versions using this code:

```
# List the available versions:
apt-cache madison docker-ce | awk '{ print $3 }'

5:24.0.0-1~ubuntu.22.04~jammy
5:23.0.6-1~ubuntu.22.04~jammy
...
```

- Then Use this code to select the one you want to install

```
VERSION_STRING=5:24.0.0-1~ubuntu.22.04~jammy
sudo apt-get install docker-ce=$VERSION_STRING docker-ce-cli=$VERSION_STRING containerd.io docker-buildx-plugin docker-compose-plugin

```

# 4. Verify that the Docker Engine installation is successful by running the hello-world image.

Use this code: 

```
sudo docker run hello-world

```

# 5. Uninstall Docker Engine

- Uninstall the Docker Engine, CLI, containerd, and Docker Compose packages using this code

```
sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras
```

- Images, containers, volumes, or custom configuration files on your host aren't automatically removed. To delete all images, containers, and volumes use this code: 

```
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```