To install Docker on an Ubuntu server, follow these steps: Update Package Index and Install Dependencies. 

Update your local package index and install necessary packages for a secure connection to Docker's repository.

Code

```
    sudo apt update    sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
```

Add Docker's Official GPG Key.

Add the official GPG key for the Docker repository to ensure the authenticity of downloaded packages.

Code

```
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Add Docker APT Repository.

Add the Docker stable repository to your APT sources.

Code

```
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Install Docker Engine.

Update the package index again to include Docker's repository and then install Docker Engine, CLI, and Containerd.

Code

```
    sudo apt update   
    sudo apt install docker-ce docker-ce-cli containerd.io -y
```

- **Add User to Docker Group (Optional but Recommended):**

To run Docker commands without `sudo`, add your current user to the `docker` group. 

Code

```
    sudo usermod -aG docker $USER
```

You will need to log out and log back in for this change to take effect. Verify Docker Installation.

Check the Docker version to confirm successful installation.

Code

```
    docker --version
```

You can also run a test container to ensure Docker is functioning correctly.

Code

```
    docker run hello-world
```


- Add the `docker` group if it doesn't already exist:
    
    ```
     sudo groupadd docker
    ```
    
- Add the connected user "$USER" to the `docker` group. Change the user name to match your preferred user if you do not want to use your current user:
    
    ```
     sudo gpasswd -a $USER docker
    ```
    
- Either do a `newgrp docker` or log out/in to activate the changes to groups.
    
- You can use
    
    ```
     docker run hello-world
    ```
    
    to check if you can run Docker without `sudo`.

```
    sudo apt update        sudo apt install openssh-server
```

Confirm the SSH service is active.

Code

```
        sudo systemctl status ssh
```

- If you have a firewall (like `ufw`) enabled on Ubuntu, allow SSH connections:

Code

```
        sudo ufw allow ssh        sudo ufw enable
```


## Setting up Wi-Fi on an Ubuntu server via the command line typically involves using Netplan, which manages network configurations in recent Ubuntu versions.

1. Identify your wireless interface:

- List network interfaces to find your Wi-Fi device name (e.g., `wlan0`, `wlpXsY`):

Code

```
    ip a
```

or

Code

```
    ls /sys/class/net
```

2. Edit the Netplan configuration file:

Navigate to the Netplan directory.

Code

```
    cd /etc/netplan/
```

- Identify the Netplan configuration file (e.g., `01-network-manager-all.yaml` or `50-cloud-init.yaml`).
- Open the file for editing using a text editor like `nano`:

Code

```
    sudo nano your_netplan_file.yaml
```

3. Configure Wi-Fi in the Netplan file:

- Add or modify the Wi-Fi configuration within the file, replacing `your_wifi_interface`, `YOUR_SSID`, and `YOUR_PASSWORD` with your specific details:

Code

```
    network:      version: 2      renderer: networkd # or network-manager if applicable      wifis:        your_wifi_interface: # e.g., wlan0, wlp3s0          optional: true          access-points:            "YOUR_SSID": # The name of your Wi-Fi network              password: "YOUR_PASSWORD" # Your Wi-Fi password          dhcp4: true # Set to true for DHCP, false for static IP
```

- Ensure proper indentation in the YAML file.

4. Apply the changes:

Apply the Netplan configuration.

Code

```
    sudo netplan apply
```

5. Verify the connection:

- Check your IP address to confirm connectivity:

Code

```
    ip a show your_wifi_interface
```

or

Code

```
    hostname -I
```