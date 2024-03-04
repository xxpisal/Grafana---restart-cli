# grafana start servive 
to start the service, run the following commands:
```bash

  sudo systemctl daemon-reload
  sudo systemctl start grafana-server
  sudo systemctl status grafana-server

# To verify that the service is running, run the following command:
```bash

  sudo systemctl status grafana-server


# Configure the Grafana server to start at boot using systemd
To configure the Grafana server to start at boot, run the following command:

```bash
  
  sudo systemctl enable grafana-server.service

    #Serve Grafana on a port < 1024
    # Run the following command to create an override file in your configured editor.

  ```bash
  
      grafana-server.service.d/override.conf
      sudo systemctl edit grafana-server.service

  # Add the following additional settings to grant the CAP_NET_BIND_SERVICE capability.
      
  +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
      [Service]
      # Give the CAP_NET_BIND_SERVICE capability
      CapabilityBoundingSet=CAP_NET_BIND_SERVICE
      AmbientCapabilities=CAP_NET_BIND_SERVICE

      # A private user cannot have process capabilities on the host's user
      # namespace and thus CAP_NET_BIND_SERVICE has no effect.
      PrivateUsers=false
  +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
  
# Restart the Grafana server using systemd
  ```bash
      
      sudo systemctl restart grafana-server

# Start the Grafana server using init.d
  To start the Grafana server, run the following commands:

```bash 

    sudo service grafana-server start
    sudo service grafana-server status


  To verify that the service is running, run the following command:

    sudo service grafana-server status

# Configure the Grafana server to start at boot using init.d

```bash

    sudo update-rc.d grafana-server defaults

  Restart the Grafana server using init.d

    sudo service grafana-server restart

  Start the server using the binary

  ```bash
    
    ./bin/grafana server

# Docker
  
  To restart the Grafana service, use the docker restart command.

    docker restart grafana

# Docker compose example
    
    Configure your docker-compose.yml file. For example:

```bash
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
version: "3.8"
services:
  grafana:
    image: grafana/grafana:latest
    container_name: grafana
    restart: unless-stopped
    environment:
      - TERM=linux
      - GF_INSTALL_PLUGINS=grafana-clock-panel,grafana-polystat-panel
    ports:
      - '3000:3000'
    volumes:
      - 'grafana_storage:/var/lib/grafana'
volumes:
  grafana_storage: {}
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

  Start the Grafana server:

      docker compose up -d

  This starts the Grafana server container in detached mode along with the two plugins specified in the YAML file.

To restart the running container, use this command:

    docker compose restart grafana
    