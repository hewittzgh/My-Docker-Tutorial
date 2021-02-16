---
sort: 2
---

# Configure Docker

> After Docker is successfully installed, some configuration is required to get a better experience.  

> The official tutorial link: [here](https://docs.docker.com/engine/install/linux-postinstall/)  

## Manage Docker as a non-root user
```note
The Docker daemon binds to a Unix socket instead of a TCP port. By default taht Unix socket is owned by the user root and other users can only access it using `sudo`. The Docker daemon always runs as the `root` user. If you don't want to preface the docker command with `sudo`, create a Unix group called `docker` and users to it. When the Docker daemon starts, it creates a Unix socket accessible by members of the `docker` group.
```

```tip
Rootless mode is currently available as an experimental feature, so don't try to run Docker without root privileges. For more information, please check the [official tutorial](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user).
```
To create the `docker` group and add your user:
- Create the `docker` group: `$ sudo groupadd docker`  
- Add your user to the `docker` group: `$ sudo usermod -aG docker $USER`  
- Log out and log back in so that your group membership is re-evaluated.  
```tip
1. If testing on a **virtual machine**, it may be necessary to restart the virtual machine for changes to take effect.  
2. On a **desktop Linux environment** such as **X Windows**, log out of your session completely and then log back in.  
3. On **Linux**, you can also run the following command to activate the changes to groups: `$ newgrp docker`.  
```
- Verify that you can run `docker` commands without `sudo`: `$ docker run hello-world`  

```warning
If you initially ran Docker CLI commands using `sudo` before adding your user to the `docker` group, you may see the following error, which indicates that your `~/.docker` directory was created with incorrect permissions due to the `sudo` commands:  
    `WARNING: Error loading config file: /home/user/.docker/config.json -`  
    `stat /home/user/.docker/config.json: permission denied`  
To fix this problem, either remove the `~/.docker/` directory(it is recreated automatically, but any custom settings are lost), or change its ownership and permissons using the following commands:  
    `$ sudo chown "$USER":"USER" /home/"USER"/.docker -R`  
    `$ sudo chmod g+rwx "$HOME/.docker" -R`  
```

## Configure Docker to start on boot
```note
1. **Ubuntu16.04 and higher** use `systemd` to manage which services start when the system boots.  
2. On **Debian and Ubuntu**, the Docker service is configured to start on boot by default.  
```

## Next Step