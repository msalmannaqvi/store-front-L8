# store-front

This is a Vue.js app that simulates a store front. It is meant to be used in conjunction with the product-service and order-service. The app is extremely simple in that it only has a cart and a order submission button. When the order submission button is clicked, the cart is emptied and the order is sent to the order service. Currently there is no order checkout pages to collect any customer information.  

## Running the app locally

### Prerequisites

- [Node.js](https://nodejs.org/en/download/)
- [Vue CLI Service](https://cli.vuejs.org/guide/cli-service.html)
- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)


### Complete Set of Commands for CENTOS stream 9
# Add the Node.js 18.x repository
curl -fsSL https://rpm.nodesource.com/setup_18.x | sudo bash -

# Install Node.js and npm
sudo dnf install -y nodejs

# Verify installation
node -v
npm -v
# Install Vue CLI globally
sudo npm install -g @vue/cli

# Verify installation
vue --version

# Remove any older versions of Docker
sudo dnf remove -y docker docker-client docker-client-latest docker-common docker-latest docker-latest-logrotate docker-logrotate docker-engine

# Set up the Docker repository
sudo dnf -y install dnf-plugins-core
sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

# Install Docker Engine
sudo dnf install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Start and enable Docker
sudo systemctl start docker
sudo systemctl enable docker

# Verify installation
docker --version

# Download the latest version of Docker Compose
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# Apply executable permissions
sudo chmod +x /usr/local/bin/docker-compose

# Verify installation
docker-compose --version

# Add Docker to Non-root Users (Optional) but highly recomended

# Add your user to the Docker group
sudo usermod -aG docker $USER

# Apply the group changes
newgrp docker



### Running the app

The app relies on the product-service and the order-service and the rabbitmq instance running. A docker-compose file is provided to make this easy.

To run the necessary services, clone the repo, open a terminal, and navigate to the `store-front` directory. Then run the following command:

```bash
docker compose up
```

With the services running, open a new terminal and navigate to the `store-front` directory. Then run the following commands:

```bash
export VUE_APP_PRODUCT_SERVICE_URL=http://localhost:3002/
export VUE_APP_ORDER_SERVICE_URL=http://localhost:3000/

npm install
npm run serve
```

When the app is running, you should see output similar to the following:

```text
  App running at:
  - Local:   http://localhost:8080/ 
  - Network: http://192.168.0.144:8080/

  Note that the development build is not optimized.
  To create a production build, run npm run build.
```

Open a browser and navigate to `http://localhost:8080/`. You should see the store front app running.
