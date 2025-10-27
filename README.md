# Install-Kathara-on-CentOS-Stream-10
Instructions on how to install Kathara on CentOS Stream 10

# Install Kathara
- Install the repository management tool:<br>
sudo dnf -y install dnf-plugins-core

- Add official Docker repository:<br>
sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

- Install the latest version of Docker Engine:<br>
sudo dnf install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

- Start and enable Docker to automatically run on boot:<br>
sudo systemctl start docker<br>
sudo systemctl enable docker

- Add your user to the docker group to run Kathara (and Docker) without sudo:<br>
sudo usermod -aG docker $USER

- You need to log out and log in again for this change to take effect.

- CentOS's default firewall will conflict with the way Kathara manages Docker's network. You'll need to disable it:<br>
sudo systemctl stop firewalld<br>
sudo systemctl disable firewalld

- Go to https://www.kathara.org/download.html, find the Red Hat-Based section and click the link for your architecture (kathara-*.rpm).

- Use dnf to install this .rpm file:<br>
sudo dnf install ./Downloads/kathara-*.rpm

- Check if Kathara is working:<br>
kathara --version

- Kathara (by default) is configured to use a terminal emulator called xterm. You need to install xterm:<br>
sudo dnf install xterm

- Kathara needs a Docker image to create virtual machines:<br>
docker pull kathara/base
