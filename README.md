<h2>Overview</h2>
This is the official repository of Spurtcommerce. Using these Docker Images, you can easily deploy Spurtcommerce Multi-Vendor Marketplace in your local server.
<h2>Start Spurtcommerce with Docker Compose</h2>
By following these two simple commands, you can quickly launch Spurtcommerce in your local server. 
<br>

Additionally, you should have <code> docker </code> and <code> docker-compose </code> installed on your system.

If you have not yet installed Docker in your local server, then follow this first step. <br><br>

<pre><code> $ sudo snap install docker </code></pre>
  
<h3>Step 1 :  </h3>

<pre><code> $ git clone https://github.com/spurtcommerce/docker-spurtcommerce.git </code></pre><br>

Having already built the Docker images you can run docker compose without the --build flag.

<h3>Step 2 : </h3>
<pre><code> $ sudo docker compose up </code></pre>
<br>


<h2> Spurtcommerce port </h2>
Your local Spurtcommerce setup is now running with each of the services occupying the following ports:
<br><br>

<table>
<thead>
<tr>
<th align="center">Parameter</th>
<th>Function</th>
</tr>
</thead>
<tbody>
<tr>
<td align="center"><code>-p 8000</code></td>
<td>The port for the spurtcommerce api</td>
</tr>
<tr>
<td align="center"><code>-p 3000/admin</code></td>
<td>Angular Frontend - Admin</td>
</tr>
</tr>
<tr>
<td align="center"><code>-p 3000</code></td>
<td>Angular Frontend - Seller</td>
</tr>


</tbody>
</table>

Then SpurtCommerce Is Ready On localhost:{your-port} or default localhost/(hostname)


<h2>Avilable Images</h2>

Spurtcommerce maintains multiple build images for testing new development as well as supporting legacy builds. Each image uses a different version of Ubuntu Linux, with a slightly different list of included language and software versions.
<br>The following image is currently available:
<br><br>


* <b> Marketplace API:</b> [https://hub.docker.com/repository/docker/spurtcommerce/marketplace-api/general](https://hub.docker.com/r/spurtcommerce/marketplace-api)

* <b> Web UI:</b> [https://hub.docker.com/r/spurtcommerce/web-ui](https://hub.docker.com/r/spurtcommerce/web-ui)

* <b> Database:</b> [https://hub.docker.com/r/spurtcommerce/database](https://hub.docker.com/r/spurtcommerce/database)


<br>

Should you require any premium support, feel free to write to support@spurtcommerce.com. 




---------------------------------------------------------------------------------------------------------------------

#!/bin/bash

# Update package index
echo "Updating package index..."
sudo apt-get update

# Install necessary packages for Docker installation
echo "Installing required dependencies..."
sudo apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release \
    sudo

# Add Docker's official GPG key
echo "Adding Docker's official GPG key..."
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Set up the Docker stable repository
echo "Setting up Docker repository..."
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Update package index again to include Docker packages
echo "Updating package index..."
sudo apt-get update

# Install Docker
echo "Installing Docker..."
sudo apt-get install -y docker-ce docker-ce-cli containerd.io

# Verify Docker installation
echo "Verifying Docker installation..."
sudo docker --version

# Add user to Docker group to run Docker without sudo (optional)
echo "Adding current user to Docker group..."
sudo usermod -aG docker $USER

# Inform user to log out and log back in to apply Docker group change
echo "You need to log out and log back in to apply Docker group change."

# Install Docker Compose (latest stable version)
echo "Installing Docker Compose..."
sudo curl -L "https://github.com/docker/compose/releases/download/$(curl -s https://api.github.com/repos/docker/compose/releases/latest | jq -r .tag_name)/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# Make Docker Compose binary executable
echo "Making Docker Compose executable..."
sudo chmod +x /usr/local/bin/docker-compose

# Verify Docker Compose installation
echo "Verifying Docker Compose installation..."
docker-compose --version

# Final message
echo "Docker and Docker Compose installation completed successfully!"



